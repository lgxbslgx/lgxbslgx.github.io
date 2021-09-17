---
title: OpenJDK Main-line Contribution Summary
date: 2020-11-20 14:39:15
tags:
  - OpenJDK
  - Java
  - Javac
  - hotspot
  - JVM
---

#### Related description and Links
The JDK Project is the JDK main-line development of OpenJDK.
- [Introduction](http://openjdk.java.net/projects/jdk)
- [Code Base](https://github.com/openjdk/jdk)


#### tool: javac
- [JDK-8254023](https://bugs.openjdk.java.net/browse/JDK-8254023) [PATCH](https://github.com/openjdk/jdk/pull/622)  A module declaration is not allowed to be a target of an annotation that lacks an @Target meta-annotation
- [JDK-8254557](https://bugs.openjdk.java.net/browse/JDK-8254557) [PATCH](https://github.com/openjdk/jdk/pull/718)  Compiler crashes with java.lang.AssertionError: isSubtype UNKNOWN
- [JDK-8255968](https://bugs.openjdk.java.net/browse/JDK-8255968) [PATCH](https://github.com/openjdk/jdk/pull/1389)  Confusing error message for inaccessible constructor
- [JDK-8257037](https://bugs.openjdk.java.net/browse/JDK-8257037) [PATCH](https://github.com/openjdk/jdk/pull/1490)  No javac warning when calling deprecated constructor with diamond
- [JDK-8245956](https://bugs.openjdk.java.net/browse/JDK-8245956) [PATCH](https://github.com/openjdk/jdk/pull/1553)  JavaCompiler still uses File API instead of Path API in a specific case
- [JDK-8231622](https://bugs.openjdk.java.net/browse/JDK-8231622) [PATCH](https://github.com/openjdk/jdk/pull/1626)  SuppressWarning("serial") ignored on field serialVersionUID
- [JDK-8257740](https://bugs.openjdk.java.net/browse/JDK-8257740) [PATCH](https://github.com/openjdk/jdk/pull/1648)  Compiler crash when compiling type annotation on multicatch inside lambda
- [JDK-8230623](https://bugs.openjdk.java.net/browse/JDK-8230623) [PATCH](https://github.com/openjdk/jdk/pull/1758)  Extract command-line help for -Xlint sub-options to new --help-lint
- [JDK-8258525](https://bugs.openjdk.java.net/browse/JDK-8258525) [PATCH](https://github.com/openjdk/jdk/pull/1732)  Some existing tests should use /nodynamiccopyright/ instead of the standard header
- [JDK-8258662](https://bugs.openjdk.java.net/browse/JDK-8258662) [PATCH](https://github.com/openjdk/jdk/pull/1849)  JDK 17ea: Crash compiling instanceof check involving sealed interface
- [JDK-8255729](https://bugs.openjdk.java.net/browse/JDK-8255729) [PATCH](https://github.com/openjdk/jdk/pull/1854)  com.sun.tools.javac.processing.JavacFiler.FilerOutputStream is inefficient
- [JDK-8225003](https://bugs.openjdk.java.net/browse/JDK-8225003) [PATCH](https://github.com/openjdk/jdk/pull/1864)  NPE in Attr.attribIdentAsEnumType
- [JDK-8239596](https://bugs.openjdk.java.net/browse/JDK-8239596) [PATCH](https://github.com/openjdk/jdk/pull/1881)  PARAMETER annotation on receiver type does not cause error
- [JDK-8226216](https://bugs.openjdk.java.net/browse/JDK-8226216) [PATCH](https://github.com/openjdk/jdk/pull/1890)  parameter modifiers are not visible to javac plugins across compilation boundaries
- [JDK-8216400](https://bugs.openjdk.java.net/browse/JDK-8216400) [PATCH](https://github.com/openjdk/jdk/pull/1895)  improve handling of IOExceptions in JavaCompiler.close()
- [JDK-8198317](https://bugs.openjdk.java.net/browse/JDK-8198317) [PATCH](https://github.com/openjdk/jdk/pull/1896)  Enhance JavacTool.getTask for flexibility
- [JDK-8057543](https://bugs.openjdk.java.net/browse/JDK-8057543) [PATCH](https://github.com/openjdk/jdk/pull/1898)  Replace javac's Filter with Predicate (and lambdas)
- [JDK-8255757](https://bugs.openjdk.java.net/browse/JDK-8255757) [PATCH](https://github.com/openjdk/jdk/pull/1912)  Javac emits duplicate pool entries on array::clone
- [JDK-8259025](https://bugs.openjdk.java.net/browse/JDK-8259025) [PATCH](https://github.com/openjdk/jdk/pull/1917)  Record compact constructor using Objects.requireNonNull
- [JDK-8150303](https://bugs.openjdk.java.net/browse/JDK-8150303) [PATCH](https://github.com/openjdk/jdk/pull/1959)  Rewrite test/tools/javac/Paths/Diagnostics.sh
- [JDK-8203925](https://bugs.openjdk.java.net/browse/JDK-8203925) [PATCH](https://github.com/openjdk/jdk/pull/1998)  tools/javac/importscope/T8193717.java ran out of java heap
- [JDK-8231179](https://bugs.openjdk.java.net/browse/JDK-8231179) [PATCH](https://github.com/openjdk/jdk/pull/2004)  Investigate why tools/javac/options/BCPOrSystemNotSpecified.java fails on Window
- [JDK-8259359](https://bugs.openjdk.java.net/browse/JDK-8259359) [PATCH](https://github.com/openjdk/jdk/pull/2021)  javac does not attribute unexpected super constructor invocation qualifier, and may crash
- [JDK-8236490](https://bugs.openjdk.java.net/browse/JDK-8236490) [PATCH](https://github.com/openjdk/jdk/pull/2060)  Compiler bug relating to @NonNull annotation
- [JDK-8232765](https://bugs.openjdk.java.net/browse/JDK-8232765) [PATCH](https://github.com/openjdk/jdk/pull/2099)  NullPointerException at Types.eraseNotNeeded() when compiling a class
- [JDK-8213766](https://bugs.openjdk.java.net/browse/JDK-8213766) [PATCH](https://github.com/openjdk/jdk/pull/2118)  Assertion error in TypeAnnotations$TypeAnnotationPositions.resolveFrame
- [JDK-8260053](https://bugs.openjdk.java.net/browse/JDK-8260053) [PATCH](https://github.com/openjdk/jdk/pull/2169)  Optimize Tokens' use of Names
- [JDK-8260566](https://bugs.openjdk.java.net/browse/JDK-8260566) [PATCH](https://github.com/openjdk/jdk/pull/2311)  Pattern type X is a subtype of expression type Y message is incorrect
- [JDK-8200145](https://bugs.openjdk.java.net/browse/JDK-8200145) [PATCH](https://github.com/openjdk/jdk/pull/2324)  Conditional expression mistakenly treated as standalone
- [JDK-8264696](https://bugs.openjdk.java.net/browse/JDK-8264696) [PATCH](https://github.com/openjdk/jdk/pull/3374)  Multi-catch clause causes compiler exception because it uses the package-private supertype
- [JDK-8263642](https://bugs.openjdk.java.net/browse/JDK-8263642) [PATCH](https://github.com/openjdk/jdk/pull/3399)  javac emits duplicate checkcast for first bound of intersection type in cast
- [JDK-8265899](https://bugs.openjdk.java.net/browse/JDK-8265899) [PATCH](https://github.com/openjdk/jdk/pull/3673)  Use pattern matching for instanceof at module jdk.compiler(part 1)
- [JDK-8265900](https://bugs.openjdk.java.net/browse/JDK-8265900) [PATCH](https://github.com/openjdk/jdk/pull/3674)  Use pattern matching for instanceof at module jdk.compiler(part 2)
- [JDK-8265901](https://bugs.openjdk.java.net/browse/JDK-8265901) [PATCH](https://github.com/openjdk/jdk/pull/3675)  Use pattern matching for instanceof at module jdk.compiler(part 3)
- [JDK-8266625](https://bugs.openjdk.java.net/browse/JDK-8266625) [PATCH](https://github.com/openjdk/jdk/pull/3899)  The method DiagnosticSource#findLine returns wrong results when using the boundary values
- [JDK-8266675](https://bugs.openjdk.java.net/browse/JDK-8266675) [PATCH](https://github.com/openjdk/jdk/pull/3912)  Optimize IntHashTable for encapsulation and ease of use
- [JDK-8266796](https://bugs.openjdk.java.net/browse/JDK-8266796) [PATCH](https://github.com/openjdk/jdk/pull/3942)  Clean up the unnecessary code in the method UnsharedNameTabl#fromUtf
- [JDK-8266819](https://bugs.openjdk.java.net/browse/JDK-8266819) [PATCH](https://github.com/openjdk/jdk/pull/3961)  Separate the stop policies from the compile policies completely
- [JDK-8267355](https://bugs.openjdk.java.net/browse/JDK-8267355) [PATCH](https://github.com/openjdk/jdk/pull/4106)  Adjust the parameters of the method UnicodeReader#digit
- [JDK-8267361](https://bugs.openjdk.java.net/browse/JDK-8267361) [PATCH](https://github.com/openjdk/jdk/pull/4111)  JavaTokenizer reads octal numbers mistakenly
- [JDK-8267570](https://bugs.openjdk.java.net/browse/JDK-8267570) [PATCH](https://github.com/openjdk/jdk/pull/4153)  The comment of the class JavacParser is not appropriate
- [JDK-8267578](https://bugs.openjdk.java.net/browse/JDK-8267578) [PATCH](https://github.com/openjdk/jdk/pull/4157)  Remove unnecessary preview checks
- [JDK-8267580](https://bugs.openjdk.java.net/browse/JDK-8267580) [PATCH](https://github.com/openjdk/jdk/pull/4158)  The method JavacParser#peekToken is wrong when the first parameter is not zero
- [JDK-8266239](https://bugs.openjdk.java.net/browse/JDK-8266239) [PATCH](https://github.com/openjdk/jdk/pull/4244)  Some duplicated javac command-line options have repeated effect
- [JDK-8263926](https://bugs.openjdk.java.net/browse/JDK-8263926) [PATCH](https://github.com/openjdk/jdk/pull/4523)  JavacFileManager.hasExplicitLocation fails with NPE while compiling
- [JDK-8268670](https://bugs.openjdk.java.net/browse/JDK-8268670) [PATCH](https://github.com/openjdk/jdk17/pull/46)  yield statements doesn't allow ~ or ! unary operators in expression
- [JDK-8267610](https://bugs.openjdk.java.net/browse/JDK-8267610) [PATCH](https://github.com/openjdk/jdk17/pull/59)  NPE at at jdk.compiler/com.sun.tools.javac.jvm.Code.emitop
- [JDK-8269738](https://bugs.openjdk.java.net/browse/JDK-8269738) [PATCH](https://github.com/openjdk/jdk/pull/4678)  AssertionError when combining pattern maching and function closure
- [JDK-8269113](https://bugs.openjdk.java.net/browse/JDK-8269113) [PATCH](https://github.com/openjdk/jdk/pull/4679)  Javac throws when compiling switch (null)
- [JDK-8268894](https://bugs.openjdk.java.net/browse/JDK-8268894) [PATCH](https://github.com/openjdk/jdk/pull/4749)  forged ASTs can provoke an AIOOBE at com.sun.tools.javac.jvm.ClassWriter::writePosition
- [JDK-8271254](https://bugs.openjdk.java.net/browse/JDK-8271254) [PATCH](https://github.com/openjdk/jdk/pull/5495)  javac generates unreachable code when using empty semicolon statement
- [JDK-8273408](https://bugs.openjdk.java.net/browse/JDK-8273408) [PATCH](https://github.com/openjdk/jdk/pull/5511)  java.lang.AssertionError: typeSig ERROR on generated class property of record


#### hotspot
- [JDK-8227106](https://bugs.openjdk.java.net/browse/JDK-8227106) [PATCH](https://github.com/openjdk/jdk/pull/1217)  InitiatingHeapOccupancyPercent is G1-specific but defined in shared
- [JDK-8250888](https://bugs.openjdk.java.net/browse/JDK-8250888) [PATCH](https://github.com/openjdk/jdk/pull/1319)  nsk/jvmti/scenarios/general_functions/GF08/gf08t001/TestDriver.java fails
- [JDK-8268368](https://bugs.openjdk.java.net/browse/JDK-8268368) [PATCH](https://github.com/openjdk/jdk/pull/4546)  Adopt cast notation for JavaThread conversions

