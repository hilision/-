---
description: springboot路由出现404响应，你可能需要注意包扫描的问题
---

# SpringBoot路由访问404
在出现了这个问题时，通过网上查找方案，都会说框架会自动扫描启动类同级包（类文件）或者子级包下的类，只要有正确的注解，那都会被扫描到。所以如果在你的Application启动类上添加注解Application当前包路径的话，Idea会提示这行代码是多余的。

```text
package com.hilsion;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.context.annotation.ComponentScan;

@SpringBootApplication
//以下代码将是多余的
@ComponentScan(basePackages = {"com.hilsion"})
public class App {
    public static void main(String[] args) {
        SpringApplication.run(App.class, args);
    }
}
```
在得到Idea的提示后，我将`@ComponentScan`注解删除了。但由于我的工程在和`com.hilsion`还有同级的一个`org.idworker`包，为能正常使用，我将该注解加上：

```text
package com.hilsion;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.context.annotation.ComponentScan;

@SpringBootApplication
//此处增加了扫描另一个包路径的注解
@ComponentScan(basePackages = {"org.idworker"})
public class App {
    public static void main(String[] args) {
        SpringApplication.run(App.class, args);
    }
}
```
此时，我去访问位于`com.hilsion`包下的Controller时，响应了`404`。经过一番的折腾，选择尝试将需要的扫描的包路径都加上，而不管Idea有没有提示（实际上Idea并不会去标记改正过的注解）。至此，访问正常。

```text
package com.hilsion;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.context.annotation.ComponentScan;

@SpringBootApplication
//若有需要扫描包路径，则涉及到的所有包路径都应该添加
@ComponentScan(basePackages = {"com.hilsion","org.idworker"})
public class App {
    public static void main(String[] args) {
        SpringApplication.run(App.class, args);
    }
}
```
由于是第一次使用，对框架还不太熟悉。猜想应该是一个显性的规则，但也还未去做求证。
