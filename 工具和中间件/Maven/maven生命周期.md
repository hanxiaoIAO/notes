每个生命周期的各个阶段。

#### 1. clean 生命周期

clean 生命周期的目的是清理项目，它包括以下三个阶段。

- pre-clean：执行清理前需要完成的工作。
- clean：清理上一次构建过程中生成的文件，比如编译后的 class 文件等。
- post-clean：执行清理后需要完成的工作。

#### 2. default 生命周期

default 生命周期定义了构建项目时所需要的执行步骤，它是所有生命周期中最核心部分，包含的阶段如下表所述，比较常用的阶段用粗体标记。

| 名称                        | 说明                                                         |
| --------------------------- | ------------------------------------------------------------ |
| validate                    | 验证项目结构是否正常，必要的配置文件是否存在                 |
| initialize                  | 做构建前的初始化操作，比如初始化参数、创建必要的目录等       |
| generate-sources            | 产生在编译过程中需要的源代码                                 |
| process-sources             | 处理源代码，比如过滤值                                       |
| **generate-resources**      | 产生主代码中的资源在 classpath 中的包                        |
| **process-resources**       | 将资源文件复制到 classpath 的对应包中                        |
| **compile**                 | 编译项目中的源代码                                           |
| process-classes             | 产生编译过程中生成的文件                                     |
| generate-test-sources       | 产生编译过程中测试相关的代码                                 |
| process-test-sources        | 处理测试代码                                                 |
| **generate-test-resources** | 产生测试中资源在 classpath 中的包                            |
| **process-test-resources**  | 将测试资源复制到 classpath 中                                |
| **test-compile**            | 编译测试代码                                                 |
| process-test-classes        | 产生编译测试代码过程的文件                                   |
| **test**                    | 运行测试案例                                                 |
| prepare-package             | 处理打包前需要初始化的准备工作                               |
| package                     | 将编译后的 class 和资源打包成压缩文件，比如 rar              |
| pre-integration-test        | 做好集成测试前的准备工作，比如集成环境的参数设置             |
| integration-test            | 集成测试                                                     |
| post-integration-test       | 完成集成测试后的收尾工作，比如清理集成环境的值               |
| verify                      | 检测测试后的包是否完好                                       |
| **install**                 | 将打包的组件以构件的形式，安装到本地依赖仓库中，以便共享给本地的其他项目 |
| **deploy**                  | 运行集成和发布环境，将测试后的最终包以构件的方式发布到远程仓库中，方便所有程序员共享 |

这些阶段的详细介绍内容可以参考链接：
http://maven.apache.org/guides/introduction/introduction-to-the-lifecycle.html

#### 3. site 生命周期

site 生命周期的目的是建立和发布项目站点。Maven 可以基于 pom 所描述的信息自动生成项目的站点，同时还可以根据需要生成相关的报告文档集成在站点中，方便团队交流和发布项目信息。site 生命周期包括如下阶段。

- pre-site：执行生成站点前的准备工作。
- site：生成站点文档。
- post-site：执行生成站点后需要收尾的工作。
- site-deploy：将生成的站点发布到服务器上。