# Gradle使用笔记

## 1、Gradle简介

**官方介绍**：

Gradle是一个基于Apache Ant和Apache Maven概念的项目自动化构建开源工具。它使用一种基于Groovy的特定领域语言
(DSL)来声明项目设置，目前也增加了基于Kotlin语言的kotlin-based DSL，抛弃了基于XML的各种繁琐配置。

Gradle是一个基于JVM的构建工具，是一款通用灵活的构建工具，支持maven， Ivy仓库，支持传递性依赖管理，而不需要远程仓库或者是pom.xml和ivy.xml配置文件，基于Groovy，build脚本使用Groovy编写。

**简单理解：**

Gradle就是一个帮我们管理依赖、打包、部署、发布等工作的项目管理工具。用Gradle来帮我们管理项目可以使我们程序员更加专注于代码开发，将其他琐碎的事情交给Gradle即可。

尽管我们可以将这些工作交给Gradle去做，但是我们也得掌握Gradle相关的命令。这样我们才能指挥Gradle根据我们的需求来构建项目。

## 2、gradle-wrapper文件

路径：Gradle项目/gradle/wrapper

该路径下存放了“gradle-wrapper.jar”和“**gradle-wrapper.properties**”这两个文件。

在gradle-wrapper.properties文件当中存放了Gradle这个工具本身的一些配置信息，详细说明如下：

| 字段名              | 说明                                                     |
| ------------------- | -------------------------------------------------------- |
| distributionBase    | 下载的Gradle压缩包解压后存放路径；                       |
| distributionPath    | 相对于distributionBase的解压后的Gradle压缩包的存放路径； |
| zipStoreBase        | 同distributionBase，只不过是存放zip压缩包的；            |
| zipStorePath        | 同distributionPath，只不过是存放zip压缩包的；            |
| **distributionUrl** | Gradle发行版压缩包的下载地址；                           |

**gradle-wrapper.properties文件示例：**

```properties
distributionBase=GRADLE_USER_HOME
distributionPath=wrapper/dists
zipStoreBase=GRADLE_USER_HOME
zipStorePath=wrapper/dists
distributionUrl=https\://services.gradle.org/distributions/gradle-6.5-bin.zip
```

开发过程中值得注意的是’distributionUrl‘这个字段，因为它指定了Gradle的版本号。

当我们从GitHub上克隆别人的项目到本地时往往会因为本地Gradle版本号与克隆项目的版本号不符，这就会导致Gradle去下载克隆项目的对应版本的Gradle，这非常耗时且没必要。

**所以：在导入别人的Gradle项目到本地时切记修改distributionUrl字段的内容与本地Gradle版本号一致。**



## 3、setting.gradle文件

Gradle项目根目录下的setting.gradle文件用于初始化以及工程树的配置

这个文件大多数是为了配置”自工程“。Gradle项目中众多工程是通过工程树来表示的，这与AndroidStudio中的项目与Module是一一对应的。根工程相当于一个AndroidStudio项目，而更工程当中的“自工程”便相当于一个Module了。

**setting.gradle文件示例：**

```groov
include ':bilibili', ':common', ':ijkplayer'
//这表示该Gradle项目包含了“bilibili”、“common”、“ijkplayer”三个自工程，一个自工程对应AndroidStudio当中的Module。
```



## 4、build.gradle文件

- 根工程的build.gradle文件

  示例：

```groovy
// Top-level build file where you can add configuration options common to all sub-projects/modules.
buildscript {
    repositories {
        google()
        jcenter()
    }
    dependencies {
        classpath "com.android.tools.build:gradle:4.1.3"

        // NOTE: Do not place your application dependencies here; they belong
        // in the individual module build.gradle files
    }
}

allprojects {
    repositories {
        google()
        jcenter()
    }
}

task clean(type: Delete) {
    delete rootProject.buildDir
}
```

​	1、buildscript

​	buildscript中的声明是gradle脚本自身需要使用的资源。可以声明的资源包括依赖项、第三方插件、maven仓库地址等

​	2、ext

​	ext是自定义属性，现在很多人都喜欢把所有关于版本的信息都利用ext放在另一个自己新建的gradle文件中集中管理，下面我介绍一下	ext是怎么用的：

​	3、repositories

​	顾名思义就是仓库的意思啦，而jcenter()、maven()和google()就是托管第三方插件的平台

​	4、dependencies

​	当然配置了仓库还不够，我们还需要在dependencies{}里面的配置里，把需要配置的依赖用classpath配置上，因为这个dependencies	在buildscript{}里面，所以代表的是Gradle需要的插件。





- 自工程的build.gradle文件