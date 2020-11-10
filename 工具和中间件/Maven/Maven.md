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

## 常见Maven插件

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

## pom

POM（Project Object Model，项目对象模型）是 Maven 工程的基本工作单元，包含了项目的基本信息。POM 中可以指定一下配置：

- 项目依赖
- 插件
- 执行目标
- 项目构建的配置文件
- 项目版本
- 项目开发者列表
- 相关邮件列表信息

[pom详解](pom.xml)

## MAVEN 构建生命周期

Maven 有以下三个标准的生命周期：

- **clean**：项目清理的处理
- **default(或 build)**：项目部署的处理
- **site**：项目站点文档创建的处理

在一个生命周期中，运行某个阶段的时候，它之前的所有阶段都会被运行。

default(或 build)生命周期包括23个阶段：

| 生命周期阶段                                | 描述                                                         |
| ------------------------------------------- | ------------------------------------------------------------ |
| validate（校验）                            | 校验项目是否正确并且所有必要的信息可以完成项目的构建过程。   |
| initialize（初始化）                        | 初始化构建状态，比如设置属性值。                             |
| generate-sources（生成源代码）              | 生成包含在编译阶段中的任何源代码。                           |
| process-sources（处理源代码）               | 处理源代码，比如说，过滤任意值。                             |
| generate-resources（生成资源文件）          | 生成将会包含在项目包中的资源文件。                           |
| process-resources （处理资源文件）          | 复制和处理资源到目标目录，为打包阶段最好准备。               |
| compile（编译）                             | 编译项目的源代码。                                           |
| process-classes（处理类文件）               | 处理编译生成的文件，比如说对Java class文件做字节码改善优化。 |
| generate-test-sources（生成测试源代码）     | 生成包含在编译阶段中的任何测试源代码。                       |
| process-test-sources（处理测试源代码）      | 处理测试源代码，比如说，过滤任意值。                         |
| generate-test-resources（生成测试资源文件） | 为测试创建资源文件。                                         |
| process-test-resources（处理测试资源文件）  | 复制和处理测试资源到目标目录。                               |
| test-compile（编译测试源码）                | 编译测试源代码到测试目标目录.                                |
| process-test-classes（处理测试类文件）      | 处理测试源码编译生成的文件。                                 |
| test（测试）                                | 使用合适的单元测试框架运行测试（Juint是其中之一）。          |
| prepare-package（准备打包）                 | 在实际打包之前，执行任何的必要的操作为打包做准备。           |
| package（打包）                             | 将编译后的代码打包成可分发格式的文件，比如JAR、WAR或者EAR文件。 |
| pre-integration-test（集成测试前）          | 在执行集成测试前进行必要的动作。比如说，搭建需要的环境。     |
| integration-test（集成测试）                | 处理和部署项目到可以运行集成测试环境中。                     |
| post-integration-test（集成测试后）         | 在执行集成测试完成后进行必要的动作。比如说，清理集成测试环境。 |
| verify （验证）                             | 运行任意的检查来验证项目包有效且达到质量标准。               |
| install（安装）                             | 安装项目包到本地仓库，这样项目包可以用作其他本地项目的依赖。 |
| deploy（部署）                              | 将最终的项目包复制到远程仓库中与其他开发者和项目共享。       |