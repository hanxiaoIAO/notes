# 认识JavaFX

## 简单介绍

声明式、静态类型的脚本语言；它具有一等函数、声明的语法、列表推导，以及基于依赖关系的增量式求值等特征；JavaFX 脚本式语言特别适用于Java2D swing GUI组件，它允许简单地创建图形界面；在JavaFX中可以直接调用Java的算术、逻辑运算符，instance等操作符，还可以显式调用Java类库和方法；使用JavaFX可以轻松的编写跨平台的富客户端应用程序

## 例子

1.Application是JavaFX程序入口，Main类要继承Application类，并覆盖Start方法。 Start方法用于展示Stage。

2.Stage是任何 JavaFx 应用程序的 UI 最顶层容器，代表一个窗口，用于容纳一个Scene。

3.Scene 是 JavaFx 应用程序的第二级 UI 容器。它包含所有被程序包含的 UI 组件。这些组件被称为*图形结点*（graphical nodes），或者简称*结点*（Node）。

```java
package com.bokesoft.yes.dev;

import javafx.application.Application;
import javafx.geometry.Rectangle2D;
import javafx.scene.Scene;
import javafx.stage.Screen;
import javafx.stage.Stage;

@SuppressWarnings("restriction")
public class JavaFXDemo extends Application {
  
  public void start(Stage paramStage) throws Exception {
    paramStage.setTitle("Title");
    Rectangle2D rectangle2D = Screen.getPrimary().getVisualBounds();
    paramStage.setX(rectangle2D.getMinX());
    paramStage.setY(rectangle2D.getMinY());
    paramStage.setWidth(rectangle2D.getWidth());
    paramStage.setHeight(rectangle2D.getHeight());
    FXMLLoader loader = new FXMLLoader(getClass().getResource("Demo.fxml"));
	Parent root = loader.getRoot();
    Scene scene = new Scene(root, rectangle2D.getWidth(), rectangle2D.getHeight());
    paramStage.setScene(scene);
    paramStage.show();
  }
  
  
  public static void main(String[] args) {
    Application.launch(args);
  }
}
```

