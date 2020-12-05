[toc]

# Java IO 流

## 流的概念和作用

流：任何有能力产出数据的数据源对象或者有能力接受数据的接收端对象。

流的本质：数据传输，根据数据传输特性将流抽象成各种类，方便更直观的进行操作。

流的作用：为数据源和目的地建立一个输送通道

## java IO 模型

使用 Decorator (装饰者) 模式，按功能划分 Stream，可以根据需求动态装配这些Stream。

## IO 分类

| 按数据流方向分   | 1. 输入流 | 2. 输出流 |
| ---------------- | --------- | --------- |
| 按处理数据单位分 | 1. 字节流 | 2. 字符流 |
| 按功能不同分     | 1. 节点流 | 2. 处理流 |

### 节点流和处理流

节点流：可以从/向一个特定的 IO 设备(如磁盘、网络)读/写数据的流。节点流也被称为低级流。

处理流：对一个已存在的流进行连接和封装，通过封装后的流来实现数据的读/写功能。处理流也被称为高级流。

## IO 流的四大抽象基类

InputStream/Reader: 所有的输入流的基类，前者是字节输入流，后者是字符输入流。

OutputStream/Writer: 所有输出流的基类，前者是字节输出流，后者是字符输出流。

## 字符流和字节流

字符流的本质其实就是基于字节流的读取，然后根据指定的码表进行转换。

### 区别

|          | 字节流                 | 字符流                 |
| -------- | ---------------------- | ---------------------- |
| 读写单位 | 以字节(8bit) 为单位    | 以字符为单位           |
| 处理对象 | 可以处理所有类型的数据 | 只能处理字符类型的数据 |
| 缓冲     | 不使用缓冲区           | 使用缓冲区             |

## 常见 IO 流

### 文件流

FileInputStream、FileOutputStream和FileReader、FileWriter

节点流，直接和指定文件关联

### 缓存流

BufferedInputStream、BufferedOutputStream和BufferedReader、BufferedWriter

缓冲流是处理流的一种，它依赖于原始的输入输出流, 它令输入输出流具有1个缓冲区, 显著减少与外部设备的IO次数, 而且提供一些额外的方法

### 转换流

InputStreamReader 和 OutputStreamWriter

InputStreamReader 类包含了一个底层输入流，可以从中读取原始字节。它根据指定的编码方式，将这些字节转换为 Unicode 字符。

OutputStreamWriter 类从运行的程序中接受 Unicode 字符，然后使用指定的编码方式将这些字符转换为字节，再讲这些字节写入底层的输出流中。

转换流的特点：

1. 字符流和字节流之间的桥梁

2. 可对读取到的字节数据经过指定编码转换成字符

3. 可对读取到的字符数据经过指定编码转换成字节

使用场景：

1. 源或者目的对应的设备是字节流，但操作的确实文本数据，可以使用转换作为桥梁，提高对文本操作的便捷
2. 操作文本设计到具体的指定编码表

### 字节数组流

ByteArrayInputStream和ByteArrayOutputStream

内部包含一个内部的缓冲区（就是一个字节数组 ），该缓冲区含有从流中的字节。

## 对象流

ObjectInputStream 和ObjectOutpuStream

用于 java 对象的序列化。

# BIO、NIO、AIO

java IO 通常指的是 BIO ，即同步阻塞IO。NIO 指的是同步非阻塞IO，AIO 指的是非同步非阻塞IO。

IO 是面向流的，NIO 是面向缓冲区的。

NIO 包括三个主要结构：Buffer(缓冲区)、Channel(通道)、Selectors(选择器)。

NIO 似乎多用于网络编程，且通常开发者很少**直接**使用JDK的NIO类库进行开发。

# java输入/输出流体系中常用的流的分类表

| 分类       | 字节输入流               | 字节输出流                | 字符输入流          | 字符输出流          |
| ---------- | ------------------------ | ------------------------- | ------------------- | ------------------- |
| 抽象基类   | *InputStream*            | *OutputStream*            | *Reader*            | *Writer*            |
| 访问文件   | **FileInputStream**      | **FileOutputStream**      | **FileReader**      | **FileWriter**      |
| 访问数组   | **ByteArrayInputStream** | **ByteArrayOutputStream** | **CharArrayReader** | **CharArrayWriter** |
| 访问管道   | **PipedInputStream**     | **PipedOutputStream**     | **PipedReader**     | **PipedWriter**     |
| 访问字符串 |                          |                           | **StringReader**    | **StringWriter**    |
| 缓冲流     | BufferedInputStream      | BufferedOutputStream      | BufferedReader      | BufferedWriter      |
| 转换流     |                          |                           | InputStreamReader   | OutputStreamWriter  |
| 对象流     | ObjectInputStream        | ObjectOutputStream        |                     |                     |
| 打印流     |                          | PrintStream               |                     | PrintWriter         |
| 推回输入流 | PushbackInputStream      |                           | PushbackReader      |                     |
| 特殊流     | DataInputStream          | DataOutputStream          |                     |                     |

# 参考文档

[Java-IO流]:(https://blog.csdn.net/sinat_37064286/article/details/86537354)
[Java Io流的概念，分类，类图]:(https://blog.csdn.net/wangquan1992/article/details/9852381)
[java IO流详解]:(https://www.cnblogs.com/QQ846300233/p/6046388.html)
[一文带你看懂JAVA IO流，史上最全面的IO教学啦]:(https://zhuanlan.zhihu.com/p/99609337)

[BIO、NIO、AIO 区别和应用场景]:(https://blog.csdn.net/lisha006/article/details/82856906)