---
title: spring-framework的issue-22675解决过程
date: 2019-05-14 23:39:52
tags:
  - spring-framework
  - Java
---

### 相关链接
- [spring-framework](https://github.com/spring-projects/spring-framework)
- [issue-22675](https://github.com/spring-projects/spring-framework/issues/22675)
- [issue-22675 相关的提问](https://stackoverflow.com/questions/46317961/primary-on-factory-beans)
- [我的PR](https://github.com/spring-projects/spring-framework/pull/22711)
- [修复版本5.2.0.M1](https://github.com/spring-projects/spring-framework/releases/tag/v5.2.0.M1)

### 问题描述
当同一个类有多个bean定义，Spring在注入的时候，不知道使用哪个bean定义，从而提示bean定义重复，应用也会启动失败。如果在其中一个bean定义加上@Primary注解，Spring就可以优先使用该bean定义，应用就可以正常启动运行。这是Spring已有的功能。

issue-22675 报告了一种特殊情况，在这个情况下这个功能无法生效，即@Primary不起作用。使用了@Primary之后，Spring还是提示了bean定义重复。这种特殊情况就是：@Primary作用在FactoryBean的bean定义。代码例子可以看上面的相关链接。

### 解决过程
#### 1. 准备阶段
因为这是我在Spring项目第一个bug的解决过程，所以我把准备阶段写的详细一点。一方面是为了总结，另一方面是给想参与开源项目的人一些指导。首先我的目标很明确：理解Spring源码、为Spring解决bug、进而希望为Spring实现新功能。有了这个目标之后，做了一些基础工作和学习积累。准备的内容有：
- 复习设计模式，看了《head first 设计模式》。因为最开始翻代码一脸迷茫，发现设计模式不熟悉，赶紧补上。
- 看Spring官方文档：要理解Spring源码，一定要先知道Spring能做什么，之前只是在项目上用Spring，对Spring能做的事情不够全面。这次看了文档前三部分，即看完 核心技术（Core Technologies）。
- 看《Spring源码深度解析》和《Spring技术内幕》，也只看了对应的核心部分：core、beans、context、aop、aspects这些模块。
- **（这个方法不可取，别学）**看模块的详细源码，当时是每个包都导出类的关系图（感谢Idea强大的功能），然后一个一个类地去看源码。看完了core模块的代码感觉还好，看beans模块两天直接放弃。
- 看《Expert One-on-One J2EE Development without EJB》，有了之前对Spring的初步理解，然后就看了这本经典著作。
- 再次学习Gradle，因为spring-frame项目是Gradle构建的。大学开发Android应用有Gradle使用经验，这次只是回头看一下基本用法。这里只是强调构建工具也是需要学习的一个方面。
	
有了这些准备，我就开始在GitHub上看Spring的issue了。没有捷径，一个一个地看，理解问题，看自己能不能解决。下面开始这个bug的解决过程。

#### 2. 知识回顾
虽然看了一遍Spring官方文档，但是遇到具体功能，还是不能立刻想起功能的作用和用法。根据issue的描述，我重新看了下面的内容：
- @Configuration和@Bean配置bean的方法
- @Primary的使用
- FactoryBean的使用方法，对于解决这个bug很关键。
	
#### 3. 构建测试demo
使用spring-boot搭建一个测试demo，准备开始代码调试之旅。（用spring-boot为了方便搭建，直接用原始的Spring也行）

#### 4. 调试
根据demo报错的调用栈，把栈上层的几个类和方法打上断点。然后在两种不同的情况（使用FactoryBean和不使用FactoryBean）下，不断调试代码。调试期间，看注释和上网搜索这些类和方法的作用，推测可能出现问题的类和方法。比较这两种情况，看哪里不一样。这个调试过程及其漫长和需要耐心。当然之前的准备和对源码的理解也派上了用场。（顺便说一下，Idea的调试功能太好用了，疯狂安利Idea）
面对一个大型的不熟悉的项目，这种调bug的方式，还是比较好用的。

#### 5. 调试结果
原来是bean别名和FactoryBean名称使用的问题。
在使用FactoryBean的时候，要获取FactoryBean创建的bean，只需要原始bean名称："beanName"，如果要获取FactoryBean本身，需要在前面加上"&",即bean名称为："&beanName"。
在使用别名搜索或获取bean的时候，系统要把别名转换成权威的名字（canonical name）,再用这个canonical name去做操作。
当用到bean的名称的时候，系统都需要把前面的&去掉，并且转换成canonical name，再进行其他操作。这个步骤由AbstractBeanFactory的transformedBeanName方法来完成的。下面举个例子
	
```java
AbstractBeanFactory.java
@Override
public boolean containsBean(String name) {
	String beanName = transformedBeanName(name);
	if (containsSingleton(beanName) || containsBeanDefinition(beanName)) {
		return (!BeanFactoryUtils.isFactoryDereference(name) || isFactoryBean(name));
	}
	// Not found -> check parent.
	BeanFactory parentBeanFactory = getParentBeanFactory();
	return (parentBeanFactory != null && parentBeanFactory.containsBean(originalBeanName(name)));
}```

上面这个方法根据bean的名称，查看bean是否在容器中。它不信任输入，认为输入的名称不一定是canonical name。所以它使用transformedBeanName进行了处理，拿到canonical name，再根据这个canonical name去看有没有包含相应的bean，所以没有出现问题。

```java
DefaultListableBeanFactory.java
protected boolean isPrimary(String beanName, Object beanInstance) {
	if (containsBeanDefinition(beanName)) {
		return getMergedLocalBeanDefinition(beanName).isPrimary();
	}
	BeanFactory parent = getParentBeanFactory();
	return (parent instanceof DefaultListableBeanFactory &&
			((DefaultListableBeanFactory) parent).isPrimary(beanName, beanInstance));
}```

而上面这个方法，在使用beanName之前没有做处理。如果输入是带"&"的名称或者是bean别名，根据bean名称找不到对应的bean定义，isPrimary将会为false。同一个类的全部bean定义的isPrimary都为false，Spring不知道选择哪个，就会出现issue描述中的问题（提示bean定义重复，应用启动失败）。

#### 6. 解决方法
分析到了这里，解决就变得简单了，使用beanName之前，先使用transformedBeanName处理一下。代码如下：

```java
protected boolean isPrimary(String beanName, Object beanInstance) {
	String transformedBeanName = transformedBeanName(beanName);
	if (containsBeanDefinition(transformedBeanName)) {
		return getMergedLocalBeanDefinition(transformedBeanName).isPrimary();
	}
	BeanFactory parent = getParentBeanFactory();
	return (parent instanceof DefaultListableBeanFactory &&
			((DefaultListableBeanFactory) parent).isPrimary(transformedBeanName, beanInstance));
}```


但是这就行了吗？当然不行！
时刻谨记，开源项目的代码将会被很多公司、组织和个人使用。添加代码之后，必须添加对应的测试代码。修改代码之后，必须运行之前的测试代码（回归测试）。我添加了两个测试用例，并且运行了那个包的所有测试用例，才提交代码，提PR。测试代码可以看上面的相关链接。
	
### 题外话
之前一直认为GitHub可以搜索一个人的全部code、comment、issue、pull request，没必要再写博客汇总自己做的一些事情。但是最近在tomcat邮件列表进行一些讨论后，越来越觉得GitHub的搜索功能并不能满足自己的全部需求。

一方面，自己参与和感兴趣的项目可能不在GitHub进行讨论。这些讨论分布在了GitHub、邮件、以及项目单独的issue tracker里面，很难汇总。另一方面，对问题的讨论过程和解决方法进行回顾和总结，可以加深对项目的理解。这种分享也可以启发和帮助到对相关问题有困惑的人。spring-framework的issue-22675是5月份解决的一个bug了，现在10月份再写解决过程，一些细节已经记不清楚了，只能粗略记录。这些细节的遗忘也说明了及时写博客的重要性。今后要坚持写博客，利人利己。

如非必要，我尽量不会贴一堆源码和对源码进行大量的分析。因为对于知名的开源项目，其主要的架构和源码已经有很多人分析并且写了博客或者出版了相关书籍。我主要想提供问题解决的思路和过程，为想参与开源项目的人提供一些指导。如果一些具体细节在网上搜索不到很好的分析过程，我也会进行一些分析。最主要是避免重复。现在用中文搜索技术问题，有些时候前半页都是一样的内容。虽然发布者会在里面加上一条引用或出处的链接，但是我感觉这种重复是很没必要和略不负责任的行为。
