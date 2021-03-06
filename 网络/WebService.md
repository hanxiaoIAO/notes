## 参考

[Web Service 百度百科]:(https://baike.baidu.com/item/Web%20Service/1215039?fromtitle=webservice&fromid=2342584&fr=aladdin)
[WebService介绍及使用(Java)]:(https://blog.csdn.net/qq_34845394/article/details/86478208)
[Java - 概念解释：SOAP、WSDL、UDDI]:(https://blog.csdn.net/troubleshooter/article/details/78454954)
[java根据WSDL文档，如何调用WebService？]:(https://blog.csdn.net/myblogzz/article/details/80311038)

## Web Service

WebService 也叫XML Web Service，WebService是一种可以接收从Internet或者Intranet上的其它系统中传递过来的请求，轻量级的独立的通讯技术。是通过SOAP在Web上提供的软件服务，使用WSDL文件进行说明，并通过UDDI进行注册。WebService 是一种**跨编程语言和跨操作系统平台的远程调用技术**。

SOAP、WSDL、UDDI（UniversalDescriptionDiscovery andIntegration）三者构成了WebService的三要素。

![img](C:\mydata\notes\notes\网络\resources\Web服务工作流程.png)

### SOAP

简单对象访问协议（Simple Object Access Protocol），是Web Service中交换数据的一种协议规范。

SOAP协议组成：

```
SOAP协议 = HTTP协议 + XML数据格式
```

SOAP提供了标准的RPC(Remote Procedure Call)方法来调用WebService。

### WSDL

Web服务描述语言（Web Service Description Language），它描述了Web服务的公共接口。这是一个基于XML的关于如何与Web服务通讯和使用的服务描述；也就是描述与目录中列出的Web服务进行交互时需要绑定的协议和信息格式。通常采用抽象语言描述该服务支持的操作和信息，使用的时候再将实际的网络协议和信息格式绑定给该服务。 

### UDDI

统一描述、发现和集成（Universal Description, Discovery and Integration），它是一个基于XML的跨平台的描述规范，可以使世界范围内的企业在互联网上发布自己所提供的服务。简单的说，UDDI是访问各种WSDL的一个门面（可以参考设计模式中的门面模式）。

## java 应用

### 创建Web Service服务

```java
package com.proinnova.webservice;

import javax.jws.WebMethod;
import javax.jws.WebService;

@WebService
public interface WeatherService {

	@WebMethod
    String getWeatherByCityname(HeadEntity head);
	
}
```

```java
package com.proinnova.webservice;

import java.util.List;

import javax.jws.WebService;

@WebService
public class WeatherServiceImpl implements WeatherService{

	@Override
	public String getWeatherByCityname(HeadEntity head) {
		List<DtlEntity> dtlList = head.getDtls();
		StringBuilder sb = new StringBuilder();
		sb.append(head.getCode()+":");
		for(DtlEntity dtl:dtlList) {
			sb.append("\t"+dtl.getCode() + "天气晴朗！");
		}
		return sb.toString();
	}

}
```

```java
package com.proinnova.webservice;

import javax.xml.ws.Endpoint;

public class Main {
    public static void main(String[] args) {
        //发布天气服务，这里只是简单的测试
        Endpoint.publish("http://localhost:8085/ws_server/weather", new WeatherServiceImpl());
        System.out.println("发布天气服务成功...");
    }
}
```

### 查看接口文档

访问：`http://localhost:8085/ws_server/weather?wsdl`

接口文档中比较重要的信息：

```xml
targetNamespace="http://webservice.proinnova.com/"

类型：可以确定接口方法以及参数，后面带Response的是对应方法的回复。
<types>
	<xsd:schema>
		<xsd:import namespace="http://webservice.proinnova.com/" schemaLocation="http://localhost:8085/ws_server/weather?xsd=1"/>
	</xsd:schema>
</types>

<xs:schema version="1.0" targetNamespace="http://webservice.proinnova.com/">
	<xs:element name="getWeatherByCityname" type="tns:getWeatherByCityname"/>
	<xs:element name="getWeatherByCitynameResponse" type="tns:getWeatherByCitynameResponse"/>
	<xs:complexType name="getWeatherByCityname">
		<xs:sequence>
			<xs:element name="arg0" type="tns:headEntity" minOccurs="0"/>
		</xs:sequence>
	</xs:complexType>
	<xs:complexType name="headEntity">
		<xs:sequence>
			<xs:element name="code" type="xs:string" minOccurs="0"/>
			<xs:element name="dtls" type="tns:dtlEntity" nillable="true" minOccurs="0" maxOccurs="unbounded"/>
			<xs:element name="id" type="xs:int"/>
		</xs:sequence>
	</xs:complexType>
.
.
.
</xs:schema>
```

### Web Service 调用方式

#### wsdl



