# day11_课后练习

# 代码阅读分析题

## 第1题（实例化）

知识点：实例初始化

案例：判断运行结果

```java
package com.atguigu.test01;

class HelloA{
    //构造方法
	public HelloA(){
		System.out.println("HelloA");//②
	}
    //构造代码块
	{
		System.out.println("I'm A Class");//①
	}
}

class HelloB extends HelloA{
	public HelloB(){
		System.out.println("HelloB");//④
	}
	{
		System.out.println("I'm B Class");//③
	}
}
public class Test01{
	public static void main(String[] args) {
		new HelloB();
	}
}

```

## 第2题（实例化）

知识点：实例初始化

案例：判断运行结果

```java
package com.atguigu.test02;

public class Test02 {
	public static void main(String[] args) {
		new Child("mike");
	}
}

class People {
	private String name;

	public People() {
		System.out.print("1");//①
	}

	public People(String name) {
		System.out.print("2");//③
		this.name = name;
	}
    
}

class Child extends People {
	People father;

	public Child(String name) {
        super();//隐含
		System.out.print("3");//②
		father = new People(name + " F");
	}

	public Child() {
		System.out.print("4");
	}
}

```

## 第3题（实例化）

知识点：实例初始化

案例：分析运行结果

```java
package com.atguigu.test03;

public class Test03 {
	public static void main(String[] args) {
		Father f = new Father();
		Child c = new Child();
	}
}
class Father {
	public Father(){
		System.out.println("father create");//①②
	}
}
class Child extends Father{
	public Child(){
		System.out.println("child create");//③
	}
}
```

## 第4题（继承中成员访问）

知识点：继承、属性同名问题

```java
package com.atguigu.test04;

public class Test04 extends Father{
	private String name = "test";
	
	public static void main(String[] args) {
		Test04 test = new Test04();
		System.out.println(test.getName());
	}
}
class Father {
	private String name = "father";

	public String getName() {
		return name;
	}
}
```

## 第5题（实例化）

知识点：实例初始化、构造器

案例：分析运行结果

```java
package com.atguigu.test05;

public class Test05 {

	public static void main(String[] args) {
		new A(new B());
	}
}

class A {
	public A() {
		System.out.println("A");
	}

	public A(B b) {
		this();
		System.out.println("AB");
	}
}

class B {
	public B() {
		System.out.println("B");
	}
}

```

## 第6题（实例化）

知识点：实例初始化

案例：分析运行结果

```java
package com.atguigu.test06;

public class Test06 {
	public static void main(String[] args) {
		Sub s = new Sub();
	}
}
class Base{
	Base(){
		method(100);
	}
	{
		System.out.println("base");
	}
	public void method(int i){
		System.out.println("base : " + i);
	}
}
class Sub extends Base{
	Sub(){
		super.method(70);
	}
	{
		System.out.println("sub");
	}
	public void method(int j){
		System.out.println("sub : " + j);
	}
}
```

## 第7题（实例化）

```java
public class Test07 {
	public static void main(String[] args) {
		Son son = new Son();
	}
}
class Father{
	static{
		System.out.println("（1）父类的静态代码块");
	}
	{
		System.out.println("（2）父类的非静态代码块");
	}
	Father(){
		System.out.println("（3）父类的无参构造");
	}
}
class Son extends Father{
	static{
		System.out.println("（4）子类的静态代码块");
	}
	{
		System.out.println("（5）子类的非静态代码块");
	}
	Son(){
		System.out.println("（6）子类的无参构造");
	}
}
```

## 第8题（超难）

```java
public class Test08 {
	public static void main(String[] args) {
		Zi zi = new Zi();
	}
}
class Fu{
	private static int i = getNum("（1）i");
	private int j = getNum("（2）j");
	static{
		print("（3）父类静态代码块");
	}
	{
		print("（4）父类非静态代码块，又称为构造代码块");
	}
	Fu(){
		print("（5）父类构造器");
	}
	public static void print(String str){
		System.out.println(str + "->" + i);
	}
	public static int getNum(String str){
		print(str);
		return ++i;
	}
}
class Zi extends Fu{
	private static int k = getNum("（6）k");
	private int h = getNum("（7）h");
	static{
		print("（8）子类静态代码块");
	}
	{
		print("（9）子类非静态代码块，又称为构造代码块");
	}
	Zi(){
		print("（10）子类构造器");
	}
	public static void print(String str){
		System.out.println(str + "->" + k);
	}
	public static int getNum(String str){
		print(str);
		return ++k;
	}
}

```

## 第9题（超难）

```java
public class T {
	public static int k = 0;
	public static T t1 = new T("t1");
	public static T t2 = new T("t2");
	public static int i = print("i");
	public static int n = 99;
	
	public int j = print("j");
	{
		print("构造块");
	}

	static{
		print("静态块");
	}
	public T(String str){
		System.out.println((++k) + ":" + str + "  i=" + i + "  n=" + n);
		++n;
		++i;
	}
	public static int print(String str){
		System.out.println((++k) + ":" + str + "  i=" + i + "  n=" + n);
		++n;
		return ++i;
	}
	public static void main(String[] args) {
	
	}
}
```

## 第10题（参数传递）

考核知识点：方法的参数传递、final关键字

```java
package com.atguigu.test10;

public class Test10 {
	public static void main(String[] args) {
		Other o = new Other();
		new Test10().addOne(o);
		System.out.println(o.i);
	}
	
	public void addOne(final Other o){
		o.i++;
	}
}
class Other{
	public int i;
}
```

## 第11题（初始化，变量自增自减）

考核知识点：类初始化，局部变量与类变量，自增自减

```java
package com.atguigu.test11;

public class Test11 {
	static int x, y, z;

	static {
		int x = 5;
		x--;
	}

	static {
		x--;
	}

	public static void main(String[] args) {
		System.out.println("x=" + x);
		z--;
		method();
		System.out.println("result:" + (z + y + ++z));
	}

	public static void method() {
		y = z++ + ++z;
	}
}
```

## 第12题（this）

考核知识点：继承、this

```java
package com.atguigu.test12;

public class Test12 {
	public static void main(String[] args) {
		Father f = new Father();
		Son s = new Son();
		System.out.println(f.getInfo());
		System.out.println(s.getInfo());
		s.setInfo("尚硅谷");
		System.out.println(f.getInfo());
		System.out.println(s.getInfo());
	}
}
class Father{
	private String info = "atguigu";
	public void setInfo(String info){
		this.info = info;
	}
	public String getInfo(){
		return info;
	}
}
class Son extends Father{
	
}
```

## 第13题（this,super）

考核知识点：继承、this、super

```java
package com.atguigu.test13;

public class Test13 {
	public static void main(String[] args) {
		Father f = new Father();
		Son s = new Son();
		System.out.println(f.getInfo());
		System.out.println(s.getInfo());
		s.test();
		System.out.println("-----------------");
		s.setInfo("大硅谷");
		System.out.println(f.getInfo());
		System.out.println(s.getInfo());
		s.test();
	}
}
class Father{
	private String info = "atguigu";
	public void setInfo(String info){
		this.info = info;
	}
	public String getInfo(){
		return info;
	}
}
class Son extends Father{
	private String info = "尚硅谷";
	public void test(){
		System.out.println(this.getInfo());
		System.out.println(super.getInfo());
	}
}
```

## 第14题(this,super,重写)

考核知识点：继承、this、super、重写

```java
package com.atguigu.test14;

public class Test14 {
	public static void main(String[] args) {
		Father f = new Father();
		Son s = new Son();
		System.out.println(f.getInfo());
		System.out.println(s.getInfo());
		s.test();
		System.out.println("-----------------");
		s.setInfo("大硅谷");
		System.out.println(f.getInfo());
		System.out.println(s.getInfo());
		s.test();
	}
}
class Father{
	private String info = "atguigu";
	public void setInfo(String info){
		this.info = info;
	}
	public String getInfo(){
		return info;
	}
}
class Son extends Father{
	private String info = "尚硅谷";
	public void setInfo(String info){
		this.info = info;
	}
	public String getInfo(){
		return info;
	}
	public void test(){
		System.out.println(this.getInfo());
		System.out.println(super.getInfo());
	}
}
```

## 第15题（实例化）

考核知识点：类初始化与实例初始化，比第1题仅多了静态代码块

```java
package com.atguigu.test15;

class HelloA{
	public HelloA(){
		System.out.println("HelloA");
	}
	{
		System.out.println("I'm A Class");
	}
	static{
		System.out.println("static A");
	}
}

public class HelloB extends HelloA{
	public HelloB(){
		System.out.println("HelloB");
	}
	{
		System.out.println("I'm B Class");
	}
	static{
		System.out.println("static B");
	}

	public static void main(String[] args) {
		new HelloB();
	}

}

```

# 代码编程题

## 第16题

案例：

1、在com.atguigu.test16包中声明员工类、程序员类、设计师类、架构师类，

![1558933215448](imgs/1558933215448.png)

* 员工类属性：编号、姓名、年龄、薪资

* 程序员类属性：编程语言，默认都是"java"

* 设计师类属性：奖金

* 架构师类属性：持有股票数量

  要求：属性私有化，无参有参构造，get/set，getInfo方法（考虑重写）

2、在com.atguigu.test16包中声明Test16类，并在main中创建每一个类的对象，并为属性赋值，并调用它们的getInfo()显示信息

