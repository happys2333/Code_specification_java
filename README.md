# Java代码书写建议

本篇是基于本人平时开发经验与实习经历撰写而成的一套简易的代码开发规范，每个人都有自己的代码书写习惯，流水线化的书写代码有利有弊，所以本文旨在提供一套可供参考的代码规范，具体采纳与否，请各位读者自行决定。

# 目录

```txt
 Copyright (c) Happys 2021-2021. All rights reserved.
 @author 开心
 @email happys2333@outlook.com
```

- [Java代码书写建议](#java代码书写建议)
- [目录](#目录)
- [为什么需要代码规范](#为什么需要代码规范)
  - [代码书写原则](#代码书写原则)
- [代码书写规范](#代码书写规范)
  - [代码风格](#代码风格)
  - [类型使用](#类型使用)
  - [方法与类](#方法与类)
  - [异常日志](#异常日志)
  - [语言特性](#语言特性)
  - [代码性能](#代码性能)
- [代码安全规范](#代码安全规范)
  - [输入安全](#输入安全)
  - [数据安全](#数据安全)
  - [代码安全](#代码安全)

# 为什么需要代码规范

任何编程的最终目的都是给人看的，无论何时何地，具有良好的代码编写习惯都会让你的程序变得赏心悦目，同时这也意味着更快的开发效率以及更好的代码维护性。大部分情况下，你都会需要和别人合作完成一个项目，正确的规范你的代码将会让你更快更好的完成一个项目。

## 代码书写原则

- 清晰易懂，清晰性是易于维护、易于重构的程序必需具备的特征。
- 简洁明确，一套简洁的代码有助于后期的维护梳理。
- 风格一致，具有风格一致的代码会让你的书写阅读速度提升百倍。
- 安全稳定，代码能安全稳定运行是编写程序的第一要务。

# 代码书写规范

## 代码风格

- 使用驼峰命名规范，类首字母大写，方法和变量首字母小写

```java
//错误样例
int a;
public static void s();
Object SQLRESULT;
Class sqlfun;
//正确样例
int userId;
public static void runSelect();
Object userSqlRestul;//如果要用缩写，仅第一个字母大写其余小写
Class SqlFunction;
```

- 禁止魔鬼数字，直接使用数字英文命名变量或赋值时并不能让人明确知晓涵义等行为严禁出现在代码中

```java
//错误示例
int one=1;
int doorState = 3;
//正确示例(采用枚举或静态变量)
static final int CLOSE = 3;
int doorState = CLOSE;
enum DoorState{
  open,close
}
DoorState mainDoor = DoorState.open;
```

- 常量命名，由全大写单词组成，单词间用下划线分隔，且使用 static final修饰

```java
//错误示例
static int a = 1;
//正确示例
static final int MAX_USER_TYPE = 1;
```

- 任何情况下命名应采用英文单词，严禁中文\拼音\中英文混杂的命名
- 不应该使用否定含义的名称命名布尔类型
  ```java
  //错误
  boolean isNotNum;
  ```
- 除明确容易知晓其涵义的情况下，变量名应均有足够的信息保障阅读者可以看懂这个变量名的用途，当具有集合涵义的变量出现的时候应采用其复数形式
- 左大括号在大部分情况下应紧贴于上一个语句

```java
//正确样例
if(true){
  ...
}
while (i=0){
  ...
}
try{
  ...
}
catch(e){
  ...
}
```

- 方法命名规范应采用如下格式

```txt
动词()
动词+宾语()
get + 非布尔属性名()
is + 布尔属性名()
set + 属性名()
has + 名词/形容词()
```

- 包命名应使用多个单词组成，所有字母均为小写

```java
package org.happys.test.web
```

- 使用适量的注释，让代码自己能解释自己
  注释一定程度上是代码可读性过低导致的问题，在编写代码时，注释只是辅助理解，而不应该以注释为借口编写可读性过低的代码

```java
//错误样例
for(int i:a){//i represent the statement of the door in array a
  System.out.print(i);
}
//正确样例
for(int doorStatement:doors){
  System.out.print(doorStatement);
}
```

- 注释应该关注代码执行意图，而非具体如何实现
- 注释应无论何时都与其对应的代码保持一致，及时更新或删除注释
- 不允许在最终结果中上传大量debug期间注释的代码，应及时删除此类代码
- 单行注释用//，块注释用/* */，JavaDoc注释用/**  */
- 数组声明采用中括号前置法

```java
//错误样例
int array[] = new int[10];
//正确样例
int[] array = new int[10];
```

- 单行代码不应该超过屏幕宽度(一般推荐80字符换行)
- 在不同的概念（关键字、变量、操作符等）增加空格

```java
a++;
a += 1;
```

- 规范缩进区分不同层级代码，一个tab对应4个空格，非特殊情况下均使用tab缩进
- 局部变量应影响作用域最小，不应该让局部变量毫无意义的放置到更大的作用范围
- if、for、do、while、switch等语句的执行体加大括号{}

```java
//错误样例
  if(true)
    a++;
//正确样例
  if(true){
    a++;
  }
```

- 单个文件长度应保持在约1000行代码左右的长度，避免过短或过长
- 建议在调用其他库文件时避免使用*导入
  ```java
  import java.util.*; // 错误
  ```

## 类型使用

- 避免任何使用浮点数的精确计算计算机本身不能进行精确浮点数运算，所以在任何情况下都不可能获取准确的浮点数值，应避免对浮点数进行精确计算
- 减少或避免强制类型转换的使用，如需使用，应在转化前采用instanceof判断，更多情况下建议改善设计，使得只有一种类型
- 避免同一局部变量前后不同的含义

```java
//错误样例
public void foo() {
  Entity entity;
  if (CollectionUtils.isNotEmpty(entityList)) {
    	entity = findFirst(entityList);
      //...
      entity = findLast(entityList);
      //...
  } 
}
```

- 严禁魔鬼写法，这类写法无论何时都会让你的代码直接变成垃圾堆

```java
//避免类似写法
a = ++a;
a = a++;
a = ++-+a;
```

## 方法与类

- 方法编写应短小精悍，一个方法的长度不建议超过50行
- 方法不应该冗杂，保证方法只为这一个单一的功能实现而非过于冗杂的内容
- 不要把方法的入参当做工作变量/临时变量，除非特别需要

```java
//错误样例
int sample(int inputVal) {
    inputVal = inputVal * CurrentMuiniplier(inputVal);
    inputVal = inputVal * CurrentAdder(inputVal);
    return inputVal;
}
//正确样例，使用局部变量
int sample (int inputVal) {
    int workingVal = inputVal;
    workingVal = workingVal * CurrentMuiniplier(workingVal);
    workingVal = workingVal * CurrentAdder(workingVal);
    //...
    return workingVal;
}
```

- 谨慎使用静态方法或类，尤其应该关注可能导致的问题
- 当有库函数支持某一个方法的时候应优先使用库函数
- 方法参数应少于7个，过多参数难以维护
- 每一个类无论何时都应该写出其构造函数
- 创建类的时候，尤其是类数组时应关注是否会出现空指针问题
- 类中内容应按照需求规定其可访问的级别，不应全设置为public，非必须情况下变量更应该设计为private
- 类设计时优选组合而不是继承

```JAVA
蜡笔有三种颜色和三种型号，我们应按照颜色和型号进行分类继承，这样需要3+3=6个类
如果我们以蜡笔本身进行分类，则需要3*3=9个类
```

- 避免无关变量或毫无区分度的变量名及其重用
- 覆写时应该注释@Override
- 当类可以抽象出接口的时候，优先抽象出接口

## 异常日志

- 只有遇到真正的异常时才采用Exception,不应该滥用异常

```java
//错误样例
try {
	int i = 0;
	while(true){ //不应该试图用expection来终止循环体
		range[i++].climb();
     }
} 
catch(ArrayIndexOutOfBoundsException e) {	
	...
}
```

- 抛出异常时应该捕获到能导致异常发生的有用的信息
- 应避免空catch块来忽略异常
- 注释和文档中应该注明异常的可能性以及说明
- 当异常过多时应该对异常进行封装，尤其是使用第三方代码时
- 异常信息应该尽可能被使用，而非单纯抛出一个错误代码
- 在finally块中不要使用return、break或continue使finally块非正常结束
- 异常抛出不应该过多，过多会拖慢效率
- 日志应该使用专业的日志工具(比如：slf4j+logback)，而非使用命令行打印
- 日志应该区分等级，常见区分等级为:debug、info、warn、error、fatal
- 日志中严禁记录敏感信息

## 语言特性

- 采用括号明确区分运算优先级
- 运算应避免溢出
- 不要使用过度复杂的表达式
- 在switch语句的每一个case、和default中都放置一条break语句，避免遗漏导致异常
- 在设计类时应优先考虑运用泛型
- 优先升级到稳定最新的Java版本上，保障代码可以获取更新的收益
- 充分利用编译器/IDEA的告警提示，保障告警尽可能降到最低

## 代码性能

- 谨慎的进行性能优化
  优化的弊大于利，特别是不成熟的优化。在优化的过程中，产生的软件可能既不快速，也不正确，而且还不容易修正。不要因为性能而牺牲合理的结构。要努力编写好的程序而不是快的程序。只有在性能影响到程序功能时才考虑设计中的性能问题。

# 代码安全规范

## 输入安全

- 谨慎对待任何外部输入(不可信输入)用户可能会输入任何内容，在编写程序时应考虑因用户输入而导致的问题，如数据库注入
- 对用户输入内容采取白名单方法进行过滤
  在编写代码时采用白名单可以更加明确的安全的规避大部分安全风险

```java
//错误示范
public static boolean isCorrect(String userType){
  if(userType.contains(";")){
      return false;
  }
  return true;
}
//正确示范
public static boolean isCorrect(String userType){
  if(userType.equals("admin")||userType.equals("user")){
      return true;
  }
  return false;
}
```

- 禁止使用未经校验的输入拼接构建SQL语句

```java
//错误样例
String sqlString = "SELECT * FROM db_user WHERE username = '"
        + username + "' AND password = '" + pwd + "'";
ResultSet rs = stmt.executeQuery(sqlString);
//正确使用(预编译)
String sqlString = "select * from db_user where username=? and password=?";
PreparedStatement stmt = connection.prepareStatement(sqlString);
//正确使用(使用OWASP的ESAPI做转义)
String pwd = hashPassword(password);
Codec oe = new OracleEncodec();
String susername = ESAPI.encoder().encodeForSQL(oe,username);
String spwd = ESAPI.encoder().encodeForSQL(oe,pwd);
String sqlString = "SELECT * FROM db_user WHERE username = '"
      + susername + "' AND password = '" + spwd + "'";
```

- 禁止使用未经校验的输入拼接构建OS命令行语句并通过Runtime.exec()方法执行

```java
//错误示例：导致提权问题
String dir = System.getProperty("dir");   
Runtime rt = Runtime.getRuntime();  
Process proc = rt.exec(new String[] {"sh", "-c", "ls " + dir});
//正确示例(避免使用exec())
File dir = new File(System.getProperty("dir"));
```

- 禁止使用未经校验的输入拼接使用xml

```java
//错误示例（未检查的输入）：
String xmlString = "<user><role>operator</role><id>" + user.getUserId()
      + "</id><description>" + user.getDescription() + "</description></user>";
//正确示例（白名单过滤）
// Write XML string if userID contains alphanumeric and underscore characters only
if (!Pattern.matches("[_a-bA-B0-9]+", user.getUserId())){
    // Handle format violation
}
if (!Pattern.matches("[_a-bA-B0-9]+", user.getDescription())){
    // Handle format violation
}
String xmlString = "<user><id>" + user.getUserId()
        + "</id><role>operator</role><description>"
        + user.getDescription() + "</description></user>";
```

## 数据安全

- 对于敏感信息，严禁在任何地方输出
- 严禁使用String存储敏感信息，应该采用char[]且在使用后应立刻删除
- 对于安全敏感的应用场景，使用强随机数生成器

```java
//错误样例
Random number = new Random(123L);
int n = number.nextInt(21);
//正确样例
SecureRandom number = SecureRandom.getInstance("SHA1PRNG");
System.out.println(number.nextInt(21));
```

- 创建文件时指定合理的访问权限，严禁越权访问

## 代码安全

- 在需要的情况下使用加壳等技术阻止对代码的反编译
- 减少代码中的冒险，对于异常应尽快尽早处理
- 使用JDK8及以上的JDK去编译程序，如果是多人合作项目，请提前规定使用的JDK版本
- 在任何非必要情况下，开辟数组应该符合自己需要选择开辟

```java
//数据量1000
//错误样例
public int[] array = new int[10000];
//正确样例
public int[] array = new int[1000];
```

- 多线程技术中考虑冒险竞争问题，避免因此导致的程序问题
