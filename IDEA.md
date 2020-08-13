tag: # 内存

IDEA的内存设置与eclipse不同。eclipse的内存只需要在eclipse.ini中做配置即可，而IDAE的内存设置做了很多区分，不同的情况使用不同的内存配置。比如，idea编译Java项目使用的虚拟机和idea软件自身使用的虚拟机是分开的（也就是独立的进程）。

tag:# idea软件配置文件 # 内存

文件路径：C:\Users\bokeerp\AppData\Roaming\JetBrains\IntelliJIdea2020.1\idea64.exe.vmoptions

可以从IDEA的以下入口打开当前使用的配置文件： IDEA help->Edit Customer VM options.

tag:# 内存 # 编译

File->Settings（ctrl+alt+S）:  Build,Execution,Deployment -> Compiler  : Build process heap size(Mbytes)