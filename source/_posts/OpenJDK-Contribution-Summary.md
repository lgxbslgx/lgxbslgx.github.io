---
title: OpenJDK Contribution Summary
date: 2020-11-20 14:39:15
tags:
  - OpenJDK
  - Java
---

### OpenJDK Contribution Summary

#### hotspot
- [JDK-8227106](https://bugs.openjdk.java.net/browse/JDK-8227106) [PATCH](https://github.com/openjdk/jdk/pull/1217)  InitiatingHeapOccupancyPercent is G1-specific but defined in shared
- [JDK-8250888](https://bugs.openjdk.java.net/browse/JDK-8250888) [PATCH](https://github.com/openjdk/jdk/pull/1319)  nsk/jvmti/scenarios/general_functions/GF08/gf08t001/TestDriver.java fails

#### tool: javac
- [JDK-8254023](https://bugs.openjdk.java.net/browse/JDK-8254023) [PATCH](https://github.com/openjdk/jdk/pull/622)  A module declaration is not allowed to be a target of an annotation that lacks an @Target meta-annotation
- [JDK-8254557](https://bugs.openjdk.java.net/browse/JDK-8254557) [PATCH](https://github.com/openjdk/jdk/pull/718)  Compiler crashes with java.lang.AssertionError: isSubtype UNKNOWN
- [JDK-8255968](https://bugs.openjdk.java.net/browse/JDK-8255968) [PATCH](https://github.com/openjdk/jdk/pull/1389)  Confusing error message for inaccessible constructor
- [JDK-8257037](https://bugs.openjdk.java.net/browse/JDK-8257037) [PATCH](https://github.com/openjdk/jdk/pull/1490)  No javac warning when calling deprecated constructor with diamond
- [JDK-8245956](https://bugs.openjdk.java.net/browse/JDK-8245956) [PATCH](https://github.com/openjdk/jdk/pull/1553)  JavaCompiler still uses files API instead of Path API in a specific case
- [JDK-8231622](https://bugs.openjdk.java.net/browse/JDK-8231622) [PATCH](https://github.com/openjdk/jdk/pull/1626)  SuppressWarning("serial") ignored on field serialVersionUID

