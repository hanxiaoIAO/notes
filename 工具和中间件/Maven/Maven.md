[toc]

## 参考资料

[1]:http://c.biancheng.net/view/4715.html

## Maven 介绍

Maven 的本质是一个**项目管理工具**，将项目开发和管理过程抽象成一个**项目对象模型（POM）**。

Maven 最大化地消除了构建的重复，抽象了**构建生命周期**，并且为绝大部分的构建任务提供了已实现的插件。Maven 作为一个开放的架构，提供了公共接口，方便同第三方插件集成。程序员可以将自己需要的插件，动态地集成到 Maven，从而扩展新的管理功能。

Maven 可以统一**管理所有的依赖 jar**，甚至是不同的版本。

Maven 还能帮助我们管理原本分散在项目中各个角落的**项目信息**，包括项目描述、开发者列表、版本控制系统地址、许可证、缺陷管理系统地址等。

除了直接的项目信息，通过 Maven **自动生成的站点**，以及一些已有的插件，我们还能够轻松获得项目文档、测试报告、静态分析报告、源码版本日志报告等非常具有价值的项目信息。

Maven 对于项目目录结构、测试用例命名方式等内容都有既定的规则，只要遵循了这些成熟的规则，用户在项目间切换的时候就免去了额外的学习成本，可以说是**约定优于配置（Convention Over Configuration）**。

## Maven 安装配置

将 Maven 里面的 bin 目录添加到 Path 环境变量

## Maven 目录结构

1. bin

   > mvn 运行的脚本，这些脚本用来配置 Java 命令，准备好 classpath 和相关的 Java 系统属性，然后执行 Java 命令。
   >
   > mvnDebug脚本。mvnDebug 多了一条 MAVEN_DEBUG_OPTS 配置，其作用就是在运行 Maven 时开启 debug，以便调试 Maven 本身。
   >
   >  m2.conf 文件，这是 classworlds 的配置文件。

2. boot

   >一个类加载器框架，相对于默认的 java 类加载器，它提供了更丰富的语法以方便配置，Maven 使用该框架加载自己的类库。

3. conf

   > settings.xml。直接修改该文件，就能在机器上全局地定制 Maven 的行为。
   >
   > 一般情况下，我们更偏向于复制该文件至 ～/.m2/ 目录下（～表示用户目录），然后修改该文件，在用户范围定制 Maven 的行为。

4. lib

   > 包含了所有 Maven 运行时需要的 Java 类库，Maven 本身是分模块开发的。
   >
   > 还包含一些 Maven 用到的第三方依赖，如 common-cli-1.2.jar、commons-lang-2.6.jar 等。
   >
   >  Maven 内置的超级 POM。

5. LICENSE.txt

   > 记录了 Maven 使用的软件许可证Apache License Version 2.0。

6. NOTICE.txt

   > 记录了 Maven 包含的第三方软件。

7. README.txt

   > 包含了 Maven 的简要介绍，包括安装需求及如何安装的简要指令等。

## Maven 生成站点和报告文档（cmd）

[1]:(http://c.biancheng.net/view/4800.html)

## Maven插件

在 Maven Repository（仓库）中找插件的坐标。用浏览器打开 http://mvnrepository.com/，在 Search 输入框中输入插件名称。

| 插件名称                     | 用途              | 来源   |
| ---------------------------- | ----------------- | ------ |
| maven-clean-plugin           | 清理项目          | Apache |
| maven-compile-plugin         | 编译项目          | Apache |
| maven-deploy-pligin          | 发布项目          | Apache |
| maven-site-plugin            | 生成站点          | Apache |
| maven-surefire-plugin        | 运行测试          | Apache |
| maven-jar-plugin             | 构建 jar 项目     | Apache |
| maven-javadoc-plugin         | 生成 javadoc 文件 | Apache |
| maven-surefire-report-plugin | 生成测试报告      | Apache |

### 绑定第三方插件

```xml
<!--子项目可以引用的默认插件信息。该插件配置项直到被引用时才会被解析或绑定到生命周期。给定插件的任何本地配置都会覆盖这里的配置 -->
<pluginManagement>
    <!--使用的插件列表 。 -->
    <plugins>
    </plugins>
</pluginManagement>
<!--使用的插件列表 -->
<plugins>
</plugins>
```

### 使用命令行执行 Maven 插件的语法

```cmd
maven <插件名称|前缀>:<目标> [-D参数名=参数值 ...]
```

### 使用 maven-help-plugin 查看插件

```cmd
Mvn help:describe -Dplugin=org.apache.maven.plugins:maven-site-plugin:3.4 -Ddetail
```

-Dgoal＝目标的方式查看指定目标的信息

```cmd
Mvn help:describe -Dplugin=site -Dgoal=site -Ddetail
```

### 列出当前项目的依赖树

```cmd
Mvn dependency:tree
```

### 配置第三方插件仓库

```xml
    <pluginRepositories>
        <pluginRepository>
			...
        </pluginRepository>
    </pluginRepositories>
```

### 插件默认 groupId 和 版本

 Maven 官方插件的groupId都是 org.apache.maven.plugins。使用官方插件时可以不指定 groupId 。

如果插件不属于核心插件范畴，Maven 会去检测所有仓库中的版本，最终会选择最新版本，而且这个最新版本不排除是快照版本。

## 私服创建

常用搭建 Maven 服务器的工具：

Apache 基金会的 Archiva [下载](http://archiva.apache.org/download.cgi)

JFrog 的 Artifactory [下载](https://www.jfrogchina.com/open-source/)

Sonatype 的 Nexus

## 版本管理

版本管理只对项目整体版本的演变过程进行管理。例如从 1.0 到 1.1，再到 2.0等。

### 专业术语

1. 快照版本

   项目开发过程中的临时性版本，该版本定位的构件文件会随开发的进展不断更新。

2. 发布版本

   向外部发布的一个比较稳定的版本。这个版本构件所对应的构件文件是固定的。就算后期开发新的功能，完成后也不会改变当前发布版本的内容。

3. 版本管理关系

   在项目开发过程中，团队内部会随着项目的进展发布最新的快照版本。但是开发到一定的阶段，需要将快照版本定位成一个发布版本对团队外部进行发布，同时，在这个定位版本的基础上进行二次开发，开发过程中又形成新的快照，到一定阶段后，再发布一个定位的发布版本，以此重复进行，直到最后项目完成。

    这个过程中**快照版本和发布版本的切换管理**就是版本管理。

### 理想发布版本的条件

1. 所有的测试案例应该全部通过。
2. 项目中没有配置任何快照版本的依赖。
3. 项目中没有配置任何快照版本的插件。
4. 项目中所有文档（代码）都要提交到版本控制系统（SVN/Git）。

### 版本号的约定

Maven 将版本号约定为四个部分，即主版本、次版本、增量版本和里程碑版本，按如下格式共同形成一个版本号。当然，版本号不是都必须由这四个部分组成。

```
<主版本>.<次版本>.<增量版本>-<里程碑版本>
```

- 主版本：表示项目重大架构的变更。比如 Structs1 和 Struts2 ，调整了架构体系；JUnit3 和JUnit4 ,一个全面支持注解，另一个不支持。
- 次版本：表示有较大的功能增加和变化，或者全面系统地修复漏洞。
- 增量版本：表示有重大漏洞的修复。
- 里程碑版本：表明一个版本的里程碑（版本内部）。这样的版本项目相比下一个正式版本，相对来说不是很稳定，有待更多测试。

### 主干、分支、标签

1. 主干：项目开发的主体，也是主线、关键历程。从这里可以获取项目的最新代码和绝大部分的变更历史。
2. 分支：从主线某个点分离出去的一段分支。在一个特别的时间点，既要保持项目的总体（主线）进度，又要同步修改某些重要漏洞、或者实现特殊功能、或实验性开发，就可以创建分支。分支达到预期效果后，再讲分支里的变更合并到主线中。
3. 标签：用来标记分支和主干进展到某个状态的点，代表项目进展到某个阶段或者某个相对比较稳定的状态。实际项目中，一般是版本发布的状态。

## GPG（GnuPG）

[安装使用](http://c.biancheng.net/view/4832.html)

## pom

POM（Project Object Model，项目对象模型）是 Maven 工程的基本工作单元，包含了项目的基本信息。

[pom详解](pom详解.md)

## MAVEN 生命周期

Maven 抽象了一个通用的构建生命周期，并统一规范。具体步骤包括清理、初始化、编译、测试、打包、集成测试、验证、部署、生成站点。需要注意的是，Maven 中项目的构建生命周期只是一个标准规范，并不做具体的事情。具体的事情通过集成到 Maven 的插件完成。Maven 在生命周期的每个阶段都设计了插件接口。用户可以在接口上根据实际需求绑定第三方的插件。当然，Maven 对大多数构建阶段绑定了默认的插件。Maven 在项目的构建过程中，只是在方向步骤上起到管理协调的作用。

Maven 拥有三套独立的生命周期，它们分别是 clean、default 和 site。clean 生命周期的目的是清理项目；default 生命周期的目的是构建项目；site 生命周期的目的是建立项目站点。 每个生命周期又包含了多个阶段。这些阶段在执行的时候是有固定顺序的。后面的阶段一定要等前面的阶段执行完成后才能被执行。

[每个生命周期的各个阶段](maven生命周期.md)

