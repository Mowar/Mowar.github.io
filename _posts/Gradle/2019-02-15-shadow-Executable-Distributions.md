---
title: Shadow-Executable Distributions
categories: Gradle
tags: 基础知识
updated: 2019-02-15
---

Shadow is a Gradle plugin for combining dependency classes and resources with a project's into a single output Jar. The combined Jar is often referred to a fat-jar or uber-jar.

## 命令 ##

        gradle shadowJar

## example ##

```
plugins {
    id 'com.github.johnrengelman.shadow' version '2.0.3'
    id 'java'
}

group 'org.hyperledger.fabric-chaincode-java'
version '1.0-SNAPSHOT'

sourceCompatibility = 1.8

repositories {
    mavenLocal()
    mavenCentral()
}

dependencies {
    compile group: 'org.hyperledger.fabric-chaincode-java', name: 'fabric-chaincode-shim', version: '1.+'
}

shadowJar {
    baseName = 'chaincode'
    version = '1.0.0'
    classifier = 'st'

    manifest {
        attributes 'Main-Class': 'org.hyperledger.fabric.example.SimpleChaincode'
    }
}

```

输出到build/libs/目录下,并生成chaincode-1.0.0-st.jar,其中以org.hyperledger.fabric.example.SimpleChaincode为主类

