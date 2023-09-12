# JAVA 8 新特征

- Lambda表达式 允许把函数作为一个方法的参数

1. Lambda 表达式，也可称为闭包，它是推动 Java 8 发布的最重要新特性。
2. Lambda 允许把函数作为一个方法的参数（函数作为参数传递进方法中）。
3. 使用 Lambda 表达式可以使代码变的更加简洁紧凑。

```java
//Lambda 表达式实例
// 1. 不需要参数,返回值为 5  
() -> 5  
  
// 2. 接收一个参数(数字类型),返回其2倍的值  
x -> 2 * x  
  
// 3. 接受2个参数(数字),并返回他们的差值  
(x, y) -> x – y  
  
// 4. 接收2个int型整数,返回他们的和  
(int x, int y) -> x + y  
  
// 5. 接受一个 string 对象,并在控制台打印,不返回任何值(看起来像是返回void)  
(String s) -> System.out.print(s)
```

```java
public class Java8Tester {
   public static void main(String args[]){
      Java8Tester tester = new Java8Tester();
        
      // 类型声明
      MathOperation addition = (int a, int b) -> a + b;
        
      // 不用类型声明
      MathOperation subtraction = (a, b) -> a - b;
        
      // 大括号中的返回语句
      MathOperation multiplication = (int a, int b) -> { return a * b; };
        
      // 没有大括号及返回语句
      MathOperation division = (int a, int b) -> a / b;
        
      System.out.println("10 + 5 = " + tester.operate(10, 5, addition));
      System.out.println("10 - 5 = " + tester.operate(10, 5, subtraction));
      System.out.println("10 x 5 = " + tester.operate(10, 5, multiplication));
      System.out.println("10 / 5 = " + tester.operate(10, 5, division));
        
      // 不用括号
      GreetingService greetService1 = message ->
      System.out.println("Hello " + message);
        
      // 用括号
      GreetingService greetService2 = (message) ->
      System.out.println("Hello " + message);
        
      greetService1.sayMessage("Runoob");
      greetService2.sayMessage("Google");
   }
    
   interface MathOperation {
      int operation(int a, int b);
   }
    
   interface GreetingService {
      void sayMessage(String message);
   }
    
   private int operate(int a, int b, MathOperation mathOperation){
      return mathOperation.operation(a, b);
   }
}
10 + 5 = 15
10 - 5 = 5
10 x 5 = 50
10 / 5 = 2
Hello Runoob
Hello Google
```

- 新的Stream API    **java.util.stream** 函数式编程风格引入
- 接口拥有默认方法  **支持default和static方法**   不再是传统的 ~~接口中方法都为抽象方法。~~
- Optional类 成为JAVA8自带库一部分 用来解决空指针异常
- Date Time API 加强对日期时间处理

# Java基础概念

一个 Java 程序可以认为是一系列对象的集合，而这些对象通过调用彼此的方法来协同工作。下面简要介绍下**类**、**对象**、**方法**和**实例变量**的概念。

## 基本概念

**对象**：**对象是类的一个实例**，有状态和行为。例如，一条狗是一个对象，它的状态有：颜色、名字、品种；行为有：摇尾巴、叫、吃等。

**类**：类是一个**模板**，它描述一类对象的行为（方法）和状态（属性）。

**方法**：**方法就是行为**，一个类可以有很多方法。逻辑运算、数据修改以及所有动作都是在方法中完成的。

**实例变量**：**每个对象都有独特的实例变量**，对象的状态由这些实例变量的值决定。

## 基本语法规范

1. 大小写敏感规范：Java 区分大小写是**大小写敏感**的，这就意味着标识符 Hello 与 hello 是不同的。
2. 类名规范：对于所有类来说，类名由多个单词组成那么**每个单词首字母应该大写**。例如 **MyFirstJavaClass** 。
3. 方法名规范：对于方法类来说，方法名由多个单词组成那么**首个单词首字母应该小写**，**后续单词则大写开头**。
4. 源文件名规范：**源文件名必须和类名相同**。当保存文件的时候，文件名的后缀为 **.java**。
5. 主方法入口规范：所有的 Java 程序由 <psvm>**public static void main(String[] args)** 方法开始执行。

## Java 标识符规范

- 所有的标识符都应该以字母（A-Z 或者 a-z）,美元符（$）、或者下划线（_）开始
- 首字符之后可以是字母（A-Z 或者 a-z）,美元符（$）、下划线（_）或数字的任何字符组合
- 关键字不能用作标识符
- 标识符是大小写敏感的
- 合法标识符举例：age、$salary、_value、__1_value
- 非法标识符举例：123abc、-salary

## Java修饰符规范

- 访问控制修饰符 : default, public , protected, private。
- 非访问控制修饰符 : final, abstract, static, synchronized。

## Java 枚举规范

枚举限制变量只能是预先设定好的值。使用枚举可以减少代码中的 bug。

例如：我们为果汁店设计一个程序，它将限制果汁为小杯、中杯、大杯。这就意味着它不允许顾客点除了这三种尺寸外的果汁。

```java
class FreshSize {
   enum HotSize{ XXL, XL , L }//三种尺寸的枚举描述类
   HotSize size;//枚举对象
}
public class FreshSizeTest {
   public static void main(String[] args){
      FreshSize fs = new FreshSize();//创建对象
      fs.size = FreshSize.HotSize.L;//赋值给实例
   }
}//枚举可以单独声明或者声明在类里面。方法、变量、构造函数也可以在枚举中定义。
```

## Java 变量规范

### 局部变量

（方法中） 类的方法中的变量。

> 局部变量声明在方法、构造方法或者语句块中；
>
> 局部变量是在栈上分配的。
>
> 访问修饰符不能用于局部变量；
>
> 局部变量在方法、构造方法、或者语句块被执行的时候创建，当它们执行完成后，变量将会被销毁；
>
> 局部变量没有默认值，所以局部变量被声明后，必须经过初始化，才可以使用。
>
> ```java
> public class Test{ 
>    public void pupAge(){
>       int age = 0;
>       age = age + 7;
>       System.out.println("小狗的年龄是: " + age);
>    }
>    
>    public static void main(String[] args){
>       Test test = new Test();
>       test.pupAge();
>    }
> }
> //小狗的年龄是: 7
> ```

### 成员变量

（非静态变量）独立于方法之外的变量，不过没有 static 修饰。

> 当一个对象被实例化之后，每个实例变量的值就跟着确定；
>
> 访问修饰符可以修饰实例变量；
>
> 实例变量在对象创建的时候创建，在对象被销毁的时候销毁；
>
> 实例变量的值应该至少被一个方法、构造方法或者语句块引用，使得外部能够通过这些方式获取实例变量信息；
>
> 实例变量可以声明在使用前或者使用后；
>
> 实例变量具有默认值。数值型变量的默认值是0，布尔型变量的默认值是false，引用类型变量的默认值是null。变量的值可以在声明时指定，也可以在构造方法中指定；
>
> 实例变量对于类中的方法、构造方法或者语句块是可见的。一般情况下应该把实例变量设为私有。通过使用访问修饰符可以使实例变量对子类可见；
>
> 实例变量可以直接通过变量名访问。但在静态方法以及其他类中，就应该使用完全限定名：ObjectReference.VariableName。
>
> ```java
> import java.io.*;
> public class Employee{
>    // 这个实例变量对子类可见
>    public String name;
>    // 私有变量，仅在该类可见
>    private double salary;
>    //在构造器中对name赋值
>    public Employee (String empName){
>       name = empName;
>    }
>    //设定salary的值
>    public void setSalary(double empSal){
>       salary = empSal;
>    }  
>    // 打印信息
>    public void printEmp(){
>       System.out.println("名字 : " + name );
>       System.out.println("薪水 : " + salary);
>    }
> 
>    public static void main(String[] args){
>       Employee empOne = new Employee("RUNOOB");
>       empOne.setSalary(1000.0);
>       empOne.printEmp();
>    }
> }
> //$ javac Employee.java 
> //$ java Employee
> //名字 : RUNOOB
> //薪水 : 1000.0
> ```

### 类变量（静态变量）

> 类变量也称为静态变量，在类中以 static 关键字声明，但必须在方法之外。
>
> **无论一个类创建了多少个对象，类只拥有类变量的一份拷贝。**
>
> 静态变量除了被声明为常量外很少使用，静态变量是指声明为 public/private，final 和 static 类型的变量。静态变量初始化后不可改变。
>
> **静态变量储存在静态存储区。经常被声明为常量，很少单独使用 static 声明变量。**
>
> **静态变量在第一次被访问时创建，在程序结束时销毁。**
>
> 与实例变量具有相似的可见性。但为了对类的使用者可见，大多数静态变量声明为 public 类型。
>
> 默认值和实例变量相似。**数值型变量默认值是 0，布尔型默认值是 false，引用类型默认值是 null。**变量的值可以在声明的时候指定也可以在构造方法中指定。此外，静态变量还可以在静态语句块中初始化。
>
> 静态变量可以通过：*ClassName.VariableName*的方式访问。
>
> 类变量被声明为 public static final 类型时，类变量名称一般建议使用大写字母。如果静态变量不是 public 和 final 类型，其命名方式与实例变量以及局部变量的命名方式一致。
>
> ```java
> public class Employee {
>     //salary是静态的私有变量
>     private static double salary;
>     // DEPARTMENT是一个常量
>     public static final String DEPARTMENT = "开发人员";
>     public static void main(String[] args){
>     salary = 10000;
>         System.out.println(DEPARTMENT+"平均工资:"+salary);
>     }
> }
> //开发人员平均工资:10000.0
> ```

#### 静态方法

（1）静态方法中不需要它所属类的任何实例就可以访问，所以在静态方法中不可以使用this关键字
（2）静态方法中不可直接访问所属类的实例变量和实例方法，但可以直接访问所属类的静态变量和静态方法

## 继承与接口规范

1.继承：在 Java 中，一个类可以由其他类派生。如果你要创建一个类，而且已经存在一个类具有你所需要的属性或方法，那么你可以将新创建的类继承该类。利用继承的方法，可以重用已存在类的方法和属性，而不用重写这些代码。被继承的类称为超类（super class），派生类称为子类（sub class）。

2.接口：在 Java 中，接口可理解为对象间相互通信的协议。接口在继承中扮演着很重要的角色。接口只定义派生要用到的方法，但是方法的具体实现完全取决于派生类。

## 基本数据类型

变量就是申请内存来存储值。也就是说，当创建变量的时候，需要在内存中申请空间。内存管理系统根据变量的类型为变量分配存储空间，分配的空间只能用来储存该类型数据。

![img](https://www.runoob.com/wp-content/uploads/2013/12/2020-10-27-code-mem.png)

Java 的两大数据类型:

- **内置数据类型**
- **引用数据类型**

### **内置数据类型**

Java语言提供了**八种基本类型**。六种数字类型（**四个整数型，两个浮点型**），**一种字符类型**，还有一种**布尔**型。

> - **byte**：8位有符号的以二进制补码表示的整数；最小值是 **-128（-2^7）**最大值是 **127（2^7-1）**默认值是 **0**；
>
> byte 类型用在大型数组中节约空间，主要代替整数，因为 byte 变量占用的空间只有 int 类型的四分之一；
>
> - **short：**16 位、有符号的以二进制补码表示的整数，最小值是 **-32768（-2^15）**最大值是 **32767（2^15 - 1）**默认值是 **0** 
>
> Short 数据类型也可以像 byte 那样节省空间。一个short变量是int型变量所占空间的二分之一；
>
> - **int**：32位、有符号的以二进制补码表示的整数；最小值是 **-2,147,483,648（-2^31）**最大值是 **2,147,483,647（2^31 - 1）**默认值是 **0**
>
> 一般地整型变量默认为 int 类型
>
> - **long：** 64 位、有符号的以二进制补码表示的整数；最小值是 **-9,223,372,036,854,775,808（-2^63）**；最大值是 **9,223,372,036,854,775,807（2^63 -1）**；
>
> 默认值是 **0L **这种类型主要使用在需要比较大整数的系统上；
>
> - **float：**单精度、32位、符合IEEE 754标准的浮点数；默认值是 **0.0f**；
>
> 浮点数不能用来表示精确的值，如货币；float 在储存大型浮点数组的时候可节省内存空间；
>
> - **double：**双精度、64 位、符合 IEEE 754 标准的浮点数；double类型同样不能表示精确的值，如货币；
>
> 默认值是 **0.0d**；浮点数的默认类型为 double 类型；
>
> - **char**：一个单一的 16 位 Unicode 字符；最小值是 **\u0000**（十进制等效值为 0）；最大值是 **\uffff**（即为 65535）；char 数据类型可以储存任何字符；例子：char letter = 'A';
>
> - **boolean：**只有两个取值：true 和 false；**默认值是 false**

### **引用数据类型**

> 在Java中，引用类型的变量非常类似于C/C++的指针。引用类型指向一个对象，指向对象的变量是引用变量。这些变量在声明时被指定为一个特定的类型，比如 Employee、Puppy 等。变量一旦声明后，类型就不能被改变了。
>
> 所有引用类型的默认值都是null；对象、数组都是引用数据类型；一个引用变量可以用来引用任何与之兼容的类型。
>
> ### 引用类型
>
> > 引用是一个对象别名，与被引用的对象共享同一块内存区域。例如“鹿晗”这个对象，他的原名是“刘壮实”，但两者其实都是指同一个人（内存）。对象在创建时会请求一块内存空间来保存数据，会根据对象大小分配存储空间大小不等的内存区域。在Java中，访问对象时，不会直接访问对象在内存中的数据，而是通过引用去访问。因此，引用也是一种数据类型，类似于C/C++ 语言中的指针。引用定义时在栈中分配内存，引用变量在程序运行到作用域外释。
> >
> > java的引用类型有：1、强引用；2、软引用；3、弱引用；4、虚引用。

### 类型转换规范

<u>整数的默认类型是 int ; 小数默认是 double 类型浮点型，在定义 float 类型时必须在数字后面跟上 F 或者 f。</u>

**整型、实型（常量）、字符型数据可以混合运算。运算中，不同类型的数据先转化为同一类型，然后进行运算。**

```xml
转换从低级到高级。
低  ------------------------------------>  高
byte,short,char—> int —> long—> float —> double 
```

1.  不能对boolean类型进行类型转换。

2.  不能把对象类型转换成不相关类的对象。

3. 在把容量大的类型转换为容量小的类型时必须使用强制类型转换。

4. 转换过程中可能导致溢出或损失精度，例如：

   ```java
   int i =128;   
   byte b = (byte)i;
   //因为 byte 类型是 8 位，最大值为127，所以当 int 强制转换为 byte 类型时，值 128 时候就会导致溢出。
   ```

5. 浮点数到整数的转换是通过舍弃小数得到，而不是四舍五入，例如：

   ```java
   (int)23.7 == 23;        
   (int)-45.89f == -45
   ```

**java中的类型转换大致分为两种：1.自动类型转换  2.强制类型转换** 

#### 1.自动类型转换

必须满足转换前的数据类型的位数要低于转换后的数据类型，例如: short数据类型的位数为16位，就可以自动转换位数为32的int类型，同样float数据类型的位数为32，可以自动转换为64位的double类型。

```java
public class ZiDongLeiZhuan{
        public static void main(String[] args){
            char c1='a';//定义一个char类型
            int i1 = c1;//char自动类型转换为int
            System.out.println("char自动类型转换为int后的值等于"+i1);
            char c2 = 'A';//定义一个char类型
            int i2 = c2+1;//char 类型和 int 类型计算
            System.out.println("char类型和int计算后的值等于"+i2);
        }
}
//char自动类型转换为int后的值等于97
//char类型和int计算后的值等于66
解析：c1 的值为字符 a ,查 ASCII 码表可知对应的 int 类型值为 97， A 对应值为 65，所以 i2=65+1=66。
```

#### 2.强制类型转换

条件是转换的数据类型必须是兼容的。格式：(type)value type是要强制类型转换后的数据类型 实例：

```java
public class QiangZhiZhuanHuan{
    public static void main(String[] args){
        int i1 = 123;
        byte b = (byte)i1;//强制类型转换为byte
        System.out.println("int强制类型转换为byte后的值等于"+b);
    }
}
//int强制类型转换为byte后的值等于123
```

## Java 异常处理

异常是程序中的一些错误，但并不是所有的错误都是异常，并且错误有时候是可以避免的。

异常发生的原因有很多，通常包含以下几大类：

- **用户输入了非法数据。**
- **要打开的文件不存在。**
- **网络通信时连接中断，或者JVM内存溢出。**

这些异常有的是因为用户错误引起，有的是程序错误引起的，还有其它一些是因为物理错误引起的。

要理解Java异常处理是如何工作的，你需要掌握以下三种类型的异常：

- **检查性异常：**最具代表的检查性异常是用户错误或问题引起的异常，这是程序员无法预见的。例如要打开一个不存在文件时，一个异常就发生了，这些异常在编译时不能被简单地忽略。
- **运行时异常：** 运行时异常是可能被程序员避免的异常。与检查性异常相反，运行时异常可以在编译时被忽略。
- **错误：** 错误不是异常，而是脱离程序员控制的问题。错误在代码中通常被忽略。例如，当栈溢出时，一个错误就发生了，它们在编译也检查不到的。

### Exception 类

所有的异常类是从 java.lang.Exception 类继承的子类。

Exception 类是 Throwable 类的子类。除了Exception类外，Throwable还有一个子类Error 。

Java 程序通常不捕获错误。错误一般发生在严重故障时，它们在Java程序处理的范畴之外。

Error 用来指示运行时环境发生的错误。

例如，JVM 内存溢出。一般地，程序不会从错误中恢复。

异常类有两个主要的子类：IOException 类和 RuntimeException 类。![img](https://www.runoob.com/wp-content/uploads/2013/12/exception-hierarchy.png)

### Java 内置异常类

Java 语言定义了一些异常类在 java.lang 标准包中。

标准运行时异常类的子类是最常见的异常类。由于 java.lang 包是默认加载到所有的 Java 程序的，所以大部分从运行时异常类继承而来的异常都可以直接使用。

Java 根据各个类库也定义了一些其他的异常，下面的表中列出了 Java 的**非检查性异常**。

| **异常**                        | **描述**                                                     |
| :------------------------------ | :----------------------------------------------------------- |
| ArithmeticException             | 当出现异常的运算条件时，抛出此异常。例如，一个整数"除以零"时，抛出此类的一个实例。 |
| ArrayIndexOutOfBoundsException  | 用非法索引访问数组时抛出的异常。如果索引为负或大于等于数组大小，则该索引为非法索引。 |
| ArrayStoreException             | 试图将错误类型的对象存储到一个对象数组时抛出的异常。         |
| ClassCastException              | 当试图将对象强制转换为不是实例的子类时，抛出该异常。         |
| IllegalArgumentException        | 抛出的异常表明向方法传递了一个不合法或不正确的参数。         |
| IllegalMonitorStateException    | 抛出的异常表明某一线程已经试图等待对象的监视器，或者试图通知其他正在等待对象的监视器而本身没有指定监视器的线程。 |
| IllegalStateException           | 在非法或不适当的时间调用方法时产生的信号。换句话说，即 Java 环境或 Java 应用程序没有处于请求操作所要求的适当状态下。 |
| IllegalThreadStateException     | 线程没有处于请求操作所要求的适当状态时抛出的异常。           |
| IndexOutOfBoundsException       | 指示某排序索引（例如对数组、字符串或向量的排序）超出范围时抛出。 |
| NegativeArraySizeException      | 如果应用程序试图创建大小为负的数组，则抛出该异常。           |
| NullPointerException            | 当应用程序试图在需要对象的地方使用 `null` 时，抛出该异常     |
| NumberFormatException           | 当应用程序试图将字符串转换成一种数值类型，但该字符串不能转换为适当格式时，抛出该异常。 |
| SecurityException               | 由安全管理器抛出的异常，指示存在安全侵犯。                   |
| StringIndexOutOfBoundsException | 此异常由 `String` 方法抛出，指示索引或者为负，或者超出字符串的大小。 |
| UnsupportedOperationException   | 当不支持请求的操作时，抛出该异常。                           |

下面的表中列出了 Java 定义在 java.lang 包中的**检查性异常类**。

| **异常**                   | **描述**                                                     |
| :------------------------- | :----------------------------------------------------------- |
| ClassNotFoundException     | 应用程序试图加载类时，找不到相应的类，抛出该异常。           |
| CloneNotSupportedException | 当调用 `Object` 类中的 `clone` 方法克隆对象，但该对象的类无法实现 `Cloneable` 接口时，抛出该异常。 |
| IllegalAccessException     | 拒绝访问一个类的时候，抛出该异常。                           |
| InstantiationException     | 当试图使用 `Class` 类中的 `newInstance` 方法创建一个类的实例，而指定的类对象因为是一个接口或是一个抽象类而无法实例化时，抛出该异常。 |
| InterruptedException       | 一个线程被另一个线程中断，抛出该异常。                       |
| NoSuchFieldException       | 请求的变量不存在                                             |
| NoSuchMethodException      | 请求的方法不存在                                             |

### 异常方法

下面的列表是 Throwable 类的主要方法:

| **序号** | **方法及说明**                                               |
| :------- | :----------------------------------------------------------- |
| 1        | **public String getMessage()** 返回关于发生的异常的详细信息。这个消息在Throwable 类的构造函数中初始化了。 |
| 2        | **public Throwable getCause()** 返回一个 Throwable 对象代表异常原因。 |
| 3        | **public String toString()** 返回此 Throwable 的简短描述。   |
| 4        | **public void printStackTrace()** 将此 Throwable 及其回溯打印到标准错误流。。 |
| 5        | **public StackTraceElement [] getStackTrace()** 返回一个包含堆栈层次的数组。下标为0的元素代表栈顶，最后一个元素代表方法调用堆栈的栈底。 |
| 6        | **public Throwable fillInStackTrace()** 用当前的调用栈层次填充Throwable 对象栈层次，添加到栈层次任何先前信息中。 |

### 捕获异常<重要>

使用 try 和 catch 关键字可以捕获异常。try/catch 代码块放在异常可能发生的地方。

try/catch代码块中的代码称为保护代码，使用 try/catch 的语法如下：

```
try
{
   // 程序代码
}catch(ExceptionName e1)
{
   //Catch 块
}
```

Catch 语句包含要捕获异常类型的声明。当保护代码块中发生一个异常时，try 后面的 catch 块就会被检查。

如果发生的异常包含在 catch 块中，异常会被传递到该 catch 块，这和传递一个参数到方法是一样。

```java
// 文件名 : ExcepTest.java
import java.io.*;
public class ExcepTest{
 
   public static void main(String args[]){
      try{
         int a[] = new int[2];
         System.out.println("Access element three :" + a[3]);
      }catch(ArrayIndexOutOfBoundsException e){
         System.out.println("Exception thrown  :" + e);
      }
      System.out.println("Out of the block");
   }
}
//Exception thrown  :java.lang.ArrayIndexOutOfBoundsException: 3
//Out of the block
```

### 多重捕获块

一个 try 代码块后面跟随多个 catch 代码块的情况就叫多重捕获。

多重捕获块的语法如下所示：

```java
try{
   // 程序代码
}catch(异常类型1 异常的变量名1){
  // 程序代码
}catch(异常类型2 异常的变量名2){
  // 程序代码
}catch(异常类型3 异常的变量名3){
  // 程序代码
}
```

上面的代码段包含了 3 个 catch块。

可以在 try 语句后面添加任意数量的 catch 块。

如果保护代码中发生异常，异常被抛给第一个 catch 块。

如果抛出异常的数据类型与 ExceptionType1 匹配，它在这里就会被捕获。

如果不匹配，它会被传递给第二个 catch 块。

如此，直到异常被捕获或者通过所有的 catch 块。

```java
#实例:
    try {
    file = new FileInputStream(fileName);
    x = (byte) file.read();
} catch(FileNotFoundException f) { // Not valid!
    f.printStackTrace();
    return -1;
} catch(IOException i) {
    i.printStackTrace();
    return -1;
}
```

### throws/throw 关键字

如果一个方法没有捕获到一个检查性异常，那么该方法必须使用 throws 关键字来声明。throws 关键字放在方法签名的尾部。

也可以使用 throw 关键字抛出一个异常，无论它是新实例化的还是刚捕获到的。

**一个方法可以声明抛出多个异常，多个异常之间用逗号隔开。**

例如，下面的方法声明抛出 RemoteException 和 InsufficientFundsException：

```java
import java.io.*;
public class className
{
   public void withdraw(double amount) throws RemoteException,
                              InsufficientFundsException
   {
       // Method implementation
   }
   //Remainder of class definition
}
```

### finally关键字

finally 关键字用来创建在 try 代码块后面执行的代码块。

无论是否发生异常，finally 代码块中的代码总会被执行。

在 finally 代码块中，可以运行清理类型等收尾善后性质的语句。

finally 代码块出现在 catch 代码块最后，语法如下：

```java
try{
  // 程序代码
}catch(异常类型1 异常的变量名1){
  // 程序代码
}catch(异常类型2 异常的变量名2){
  // 程序代码
}finally{
  // 程序代码
}
```

```java
//实例：
public class ExcepTest{
  public static void main(String args[]){
    int a[] = new int[2];
    try{
       System.out.println("Access element three :" + a[3]);
    }catch(ArrayIndexOutOfBoundsException e){
       System.out.println("Exception thrown  :" + e);
    }
    finally{
       a[0] = 6;
       System.out.println("First element value: " +a[0]);
       System.out.println("The finally statement is executed");
    }
  }
}
//Exception thrown  :java.lang.ArrayIndexOutOfBoundsException: 3
//First element value: 6
//The finally statement is executed
```

### try-with-resources语法糖

JDK7 之后，Java 新增的 **try-with-resource** 语法糖来打开资源，并且可以在语句执行完毕后确保每个资源都被自动关闭 。

JDK7 之前所有被打开的系统资源，比如流、文件或者 Socket 连接等，都需要被开发者手动关闭，否则将会造成资源泄露。

```java
try (resource declaration) {
  // 使用的资源
} catch (ExceptionType e1) {
  // 异常块
}
```

以上的语法中 try 用于声明和实例化资源，catch 用于处理关闭资源时可能引发的所有异常。

**注意：**try-with-resources 语句关闭所有实现 AutoCloseable 接口的资源。

```java
public class RunoobTest {

    public static void main(String[] args) {
    String line;
        try(BufferedReader br = new BufferedReader(new FileReader("test.txt"))) {
            while ((line = br.readLine()) != null) {
                System.out.println("Line =>"+line);
            }
        } catch (IOException e) {
            System.out.println("IOException in try block =>" + e.getMessage());
        }
    }
}
```

以上实例输出结果为：

```
IOException in try block =>test.txt (No such file or directory)
```

### 通用异常

在Java中定义了两种类型的异常和错误。

- **JVM(Java虚拟机)**异常：**由 JVM 抛出的异常或错误。例如：NullPointerException 类，ArrayIndexOutOfBoundsException 类，ClassCastException 类。
- **程序级异常：**由程序或者API程序抛出的异常。例如 IllegalArgumentException 类，IllegalStateException 类。

# Spring

**全面的企业应用开发一站式的解决方案 (与其他框架兼容 例如MyBatis,Hibernate,Shrio)**

**特点 ：轻量级(仅需2M JAR文件)  非入侵式(无捆绑的)  应用中的对象不依赖与spring特定类 支持junit4测试**![spring-overview](https://www.runoob.com/wp-content/uploads/2015/07/673670c9a34075831373b711cb8f21b7.png)

## Spring的核心机制

**管理Bean**

程序主要是通过Spring容器来访问容器中的Bean，ApplicationContext是Spring容器最常用的接口，该接口有如下两个实现类：

- ClassPathXmlApplicationContext: 从类加载路径下搜索配置文件，并根据配置文件来创建Spring容器。
- FileSystemXmlApplicationContext: 从文件系统的相对路径或绝对路径下去搜索配置文件，并根据配置文件来创建Spring容器。

```java
public class BeanTest{
    public static void main(String args[]) throws Exception{
        ApplicationContext ctx = new ClassPathXmlApplicationContext("beans.xml");
        Person p = ctx.getBean("person", Person.class);
        p.say();
    }
}
```





## **1.控制反转IOC  **

**由spring容器管理整个bean的生命周期 通过<u>反射</u>实现对其它对象控制 包括初始化 创建 销毁等 无需手动管理对象过程**

> **1.1依赖注入DI**   促进低耦合 常用@Autowired根据属性自动装配无需字段的 set 方法 
>
> ```java
> //成员属性字段使用 @Autowired，无需字段的 set 方法
> @Autowired
> private AdminServiceImpl adminService;
> //set 方法使用 @Autowired
> private AdminServiceImpl adminService1;
> @Autowired
> public void setAdminService1(AdminServiceImpl adminService){
>   this.adminService1 = adminService;
> }
> //构造方法使用 @Autowired
> private AdminServiceImpl adminService2;
> @Autowired
> AdminController(AdminServiceImpl adminService){
>   this.adminService2 = adminService;
> }
> ```
>
> ----
>
> **1.2依赖查询DL** 
>
> **一个对象依赖的其他对象会以被动的方式传递进来 即无需创建查找依赖对象**
>
> **实现：容器中的受控对象通过容器的 API 来查找自己所依赖的资源和协作对象。**
>
> 依赖查询DL也有两种方式
>
> - 依赖拖拽：注入的对象如何与组件发生联系，这个过程就是通过依赖拖拽实现；
>
> - 上下文依赖查找：在某些方面跟依赖拖拽类似，但是上下文依赖查找中，查找的过程是在容器管理的资源中进行的，而不是从集中注册表中，并且通常是作用在某些设置点上；
>
>   ---
>

### **<u>简述IOC初始化过程？</u>**

> > 1. 首先要看你是怎么声明注入bean的  常见的**xml 配置 注解  bean配置** 我最常用的是**AnnotationConfigApplication**注解容器，也就是使用**@Configuration**进行注册 然后解析成Bean
> > 2. 将Bean解析成**BeanDefinition** 一个对bean信息进行包装的类 会对bean配置的参数进行或者是XML配置的property标签注入到BeanDefinition的实例中
> > 3. 再将对应的**beanDefinition**实例注册到容器**beanDefinitionMap**中
> > 4. **beanfactory**根据BeanDefinition创建实例化和初始化bean
>
> ----
>

### <u>**spring加载bean有哪些方式？**</u>

> > 1.首先要通过@Configuration+@Bean
> >
> > @Configuration用来声明一个配置类 然后使用@Bean声明一个bean 将其加入spring容器
> >
> > ```java
> > @Configuration
> > public class TestConfiguration {
> > @Bean
> > public Admin admin(){
> >   return new Admin();
> > }
> > }
> > ```
> >
> > 2.包扫描特定注解的方式 使用@Component或者@ComponentScan 
> >
> > @Component声明自己是个等待spring将自己实例化到spring容器中的类 让spring容器来统一管理 用起来不需要new了 相当于:
> >
> > ```java
> > <bean id="" class=""/>
> > ```
> >
> > 而@ComponentScan会指定一个路径 扫描路径内带有特定注解的bean 相当于告诉spring容器去哪里找自己需要的bean 添加进容器中 其中特定的注解会包括@Controller @Service @Repository @Component
> >
> > ```java
> > // 控制层
> > @Controller
> > public class UserController {
> > }
> > 
> > // 业务层
> > @Service
> > public class UserService {
> > }
> > 
> > // 持久层
> > @Repository
> > public class UserDao {
> > }
> > ```
> >
> > ```java
> > public class TestConfiguration {
> > @Test
> > public void Test() {
> >   AnnotationConfigApplicationContext applicationContext = new AnnotationConfigApplicationContext(AppConfig.class);
> >   String[] beanNames = applicationContext.getBeanDefinitionNames();
> >   for (String beanName:beanNames) {
> >       System.out.println("容器中对象名称："+beanName);
> >   }
> > 
> > }
> > }
> > @Configuration
> > @ComponentScan(value = "com.example.app.goodjobdemo.Test")
> > class AppConfig {
> > }
> > //容器中对象名称：appConfig
> > //容器中对象名称：userController
> > //容器中对象名称：userDao
> > //容器中对象名称：userService
> > ```
> >
> > 3.@Import注解导入 开发中很少使用 对spring扩展的时候才会经常用到 通常搭配自定义注解使用往容器导入配置类文件
> >
> > ```java
> > public class TestConfiguration {
> > @Test
> > public void Test() {
> >   AnnotationConfigApplicationContext applicationContext = new AnnotationConfigApplicationContext(AppConfig.class);
> >   String[] beanNames = applicationContext.getBeanDefinitionNames();
> >   for (String beanName:beanNames) {
> >       System.out.println("容器中对象名称："+beanName);
> >   }
> > 
> > }
> > }
> > @Configuration
> > @Import({UserController.class,UserDao.class,UserService.class})
> > class AppConfig {
> > }
> > //容器中对象名称：appConfig
> > //容器中对象名称：com.example.app.goodjobdemo.Test.UserController
> > //容器中对象名称：com.example.app.goodjobdemo.Test.UserDao
> > //容器中对象名称：com.example.app.goodjobdemo.Test.UserService
> > ```
> >
> > 4.实现BeanDefinitionRegistryPostProcessor进行后置处理
> >
> > ```java
> > //源码 BeanFactoryPostProcessor接口中只有一个方法 就是postProcessBeanDefinitionRegistry
> > public interface BeanDefinitionRegistryPostProcessor extends BeanFactoryPostProcessor {
> > 	void postProcessBeanDefinitionRegistry(BeanDefinitionRegistry registry) throws BeansException;
> > }
> > ```
> >
> > spring容器启动会执行postProcessBeanDefinitionRegistry方法 
> >
> > 即 等BeanDefinition加载完毕后进行后置处理 在此调整BeanDefinition就可以干扰到后面初始化bean操作
> >
> > 5.使用FactoryBean接口 
> >
> > 使用@Configuration+@Bean方式将AdminFactoryBean加入到容器中
> >
> > 代码如下 并没有向容器中直接注入Admin 而是注入AdminFactoryBean然后再从容器中拿到Admin这个类型的Bean
> >
> > ```java
> > @Configuration
> > public class TestConfiguration {
> > @Bean
> > public AdminFactoryBean adminFactoryBean(){
> >   return new AdminFactoryBean();
> > }
> > @Test
> > public void Test() {
> >   AnnotationConfigApplicationContext applicationContext = new AnnotationConfigApplicationContext(TestConfiguration.class);
> >   Admin bean = applicationContext.getBean(Admin.class);
> >   System.out.println(bean);
> > }
> > }
> > @Component
> > class AdminFactoryBean implements FactoryBean {
> > @Override
> > public Admin getObject() throws Exception {
> >   return new Admin();
> > }
> > @Override
> > public Class<?> getObjectType() {
> >   return Admin.class;
> > }
> > }
> > //Admin(id=null, name=null, password=null)
> > ```
> >
> > 还有很多实现注入Bean的方法
> >
> > `1.xml；2.扫描加注解；3.配置类@bean；4.实现factorybean；5.annotationapplicationcontext的register注册；6.import类；7.selectimport实现类；8.实现importbeandefinitionregister自定义bean；9.实现beandefinitionregisterpostprocessor后置注册修改bean`
>
> ---
>

### <u>**Spring bean 的生命周期？**</u>

> 1.调用Bean的构造方法创建Bean
>
> 2.通过反射调用setter方法进行属性依赖注入
>
> 2.1如果bean实现了BeanNameAware接口 spring将调用setBeanName()方法设置Bean的name(对应xml文件中bean的标签id)
>
> 2.2如果bean实现实现了BeanFacoryAware接口spring就将调用2.3setBeanFactory()把beanfactory设置给bean
>
> 2.4如果存在beanPostProcessor spring将会调用postProcessBeforeLinitialization预处理方法在bean初始化之前对其处理
>
> 2.5如果bean实现了InitialigBean接口spring将调用tafterPropertiesSet()方法 然后调用xml定义的init-method方法 两个方法作用类似 都是再初始化bean的时候执行
>
> 2.6如果存在beanPostProcessor spring将会调用postProcessAfterLinitialization初始化后方法在bean初始化之后对其处理
>
> 3.bean初始化完成 供应用使用 分为两种情况：
>
> 3.1如果bean为单例的话那么容器返回bean给用户并存入缓存池
>
> 如果实现了DisposableBean接口 spring将调用他的destory()然后调用xml中定义的destory-mothod方法 这两个方法作用类似都是在bean实例销毁前执行
>
> 3.2如说bean是多例的话 容器将bean返回给用户 剩下的生命周期将由用户控制
>
> ---

### <u>**Spring怎么解决循环依赖的？**</u>

> **Spring通过三级缓存来解决缓存依赖** 
>
> #example:两个对象互相形成依赖
> 创建Bean-A时 对Bean-A进行构造方法后就将Bean-A对象放入Spring的三级缓存**singletonFactories**
>
> 发现Bean-A依赖Bean-B，开始创建Bean-B并执行完Bean-B的构造方法后，放入三级缓存
>
> 处理Bean-B的依赖Bean-A时，发现三级缓存中有一个Bean-A，拿到这个BeanA完成B的注入，同时也完成A的注入

### **<u>Spring Bean如何保证并发安全？</u>**

> > ```yaml
> > example:
> > spring的bean默认都是单例的 singleton 某些情况下单例并发是不安全的
> > 假如我们在Controller控制层定义了成员变量 多个请求来临时进入的都是同一单例对象并且对成员变量进行修改会有并发安全风险
> > 如何解决？
> > ```
> >
> > 1.单例变原型
> >
> > 如果是web应用在controller类上加**@Scope("prototype")**或者**@Scope("request")**
> >
> > 如果不是web应用在Component类上加注解**@Scope("prototype")**
> >
> > 这种方式实现起虽然简单 但是会增加服务器资源中bean创建销毁实例的开销
> >
> > 2.尽量避免使用成员变量
> >
> > 在业务允许范围内 使用RequsetMapping方法中的局部变量替换控制层的成员 这种方式比较恰当
> >
> > 3.使用并发安全类
> >
> > 如果如果一定需要在单例bean使用成员变量 可以使用并发安全的容器
> >
> > 例如 ConcurrentHashMap  ConcurrentHashSet
> >
> > 4.分布式或者微服务 项目的并发安全解决方案
> >
> > 如果还需要考虑到微服务或者分布式服务的并发安全解决 第三种方法便不太合适
> >
> > 借助于可以共享某些信息的分布式缓存中间件 例如Redis等
> >
> > 这样既可以保证统一服务 不同服务实例 且都有同一共享信息
>
> ---
>

### **<u>Spring用到了那些设计模式？</u>**

> > **1.工厂模式** IOC容器可以使用BeanFactory 或 ApplicationContext创建 bean 对象 
> >
> > - BeanFactory 是bean合集工厂类 懒加载或者延时加载 (使用到某个 bean 的时候才会注入) 启动速度快占用内存少
> >
> > - ApplicationContext 是BeanFactory的扩展(接口提供额外功能)  即使加载(容器启动的时候 不管你用没用到 一次性创建所有 bean) 开发人员使用ApplicationContext会更多 
> >
> >   ```yaml
> >   #ApplicationContext的三个实现类
> >   -ClassPathXmlApplication：从类的根路径下加载配置文件（推荐使用这种）
> >   -FileSystemXmlApplication：它是从磁盘路径上加载配置文件，配置文件可以在磁盘的任意位置。
> >   -XmlWebApplicationContext：从Web系统中的XML文件载入上下文定义信息。
> >   -AnnotationConfigApplicationContext：当使用注解配置容器对象时，需要使用此类来创建 spring 容器。它用来读取注解
> >   ```
> >
> >   ```java
> >   //example
> >   ApplicationContext applicationContext = new ClassPathXmlApplicationContext("applicationContext.xml");
> >   UserService userService = (UserService) applicationContext.getBean("userService");
> >   userService.save();
> >   ```
> >
> > ---
> >
> > **2.单例模式** 一个类仅有一个实例 提供一个访问它的全局访问点
> >
> > **由于Spring中bean的默认作用域就是singleton(单例)的 优点如下：**
> >
> > - 对于频繁使用的对象，可以**省略创建对象所花费的时间**
> > - 由于new操作的次数减少，因而**对系统内存的使用频率也会降低 **减轻GC压力，缩短GC停顿时间
> >
> > **除了singleton作用域，Spring中bean还有下面几种作用域**
> >
> > - prototype : **每次**请求都会创建一个新的 bean 实例。
> > - request : 每一次HTTP请求都会产生一个新的bean，该bean仅在当前**HTTP request**内有效。
> > - session : 每一次HTTP请求都会产生一个新的 bean，该bean仅在当前**HTTP session**内有效。
> >
> > ---
> >
> > **3.代理模式**
> >
> > **1.Spring AOP**(Aspect-Oriented Programming:面向切面编程) **基于代理操作** 提供了两种动态代理实现 且都是**运行时增强** 
> >
> > - JDK Proxy 
> > - CGLIB Proxy
> >
> > **2.AspectJ AOP**  **是编译时增强**   基于**字节码操作(Bytecode Manipulation)**
> >
> > Spring AOP 已经集成了 AspectJ  相比于 Spring AOP 功能更加强大，但是 Spring AOP 相对来说更简单。如果我们的切面比较少，那么两者性能差异不大。但是，当切面太多的话，最好选择 AspectJ ，它比Spring AOP 快很多。
> >
> > ----
> >
> > **4.适配器模式 <Adapter Pattern>**
> >
> > **将一个接口转换成客户希望的另一个接口，适配器模式使接口不兼容的那些类可以一起工作，其别名为包装器(<u>Wrapper</u>)。**
> >
> > 比如 Spring MVC 中适配器HandlerAdatper，应用会有多个不同类型的Controller实现。如果需要调用方法会先判断是哪个Controller 再对应处理
> >
> > 如果增加一个 Controller就需要修改原来的判断逻辑 不利于维护 违反了模式设计开闭原则 <对扩展开放，对修改关闭>
> >
> > 为此Spring提供了该适配器接口 每个Controller对应一种HandlerAdatper实现类 对应请求时SpringMVC会通过getHandler()指定对应的Controller获取HandlerAdatper最后调用Handle()方法处理请求 实际是调用Controller的HandleRequest()方法
> >
> > 这种方法处理每次添加新的Controller时 只需增加一个适配器类即可 无需修改原有逻辑
> >
> > ---
> >
> > **5.观察者模式**      一种对象与对象之间具有依赖关系，当一个对象发生改变的时候，这个对象所依赖的对象也会做出反应
> >
> > - 事件角色 ：ApplicationEvent (org.springframework.context包下)抽象类
> >
> >    继承了java.util.EventObject并实现了 java.io.Serializable接口。
> >
> >   ```yaml
> >   #对ApplicationContextEvent的实现(继承自ApplicationContextEvent)
> >   - ContextStartedEvent：ApplicationContext 启动后触发的事件;
> >   - ContextStoppedEvent：ApplicationContext 停止后触发的事件;
> >   - ContextRefreshedEvent：ApplicationContext 初始化或刷新完成后触发的事件;
> >   - ContextClosedEvent：ApplicationContext 关闭后触发的事件。
> >   ```
> >
> > - 事件监听者角色  ApplicationListener接口 <java.util.EventListener>
> >
> >   里面只定义了一个 onApplicationEvent()方法来处理ApplicationEvent
> >
> >   我们只要实现 ApplicationListener 接口实现 onApplicationEvent() 方法即可完成监听事件
> >
> >   ```java
> >   package org.springframework.context;
> >   import java.util.EventListener;
> >   @FunctionalInterface
> >   public interface ApplicationListener<E extends ApplicationEvent> extends EventListener {
> >       void onApplicationEvent(E var1);
> >   }
> >   ```
> >
> > - 事件发布者角色 ApplicationEventPublisher  事件的发布者，它也是一个接口
> >
> >   ApplicationEventPublisher 接口的publishEvent()这个方法在AbstractApplicationContext类中被实现
> >
> >   实际是通过ApplicationEventMulticaster来广播出去的
> >
> >   ```java
> >   @FunctionalInterface
> >   public interface ApplicationEventPublisher {
> >       default void publishEvent(ApplicationEvent event) {
> >           this.publishEvent((Object)event);
> >       }
> >                                 
> >       void publishEvent(Object var1);
> >   }
> >   ```
> >
> > ---
> >
> > **6.模板模式 **
> >
> > 一个操作中的算法的骨架，而将一些步骤延迟到子类中。 
> >
> > 模板方法使得子类可以不改变一个算法的结构即可重定义该算法的某些特定步骤的实现方式。
> >
> > Spring 中 jdbcTemplate、hibernateTemplate 等以 Template 结尾的对数据库操作的类，它们就使用到了模板模式。一般情况下，我们都是使用继承的方式来实现模板模式，但是 Spring 并没有使用这种方式，而是使用Callback 模式与模板方法模式配合，既达到了代码复用的效果，同时增加了灵活性。
> >
> > ---
> >
> > ### 概括总结：
> >
> > 工厂设计模式 : Spring使用工厂模式通过 BeanFactory、ApplicationContext 创建 bean 对象。
> > 代理设计模式 : Spring AOP 功能的实现。
> > 单例设计模式 : Spring 中的 Bean 默认都是单例的。
> > 模板方法模式 : Spring 中 jdbcTemplate hibernateTemplate 等以 Template 结尾的对数据库操作的类，它们就使用到了模板模式。
> > 观察者模式: Spring 事件驱动模型就是观察者模式很经典的一个应用。
> > 适配器模式 :Spring AOP 的增强或通知(Advice)使用到了适配器模式、spring MVC 中也是用到了适配器模式适配Controller。
> > 装饰者(包装器)设计模式 : 我们的项目需要连接多个数据库，而且不同的客户在每次访问中根据需要会去访问不同的数据库。这种模式让我们可以根据客户的需求能够动态切换不同的数据源。
> >
> > ---
> >
> > 装饰者模式和适配器模式都是包装模式（Wrapper Pattern），装饰者模式是一种特殊的代理模式，二者对比如下：
> >
> > |      |          装饰者模式          |                          适配器模式                          |
> > | :--: | :--------------------------: | :----------------------------------------------------------: |
> > | 形式 |       非常特别的适配器       |              没有层级关系，装饰者模式有层级关系              |
> > | 定义 | 装饰者和被装饰着实现同一接口 | 适配器和被适配这没有必然的关系，通常采用继承或代理的形式进行包装 |
> > | 关系 |         满足is-a关系         |                        满足has-a关系                         |
> > | 功能 |        注重覆盖、扩展        |                        注重兼容、转换                        |
> > | 设计 |           前置考虑           |                           后置考虑                           |

## **2.面向切面AOP**  

**目的是业务逻辑与系统服务分开**

> 将一些公共逻辑(例如日志，事务管理等)封装成切面**@aspect** 跟业务代码进行分开 减少系统重复代码以及降低模板之间的耦合度
>
> **AOP：**
>
> 1. Aspect(切面): 是通知和切入点的结合,通知和切入点共同定义了关于切面的全部内容—它的功能、在何时和何地完成其功能
> 2. joinpoint(连接点):所谓连接点是指那些被拦截到的点。在spring中,这些点指的是方法,因为spring只支持方法类型的连接点.
> 3. Pointcut(切入点):所谓切入点是指我们要对哪些joinpoint进行拦截的定义.（何地）
>
> **Spring框架提供以下几种类型的通知：**
>
> 1. 前置通知：先执行方面功能再执行目标功能
> 2. 后置通知：先执行目标功能再执行方面功能（目标无异常才执行方面）
> 3. 最终通知：先执行目标功能再执行方面功能(目标功能有无异常都执行方面)
> 4. 异常通知：先执行目标，抛出后执行方面
> 5. 环绕通知：先执行方面强制部分，然后执行目标，最后再执行方面后置部分
>
> ```java
> /*可以按照下面的try...catch...finally结构来理解/*/        
> 		try {
> //            前置通知-执行部分
> //            环绕通知前置部分
> //            环绕目标组件方法
> //            环绕通知后置部分
> //            后置通知执行部分
>         }catch(){
> //            异常通知执行部分
>         }finally {
> //            最终通知执行部分
> 
>         }
> ```
>
> 实现方式有两种 **静态代理和动态代理**
>

### **静态代理**：

代理类编译阶段生成 编译时增强 AspectJ就是静态代理  简单实现如下：

> ```java
>public class ProxyTest implements TestInterface {
>     //也实现目标接口，但是还包含目标对象的引用。
>    TestInterface Interface;
>     ProxyTest(TestInterface testInterface){
>         this.Interface=testInterface;
>     }
>    @Override
>     public void s_out() {
>        System.out.println("切面方法a");
>         this.Interface.s_out();//目标类的目标方法 (横向业务流：对应示意图的方法5();
>         System.out.println("切面方法f");
>     }
> }
> class ProxyTestMain{
>    public static void main(String[] args) {
>         //横向业务流：方法1();
>         TestInterface face = new ProxyTest(new TestObject());
>         face.s_out();///代理对象来代理目标对象，执行目标方法。
>         //横向业务流：方法7();
>     }
> }
> class TestObject implements TestInterface {
>     @Override//实现目标接口
>     public void s_out() {
>         System.out.println("实现方法");
>     }
> }
> interface TestInterface {
>     void s_out();//定义目标方法
> }
>```
> 
>**实现步骤：**
> 
>![](https://img-blog.csdn.net/20161009162557378)
> 
> ```java
> //完整案例
> interface TestInterface {//接口定义抽象想做的事 比如说批发钟薛糕
>     float initPrice =2;//单件钟薛糕成本原料价
>     float Initial(int count);//定义批发的这件事
> }
> class TestObject implements TestInterface {//商家最先实现生产
>     //实现接口 已知厂家的单件成本价2
>     float Price = initPrice + 5;//加价五元做批发
>     @Override//实现目标接口批发方法
>     public float Initial(int count) {
>         System.out.println("商家：");
>         System.out.println("我这里批发单件钟薛糕"+Price+"元");
>         System.out.println("你在我这批发了"+count+"件");
>         System.out.println("收你"+Price *count+"元");
>         System.out.println("实际上我赚取了"+(Price-initPrice)*count+"件");
>         return Price *count;
>     }
> }
> public class ProxyTest extends TestObject implements TestInterface {//开超市
>     float Price = super.Price+ 5;//加价五元做零售
>     //也实现目标接口，但是还包含目标对象的引用。
>     TestInterface Interface;
>     ProxyTest(TestInterface testInterface){//找到联系厂家的方式
>         this.Interface=testInterface;
>     }
>     @Override//实现目标接口批发方法
>     public float Initial(int count) {
>         //切面方法a();
>         System.out.println("超市：");
>         System.out.println("我这里卖单件钟薛糕"+Price+"元");
>        System.out.println("你在我这买了"+count+"件");
>         System.out.println("收你"+Price *count+"元");
>        System.out.println("实际上我赚取了"+5*count+"元");
>         //切面方法f();
>        return Price *count;
>     }
> }
> class ProxyTestMain{
>     public static void main(String[] args) {
>         System.out.println("买多少根钟薛糕？？");
>         Scanner scanner = new Scanner(System.in);
>         int count = scanner.nextInt();
>         System.out.println("每卖"+count+"跟钟薛糕产生的数据：");
>         TestObject testObject = new TestObject();
>         testObject.Initial(count);
>         //横向业务流：方法1();
>         TestInterface face = new ProxyTest(testObject);//开了个超市做代理 参数是商家
>         face.Initial(count);///代理对象来代理目标对象，执行目标方法。
>         //横向业务流：方法7();
>     }
> }
> /**买多少根钟薛糕？？
> 10
> 每卖10跟钟薛糕
> 商家：
> 我这里批发单件钟薛糕7.0元
> 你在我这批发了10件
> 收你70.0元
> 实际上我赚取了50.0件
> 超市：
> 我这里卖单件钟薛糕12.0元
> 你在我这买了10件
> 收你120.0元
> 实际上我赚取了50元**/
> ```
> 

### **动态代理：**

> 代理类运行时创建 aop框架不会修改字节码 在内存中临时生成一个代理对象 在运行期间对业务进行增强 不会产生新的类
>
> 而Spring AOP是基于**动态代理**的，基于两种动态代理机制： **JDK动态代理**和**CGLIB动态代理**
>

####  **JDK动态代理**：

> **目标类如果实现了接口 SpringAOP会自动采用JDK动态代理方式代理目标类**
>
> - 动态代理类跟目标类实现的接口动态生成 无需编写 
>
> - 生成的目标类和动态代理类都实现同样的
> 
> - JDK动态代理的核心是java.lang.reflect(反射包)里面有三个类：InvocationHandler, Method, Proxy
>
> - 没有实现接口就无法使用JDK动态代理
>
>   ```java
>   //JDK动态代理实例
>   public class ServiceProxy {
>   /**
>    * 基于接口的动态代理
>   * 对于一些需要重复执行的验证功能或下一步操作,
>    * 在核心方法执行前后都会执行增强的功能
>    */
>       public static Object newProxyInstance(Object target){
>       return Proxy.newProxyInstance(target.getClass().getClassLoader(),target.getClass().getInterfaces(), (proxy, method, args) -> {
>           System.out.println("动态增强功能1:登录权限认证");
>           System.out.println("动态增强功能2:黑名单验证");
>           System.out.println("----------------------");
>           Object invoke = method.invoke(target, args);//执行被代理的核心业务功能
>           System.out.println("----------------------");
>           System.out.println("动态增强功能3:进入订单中心");
>           return invoke;
>       });}}
>   interface UserServiceTest {//User业务方法
>       void testUserService();
>   }
>    @Service
>   class UServiceImpl implements UserServiceTest {//User业务方法实现
>      @Override
>       public void testUserService() {
>          System.out.println("User核心功能业务Service");
>       }
>   }
>   interface OrderServiceTest {//Order业务方法
>       void testOrderService();
>   }
>   @Service
>   class OServiceImpl implements OrderServiceTest {//Order业务方法实现
>       @Override
>       public void testOrderService() {
>           System.out.println("Order核心功能业务Service");
>       }
>   }
>   class ServiceProxyTest{//Test类
>       public static void main(String[] args) {
>           UserServiceTest userService= new UServiceImpl();
>           userService = (UserServiceTest)ServiceProxy.newProxyInstance(userService);
>           userService.testUserService();
>           System.out.println("==========================");
>           OrderServiceTest orderService=new OServiceImpl();
>           orderService = (OrderServiceTest)ServiceProxy.newProxyInstance(orderService);
>           orderService.testOrderService();
>       }
>   }
>   /**动态增强功能1:登录权限认证
>   动态增强功能2:黑名单验证
>   ----------------------
>   User核心功能业务Service
>   ----------------------
>   动态增强功能3:进入订单中心
>   ==========================
>   动态增强功能1:登录权限认证
>   动态增强功能2:黑名单验证
> ----------------------
>   Order核心功能业务Service
>  ----------------------
>   动态增强功能3:进入订单中心**/
>  ```
> 

#### **CGLIB动态代理：**

> **如果目标类没有实现接口 SpringAOP会自动采用CGLIB动态代理方式代理目标类**
>
> - 通过继承实现
>
> - 运行时动态生成类的字节码 动态创建目标类子类对象 在子类对象中增强目标类
> 
> - 无需实现特定接口 更加灵活
>
>   ```java
>    //CGLIB动态代理实例
>   public class CGLIBProxy {//CGLIB动态代理类
>       public static Object newProxyInstance(Object target) {
>           //1.工具类
>           Enhancer enhancer = new Enhancer();
>           //2.设置父类,传递类对象
>          enhancer.setSuperclass(target.getClass());
>           //3.设置回调函数
>           enhancer.setCallback((MethodInterceptor) (o, method, objects, methodProxy) -> {
>               System.out.println("cglib增强功能1");
>               System.out.println("cglib增强功能2");
>               System.out.println("-------------");
>               return method.invoke(target, objects);
>           });
>           //4.功能增强后，返回代理对象
>           return enhancer.create();
>       }
>   }
>   class UserServiceCGLIB{
>       public void testUserService() {
>           System.out.println("User核心功能业务Service");
>       }
>    }
>   class OrderServiceCGLIB {
>      public void testOrderService() {
>           System.out.println("Order核心功能业务Service");
>      }
>   }
>   class CGLIBTest {
>       public static void main(String[] args) {
>           UserServiceCGLIB us_cglib = new UserServiceCGLIB();
>           us_cglib= (UserServiceCGLIB)CGLIBProxy.newProxyInstance(us_cglib);
>           us_cglib.testUserService();
>           System.out.println("======================");
>           OrderServiceCGLIB os_cglib=new OrderServiceCGLIB();
>           os_cglib=(OrderServiceCGLIB)CGLIBProxy.newProxyInstance(os_cglib);
>           os_cglib.testOrderService();
>       }
>   }
>   /**cglib增强功能1
>   cglib增强功能2
>   -------------
>   User核心功能业务Service
>   ======================
>   cglib增强功能1
>   cglib增强功能2
>   -------------
>   Order核心功能业务Service**/
>   ```

-----------------------

---

# SpringBoot

1. 简化配置，SpringBoot的核心思想就是**约定大于配置**，省去xml配置

2. 简化部署，内置Tomcat，可以快速启动应用，以jar包的形式

3. 简化依赖，开发web应用，我们只需要在pom文件中添加如下一个 starter-web 依赖即可

   ```java
   <dependency>
       <groupId>org.springframework.boot</groupId>
       <artifactId>spring-boot-starter-web</artifactId>
   </dependency>
   ```

---

## Springboot的核心注解

**@SpringBootApplication ** 包含如下组合注解

- **@SpringBootConfiguration**：声明当前类是SpringBoot应用的配置类 又包括：

  @Configuration **主类上使用的注解** 等同于spring的XML<beans></beans>配置文件 指出该类是 **Bean 配置的信息源**

  @Bean 在**方法上使用的注解** 等同于<bean></bean> **声明一个Bean并且交给Spring管理**

  @ComPonent 声明 泛指各种组件 类不属于各种归类时(Controller services Repository等) 就用该注解标记此类

- **@EnableAutoConfiguration**：开启自动配置 也可以通过exclude属性关闭某个自动配置的Class

  ```yaml
  如关闭数据源自动配置功能： @SpringBootApplication(exclude = { DataSourceAutoConfiguration.class })；
  ```

  @AutoConfiggurationPackage 保存标注相关注解的类的所在包路径 使用一个BasePackage类保存路径 使用@Import注解将其注入到ioc容器中 < @Import(AutoConfiguartionPackages.Registrar.Class) >

  @Import 用来**导入其他配置类 **<@Import (AutoConfiguartionImportSelector.Class)>

- **@ComponentScan**：扫描Spring组件 通过**basePackageClasses**或者**basePackages**属性来指定要扫描包的路径 不指定我就扫自己包以及子包

- @ImportResource 加载xml配置文件

- @Autowired 自动注入依赖的bean 通过类型bytype方式 自动装配属性方法

- @Resource 默认byName方式注入 

---

## Starters

stater作用就是加载项目启动所需要的的相关jar包，不用去一个个找jar包pom了，一键式 只需要添加对应依赖即可。

---

## SpringBoot容器功能

### 1.组件添加 

- @Configuration  配置类 == 配置文件 **默认单例Full模式** 配置类本身也是组件

  属性 proxyBeanMethods 

  **Full模式**：`@Configuration(proxyBeanMethods = true)` 保证@Bean组件多少次使用返回都是单实例
  **Lite模式**：`@Configuration(proxyBeanMethods = false)  `保证@Bean组件多少次使用返回都是新建的

- @Bean 给容器中添加组件。以方法名作为组件的id。返回类型就是组件类型。返回的值，就是组件在容器中的实例。

- @ComponentScan Spring 组件扫描
- @Import 导入其他配置类
- @Conditional 条件装配

### 2.原生配置文件引入

- @ImportResource 导入原生配置文件 `@ImportResource("classpath:beans.xml")`

### 3.配置绑定 

读取properties文件内容 并封装到 JavaBean 中 供随时使用

- @ConfigurationProperties + @EnableConfigurationProperties
- @Component + @Configurationproperties

---

## 异常处理

- 在Controller方法中使用 @ExceptionHandler 处理**局部异常 **controller外的异常无法处理
- 使用@ControllerAdvice + @ExceptionHandler 注解处理**全局异常**（开发中常用）
- 配置 **SimpleMappingExceptionResolver** 类处理异常
- 实现 **HandlerExceptionResolver** 接口处理异常

---

## 事务   <Transactional>

- **声明式事务**： 通过**<u>AOP面向切面</u>**在方法前开启事务 方法后**提交**或**回滚 **通常用用配置文件或注解**@Transactional**控制事务
- **编程式事务**：**手动** 开启、提交、回滚事务。

操作：事务提交 or 事务回滚

```yaml
#example小明给如花转账：
开启事务--- 1.从小明的账户扣除1000块 2.给如花的账户增加1000块
事务提交--- 以上两步骤任意一个步骤出现问题 都会导致事务回滚
通俗来讲 从搭讪到结婚就是事务提交，女方要求男方重新追求她一次，就是事务回滚。
```

### 事务的四大特性 

1. **原子性(Atomicity):**事务中所有操作是不可分割的原子单位。事务中所有操作要么全部执行成功，要么全部执行失败。
2. **一致性(Consistency):**事务执行后，数据库状态与其它业务规则保持一致。如转正业务，无论事务执行成功与否，参与转账的两个账号余额之和应该是不变的。
3. **隔离性(Isolation):**隔离性是指在并发操作中，不同事务之间应该隔离开来，使每个并发中的事务不会相互干扰。
4. **持久性(Durability):**一旦事务提交成功，事务中所有的数据操作都必须被持久化到数据库中，即使提交事务后，数据库马上崩溃，在数据库重启时，也必须你能保证通过某种机制恢复数据。

### 事务的传播特性

指的就是当一个事务方法被另一个事务方法调用时，这个事务方法应该**如何进行**。

spring总共给出了7种事务传播特性：

1.**死活不要事务的**

- propagation_never: 没有就非事务执行，有就抛出异常。
- propagation_not_supported: 没有就非事务执行，有就直接挂起，然后非事务执行。

2.**可有可无**

- propagation_supports: 有就用，没有就算了

3.**必须有事务的**

- propagation_requires_new: 有没有都新建事务，如果原来有，就将原来的挂起。**里面的事务，和外面事务是完全隔离的，互不影响的，外面事务不影响里面的事务，里面的事务也不影响外面的事务。**

- propagation_nested: 如果没有，就新建一个事务，如果有，就在当前事务中嵌套其他事务。**外面的事务回滚的时候会影响里面的事务，但是，里面的事务不影响外面的事务。**
- propagation_requered: 如果没有，就新建一个事务，如果有，就加入当前事务。
- propagation_mandatory: 如果没有，就抛出异常，如果有，就使用当前事务。

### 事务的隔离级别

数据库事务的隔离级别**由低到高**有4种，

1. Read uncommitted(**读未提交**)  一个事务可以读取另一个未提交事务的数据，会产生**脏读**。
2. Read committed(**读已提交**) 一个事务要等另一个事务提交后才能读取数据，会产生**不可重复读**。
3. Repeatable read(**可重复**）就是在开始读取数据(事务开启)时，不再允许修改操作。可能会产生**幻读**。
4. Serializable(**可串行化**)  **最高的事务隔离级别**  可以**避免脏读，不可重复读、与幻读**。效率低下 一般不使用。

```yaml
#数据库默认隔离等级知识
Sql Server Oracle ：读已提交 Read committed
Mysql ：可重复 Repeatable read
```

*在事务的**并发操作中**可能会出现**脏读**，**不可重复读**、**幻读**、**事务丢失**。*

**脏读**：读取了未提交的新事物，然后被回滚了

**不可重复读**：读取了提交的新事务，指更新操作

**幻读**：也是读取了提交的新事务，指增删操作

**事务丢失**：

- 回滚丢失

A和B同时在执行一个数据，然后B事务已经提交了，然后A事务回滚了，这样B事务的操作就因A事务回滚而丢失了。

- 提交覆盖丢失

A和B一起执行一个数据，两个同时取到一个数据，然后，B事务首先提交，但是，A事务接下来又提交，这样就覆盖了B事务。

### **事务总结**

- 读未提交：别人改数据的事务尚未提交，我在我的事务中也能读到。
- 读已提交：别人改数据的事务已经提交，我在我的事务中才能读到。
- 可重复读：别人改数据的事务已经提交，我在我的事务中也不去读。
- 串行：我的事务尚未提交，别人就别想改数据。
- 这4种隔离级别，并行性能依次降低，安全性依次提高。

---

## *Spring Boot自动配置原理？*

Spring Boot通过@EnableAutoConfiguration注解开启自动配置，对jar包下的META-INF/spring.factories文件进行扫描，这个文件中包含了可以进行自动配置的类，当满足@Condition注解指定的条件时，便在依赖的支持下进行实例化，注册到Spring容器中。

简单点说以上过程就是：getCandidateConfigurations()方法通过SpringFactoriesLoader加载器加载META-INF/spring.factories文件——>通过这个文件获取到每个配置类的url——>通过这些url将它们封装成Properties对象——>解析内容存于Map<String,List>中——>通过loadFactoryNames传递过来的class名称作为Key从Map中获得该类的配置列表——>getCandidateConfigurations（）方法获取到了配置类并存于List中——>通过selectImports（）方法返回一个自动配置类的全限定名数组。配置类需要在满足@Condition后才能真正的被注册到Spring容器之中。

**<u>如何在SpringBoot启动的时候运行一些特定的代码？</u>**

可以实现接口**ApplicationRunner**或者**CommandLineRunner**的run()方法

## *Spring  MVC 的处理流程？*

1. **DispatcherServlet** 前端处理器处理收到请求
2. 请求 **HandlerMapping** 找出容器中被 @Controler 注解修饰的 Bean 以及被 @RequestMapping 修饰的方法和类 生成 **Handler 和 HandlerInterceptor** 并返回一个**处理器执行链**。
3. 之后 DispatcherServlet **使用 Handler 找到对应的 HandlerApapter**，通过 HandlerApapter 调用 Handler的方法，**将请求参数绑定到方法的形参上**，执行方法处理请求并得到 ModelAndView。
4. 最后 DispatcherServlet 根据使用 ViewResolver 视图解析器对得到的 ModelAndView 逻辑视图进行解析得到 View 物理视图，然后对视图渲染，将数据填充到视图中并返回给客户端。

## *Spring事务失效问题?*

Spring事务：数据库对**事务 <u>@Transactional</u> **的支持

1. 获取连接 Connection con = DriverManager.getConnection()
2. 开启事务con.setAutoCommit(true/false);
3. 执行CRUD
4. 提交事务/回滚事务 con.commit() / con.rollback();
5. 关闭连接 conn.close();

失效原因:

- 数据库引擎不支持事务

Spring事务生效的前提是连接的数据库底层要支持事务 

例如 Mysql默认引擎MyISAM就不支持事务 InnoDB和BDB就支持事务

- 事务方法未被Spring管理

事务方法所在的类没有加载到Spring IOC容器中 没有被加载为Bean 即没有被Spring管理

```java
public class ProductService {
 @Autowired
 private ProductDao productDao;
 
 @Transactional(propagation = Propagation.REQUIRES_NEW)
 public void updateProductStockCountById(Integer stockCount, Long id){
  productDao.updateProductStockCountById(stockCount, id);
 }
}
//ProductService类上没有标注@Service注解，Product的实例没有加载到Spring IOC容器中
```

- 方法没有被public修饰

如果事务所在的方法没有被public修饰，此时Spring的事务会失效  Spring 官方文档规定

- 同一类中方法调用

自身调用问题 同一个类中的两个方法分别为A和B，方法A上没有添加事务注解，方法B上添加了 @Transactional事务注解，方法A调用方法B，则方法B的事务会失效

- 未配置事务管理器

如果在项目中没有配置Spring的事务管理器，即使使用了Spring的事务管理功能，Spring的事务也不会生效。

```java
//未在配置类配置如下代码
@Bean
public PlatformTransactionManager transactionManager(DataSource dataSource) {
 return new DataSourceTransactionManager(dataSource);
}
```

- 不正确的捕获异常

把异常吃了，然后又不抛出来，事务怎么回滚吧！ 

```java
@Service
public class OrderService {
 @Autowired
 private OrderDao orderDao;
 @Autowired
 private ProductDao productDao;
 @Transactional(propagation = Propagation.REQUIRED)
 public void submitOrder(){
  //生成订单
  Order order = new Order();
  long number = Math.abs(new Random().nextInt(500));
  order.setId(number);
  order.setOrderNo("order_" + number);
  orderDao.saveOrder(order);
  //减库存
  this.updateProductStockCountById(1, 1L);
 }
 
 @Transactional(propagation = Propagation.REQUIRED)
 public void updateProductStockCountById(Integer stockCount, Long id){
  try{
   productDao.updateProductStockCountById(stockCount, id);
   int i = 1 / 0;
  }catch(Exception e){
   logger.error("扣减库存异常:", e.getMesaage());
  }}}
```

updateProductStockCountById()方法中使用try-catch代码块捕获了异常，即使updateProductStockCountById()方法内部会抛出异常，但也会被catch代码块捕获到，此时updateProductStockCountById()方法的事务会提交而不会回滚，并且submitOrder()方法的事务会提交而不会回滚，这就造成了Spring事务的回滚失效问题。

- 错误的标注异常类型

```java
@Transactional(propagation = Propagation.REQUIRED)
public void updateProductStockCountById(Integer stockCount, Long id){
 try{
  productDao.updateProductStockCountById(stockCount, id);
 }catch(Exception e){
  logger.error("扣减库存异常:", e.getMesaage());
  throw new Exception("扣减库存异常");
 }
}
```

因为Spring中对于默认回滚的事务异常类型为RuntimeException，上述代码抛出的是Exception异常。即事务回滚会失效

解决方法：手动指定标注的事务异常类型

```java
@Transactional(propagation = Propagation.REQUIRED,rollbackFor = Exception.class)
//Spring事务注解@Transactional中的rollbackFor属性可以指定 Throwable 异常类及其子类。
```

---

---

# 容器集合

Java中集合框架被设计成要满足以下几个目标。

- 该框架必须是高性能的。基本集合（动态数组，链表，树，哈希表）的实现也必须是高效的。
- 该框架允许不同类型的集合，以类似的方式工作，具有高度的互操作性。
- 对一个集合的扩展和适应必须是简单的。

为此，整个集合框架就围绕一组标准接口而设计。你可以直接使用这些接口的标准实现，诸如： **LinkedList**, **HashSet**, 和 **TreeSet** 等,除此之外你也可以通过这些接口实现自己的集合。

![img](https://www.runoob.com/wp-content/uploads/2014/01/2243690-9cd9c896e0d512ed.gif)

从上面的集合框架图可以看到，Java 集合框架主要包括两种类型的容器，**一种是集合（Collection）**，存储一个元素集合，**另一种是图（Map）**，存储键/值对映射。**Collection 接口又有 3 种子类型，List、Set 和 Queue，**再下面是一些抽象类，最后是具体实现类，常用的有 <u>ArrayList、LinkedList、HashSet、LinkedHashSet、HashMap、LinkedHashMap</u> 等等。

集合框架是一个用来代表和操纵集合的统一架构。所有的集合框架都包含如下内容：

- **接口：**是代表集合的抽象数据类型。例如 Collection、List、Set、Map 等。之所以定义多个接口，是为了以不同的方式操作集合对象
- **实现（类）：**是集合接口的具体实现。从本质上讲，它们是可重复使用的数据结构，例如：ArrayList、LinkedList、HashSet、HashMap。
- **算法：**是实现集合接口的对象里的方法执行的一些有用的计算，例如：搜索和排序。这些算法被称为多态，那是因为相同的方法可以在相似的接口上有着不同的实现。

除了集合，该框架也定义了几个 Map 接口和类。Map 里存储的是键/值对。尽管 Map 不是集合，但是它们完全整合在集合中。

**集合框架体系如图所示**：

![img](https://www.runoob.com/wp-content/uploads/2014/01/java-coll-2020-11-16.png)

## 集合接口

集合框架定义了一些接口。本节提供了每个接口的概述：

| 序号 | 接口描述                                                     |
| :--- | :----------------------------------------------------------- |
| 1    | **Collection 接口** ：Collection 是最基本的集合接口，一个 Collection 代表一组 Object，即 Collection 的元素, Java不提供直接继承自Collection的类，只提供继承于的子接口(如List和set)。Collection 接口存储一组不唯一，无序的对象。 |
| 2    | **List 接口：** List接口是一个有序的 Collection，使用此接口能够精确的控制每个元素插入的位置，能够通过索引(元素在List中位置，类似于数组的下标)来访问List中的元素，第一个元素的索引为 0，而且允许有相同的元素。List 接口存储一组不唯一，有序（插入顺序）的对象。 |
| 3    | **Set：** Set 具有与 Collection 完全一样的接口，只是行为上不同，Set 不保存重复的元素。Set 接口存储一组唯一，无序的对象。 |
| 4    | **SortedSet：** 继承于Set保存有序的集合。                    |
| 5    | **Map：** Map 接口存储一组键值对象，提供key（键）到value（值）的映射。 |
| 6    | **Map.Entry：** 描述在一个Map中的一个元素（键/值对）。是一个 Map 的内部接口。 |
| 7    | **SortedMap：** 继承于 Map，使 Key 保持在升序排列。          |
| 8    | **Enumeration**： 这是一个传统的接口和定义的方法，通过它可以枚举（一次获得一个）对象集合中的元素。这个传统接口已被迭代器取代。 |

### Set和List的区别

1. Set 接口实例存储的是无序的，不重复的数据。List 接口实例存储的是有序的，可以重复的元素。
2. Set 检索效率低下，删除和插入效率高，插入和删除不会引起元素位置改变 **<实现类有HashSet,TreeSet>**。
3. List 和数组类似，可以动态增长，根据实际存储的数据的长度自动增长 List 的长度。查找元素效率高，插入删除效率低，因为会引起其他元素位置改变 **<实现类有ArrayList,LinkedList,Vector>** 。

## 集合实现类（集合类）

Java提供了一套实现了Collection接口的标准集合类。其中一些是具体类，这些类可以直接拿来使用，而另外一些是抽象类，提供了接口的部分实现。

标准集合类汇总于下表：

| 序号 | 类描述                                                       |
| :--- | :----------------------------------------------------------- |
| 1    | **AbstractCollection**  实现了大部分的集合接口。             |
| 2    | **AbstractList**  继承于AbstractCollection 并且实现了大部分List接口。 |
| 3    | **AbstractSequentialList**  继承于 AbstractList ，提供了对数据元素的链式访问而不是随机访问。 |
| 4    | [LinkedList](https://www.runoob.com/java/java-linkedlist.html) 该类实现了List接口，允许有null（空）元素。主要用于创建链表数据结构，该类没有同步方法，如果多个线程同时访问一个List，则必须自己实现访问同步，解决方法就是在创建List时候构造一个同步的List。例如：`List list=Collections.synchronizedList(newLinkedList(...));`LinkedList 查找效率低。 |
| 5    | [ArrayList](https://www.runoob.com/java/java-arraylist.html) 该类也是实现了List的接口，实现了可变大小的数组，随机访问和遍历元素时，提供更好的性能。该类也是非同步的,在多线程的情况下不要使用。ArrayList 增长当前长度的50%，插入删除效率低。 |
| 6    | **AbstractSet**  继承于AbstractCollection 并且实现了大部分Set接口。 |
| 7    | [HashSet](https://www.runoob.com/java/java-hashset.html) 该类实现了Set接口，不允许出现重复元素，不保证集合中元素的顺序，允许包含值为null的元素，但最多只能一个。 |
| 8    | LinkedHashSet 具有可预知迭代顺序的 `Set` 接口的哈希表和链接列表实现。 |
| 9    | TreeSet 该类实现了Set接口，可以实现排序等功能。              |
| 10   | **AbstractMap**  实现了大部分的Map接口。                     |
| 11   | [HashMap](https://www.runoob.com/java/java-hashmap.html) HashMap 是一个散列表，它存储的内容是键值对(key-value)映射。 该类实现了Map接口，根据键的HashCode值存储数据，具有很快的访问速度，最多允许一条记录的键为null，不支持线程同步。 |
| 12   | TreeMap 继承了AbstractMap，并且使用一颗树。                  |
| 13   | WeakHashMap 继承AbstractMap类，使用弱密钥的哈希表。          |
| 14   | LinkedHashMap 继承于HashMap，使用元素的自然顺序对元素进行排序. |
| 15   | IdentityHashMap 继承AbstractMap类，比较文档时使用引用相等。  |

在前面的教程中已经讨论通过java.util包中定义的类，如下所示：

| 序号 | 类描述                                                       |
| :--- | :----------------------------------------------------------- |
| 1    | Vector 该类和ArrayList非常相似，但是该类是同步的，可以用在多线程的情况，该类允许设置默认的增长长度，默认扩容方式为原来的2倍。 |
| 2    | Stack 栈是Vector的一个子类，它实现了一个标准的后进先出的栈。 |
| 3    | Dictionary Dictionary 类是一个抽象类，用来存储键/值对，作用和Map类相似。 |
| 4    | Hashtable Hashtable 是 Dictionary(字典) 类的子类，位于 java.util 包中。 |
| 5    | Properties Properties 继承于 Hashtable，表示一个持久的属性集，属性列表中每个键及其对应值都是一个字符串。 |
| 6    | BitSet 一个Bitset类创建一种特殊类型的数组来保存位值。BitSet中数组大小会随需要增加。 |

## 如何使用迭代器？

通常情况下，你会希望遍历一个集合中的元素。例如，显示集合中的每个元素。

一般遍历数组都是采用for循环或者增强for，这两个方法也可以用在集合框架，但是还有一种方法是采用迭代器遍历集合框架，它是一个对象，实现了[Iterator](https://www.runoob.com/java/java-iterator.html) 接口或 ListIterator接口。

迭代器，使你能够通过循环来得到或删除集合的元素。ListIterator 继承了 Iterator，以允许双向遍历列表和修改元素。

| 序号 | 迭代器方法描述                                               |
| :--- | :----------------------------------------------------------- |
| 1    | [使用 Java Iterator](https://www.runoob.com/java/java-iterator.html) 这里通过实例列出 Iterator 和 ListIterator 接口提供的所有方法。 |

### 遍历 ArrayList

```java
//实例
import java.util.*;
 
public class Test{
 public static void main(String[] args) {
     List<String> list=new ArrayList<String>();
     list.add("Hello");
     list.add("World");
     list.add("HAHAHAHA");
     //第一种遍历方法使用 For-Each 遍历 List
     for (String str : list) {            //也可以改写 for(int i=0;i<list.size();i++) 这种形式
        System.out.println(str);
     }
 
     //第二种遍历，把链表变为数组相关的内容进行遍历
     String[] strArray=new String[list.size()];
     list.toArray(strArray);
     for(int i=0;i<strArray.length;i++) //这里也可以改写为  for(String str:strArray) 这种形式
     {
        System.out.println(strArray[i]);
     }
     
    //第三种遍历 使用迭代器进行相关遍历
     
     Iterator<String> ite=list.iterator();
     while(ite.hasNext())//判断下一个元素之后有值
     {
         System.out.println(ite.next());
     }
 }
}
//解析：
//三种方法都是用来遍历ArrayList集合，第三种方法是采用迭代器的方法，该方法可以不用担心在遍历的过程中会超出集合的长度。
```

### 遍历 Map

```java
//实例
import java.util.*;
 
public class Test{
     public static void main(String[] args) {
      Map<String, String> map = new HashMap<String, String>();
      map.put("1", "value1");
      map.put("2", "value2");
      map.put("3", "value3");
      
      //第一种：普遍使用，二次取值
      System.out.println("通过Map.keySet遍历key和value：");
      for (String key : map.keySet()) {
       System.out.println("key= "+ key + " and value= " + map.get(key));
      }
      
      //第二种
      System.out.println("通过Map.entrySet使用iterator遍历key和value：");
      Iterator<Map.Entry<String, String>> it = map.entrySet().iterator();
      while (it.hasNext()) {
       Map.Entry<String, String> entry = it.next();
       System.out.println("key= " + entry.getKey() + " and value= " + entry.getValue());
      }
      
      //第三种：推荐，尤其是容量大时
      System.out.println("通过Map.entrySet遍历key和value");
      for (Map.Entry<String, String> entry : map.entrySet()) {
       System.out.println("key= " + entry.getKey() + " and value= " + entry.getValue());
      }
    
      //第四种
      System.out.println("通过Map.values()遍历所有的value，但不能遍历key");
      for (String v : map.values()) {
       System.out.println("value= " + v);
      }
     }
}
```

## 如何使用比较器？

TreeSet和TreeMap的按照排序顺序来存储元素. 然而，这是通过比较器来精确定义按照什么样的排序顺序。

这个接口可以让我们以不同的方式来排序一个集合。

| 序号 | 比较器方法描述                                               |
| :--- | :----------------------------------------------------------- |
| 1    | 使用 Java Comparator 这里通过实例列出Comparator接口提供的所有方法 |

## 总结

Java集合框架为程序员提供了预先包装的数据结构和算法来操纵他们。

集合是一个对象，可容纳其他对象的引用。集合接口声明对每一种类型的集合可以执行的操作。

集合框架的类和接口均在java.util包中。

任何对象加入集合类后，自动转变为Object类型，所以在取出的时候，需要进行强制类型转换。

## ArrayList

**ArrayList 继承了 AbstractList.class ，并实现了 List 接口。**<u>非线程安全 动态数组结构 随机访问get/set快 自动扩容1.5倍</u>

![img](https://www.runoob.com/wp-content/uploads/2020/06/ArrayList-1-768x406-1.png)

ArrayList 类是一个可以动态修改的数组，与普通数组的区别就是它是没有固定大小的限制，我们可以添加或删除元素。

```java
//E: 泛型数据类型，用于设置 objectName 的数据类型，只能为引用数据类型,例如一些基本数据类型的包装类和一些常用的引用类型对象。
import java.util.ArrayList; // 引入 ArrayList 类
ArrayList<E> objectName =new ArrayList<>();　 // 初始化
```

## LinkedList

链表（Linked list）是一种常见的基础数据结构，是一种线性表，但是并不会按线性的顺序存储数据，而是在每一个节点里存到下一个节点的地址。

```java
// 引入 LinkedList 类
import java.util.LinkedList; 
LinkedList<E> list = new LinkedList<E>();   // 普通创建方法
//或者
LinkedList<E> list = new LinkedList(Collection<? extends E> c); // 使用集合创建链表
```

<u>非线程安全 双向链表结构 由于移动指针操作 所以插入删除(add/remove)快</u>

与 ArrayList 相比，LinkedList 的增加和删除的操作效率更高，而查找和修改的操作效率较低。

![img](https://www.runoob.com/wp-content/uploads/2020/06/linkedlist-2020-11-16.png)

1. LinkedList 继承了 AbstractSequentialList 类。
2. LinkedList 实现了 Queue 接口，可作为队列使用。
3. LinkedList 实现了 List 接口，可进行列表的相关操作。
4. LinkedList 实现了 Deque 接口，可作为队列使用。
5. LinkedList 实现了 Cloneable 接口，可实现克隆。
6. LinkedList 实现了 java.io.Serializable 接口，即可支持序列化，能通过序列化去传输。

## HashSet

**Hash算法** Hashmap(数组+链表)实现

 **非线程安全** **非有序 ** **元素可以为NULL  但只能有一个** 

HashMap默认初始化容量：16 必须是2的次幂 数组容量达到了3/4(0.75)开始扩容2倍

HashSet 是无序的，即不会记录插入的顺序。

实现对象相等需要重写hashcode()和equals()方法 对象相等必须具有相同散列码

**存取 查找 删除 性能好**

![img](https://www.runoob.com/wp-content/uploads/2020/07/java-hashset-hierarchy.png)

## HashMap

HashMap 是一个散列(hash)表，它存储的内容是键值对(key-value)映射。

JDK1.8以后的HashMap 当链表长度大于阈值（默认为8）时 会将链表转化为红黑树

HashMap 实现了 Map 接口，根据键的 HashCode 值存储数据，具有很快的访问速度，**最多允许一条记录的键为 null**，非线程安全。

HashMap 是无序的，即不会记录插入的顺序。

HashMap 继承于AbstractMap，实现了 Map、Cloneable、java.io.Serializable 接口。![img](https://www.runoob.com/wp-content/uploads/2020/07/WV9wXLl.png)

```java
HashMap<Integer, String> Sites = new HashMap<Integer, String>();
```

## Iterator（迭代器）

Java Iterator（迭代器）不是一个集合，它是一种用于访问集合的方法接口，可用于迭代 [ArrayList](https://www.runoob.com/java/java-arraylist.html) 和 [HashSet](https://www.runoob.com/java/java-hashset.html) 等集合。

![img](https://www.runoob.com/wp-content/uploads/2020/07/ListIterator-Class-Diagram.jpg)

迭代器 it 的两个基本操作是 next 、hasNext 和 remove。

调用 it.next() 会返回迭代器的下一个元素，并且更新迭代器的状态。

调用 it.hasNext() 用于检测集合中是否还有元素。

调用 it.remove() 将迭代器返回的元素删除。

```java
// 引入 ArrayList 和 Iterator 类
import java.util.ArrayList;
import java.util.Iterator;

public class RunoobTest {
    public static void main(String[] args) {
        // 创建集合
        ArrayList<String> sites = new ArrayList<String>();
        sites.add("Google");
        sites.add("Runoob");
        sites.add("Taobao");
        sites.add("Zhihu");
        // 获取迭代器
        Iterator<String> it = sites.iterator();

        // 输出集合中的所有元素
        while(it.hasNext()) {
            System.out.println(it.next());
        }
    }
}
```

## Serializable序列化

Java 提供了一种对象序列化的机制，该机制中，一个对象可以被表示为一个字节序列，该字节序列包括该对象的数据、有关对象的类型的信息和存储在对象中数据的类型。

将序列化对象写入文件之后，可以从文件中读取出来，并且对它进行反序列化，也就是说，对象的类型信息、对象的数据，还有对象中的数据类型可以用来在内存中新建对象。

整个过程都是 Java 虚拟机（JVM）独立的，也就是说，在一个平台上序列化的对象可以在另一个完全不同的平台上反序列化该对象。

请注意，一个类的对象要想序列化成功，必须满足两个条件：

1. 该类必须实现 java.io.Serializable 接口。
2. 该类的所有属性必须是可序列化的。如果有一个属性不是可序列化的，则该属性必须注明是短暂的。

```java
public class Employee implements java.io.Serializable
{
   public String name;
   public String address;
   public transient int SSN;
   public int number;
   public void mailCheck()
   {
      System.out.println("Mailing a check to " + name
                           + " " + address);
   }
}
```

序列化对象:

```java
import java.io.*;
 
public class SerializeDemo
{
   public static void main(String [] args)
   {
      Employee e = new Employee();
      e.name = "Reyan Ali";
      e.address = "Phokka Kuan, Ambehta Peer";
      e.SSN = 11122333;
      e.number = 101;
      try
      {
         FileOutputStream fileOut =
         new FileOutputStream("/tmp/employee.ser");
         ObjectOutputStream out = new ObjectOutputStream(fileOut);
         out.writeObject(e);
         out.close();
         fileOut.close();
         System.out.printf("Serialized data is saved in /tmp/employee.ser");
      }catch(IOException i)
      {
          i.printStackTrace();
      }
   }
}
```

反序列化对象:

```java
import java.io.*;
 
public class DeserializeDemo
{
   public static void main(String [] args)
   {
      Employee e = null;
      try
      {
         FileInputStream fileIn = new FileInputStream("/tmp/employee.ser");
         ObjectInputStream in = new ObjectInputStream(fileIn);
         e = (Employee) in.readObject();
         in.close();
         fileIn.close();
      }catch(IOException i)
      {
         i.printStackTrace();
         return;
      }catch(ClassNotFoundException c)
      {
         System.out.println("Employee class not found");
         c.printStackTrace();
         return;
      }
      System.out.println("Deserialized Employee...");
      System.out.println("Name: " + e.name);
      System.out.println("Address: " + e.address);
      System.out.println("SSN: " + e.SSN);
      System.out.println("Number: " + e.number);
    }
}
Deserialized Employee...
Name: Reyan Ali
Address:Phokka Kuan, Ambehta Peer
SSN: 0
Number:101
```

这里要注意以下要点：

readObject() 方法中的 try/catch代码块尝试捕获 ClassNotFoundException 异常。对于 JVM 可以反序列化对象，它必须是能够找到字节码的类。如果JVM在反序列化对象的过程中找不到该类，则抛出一个 ClassNotFoundException 异常。

注意，readObject() 方法的返回值被转化成 Employee 引用。

当对象被序列化时，属性 SSN 的值为 111222333，但是因为该属性是短暂的，该值没有被发送到输出流。所以反序列化后 Employee 对象的 SSN 属性为 0。



























































## Collection interface <extends Iterable>

- **单列**数据容器

- 实现了**collections**工具类以及**iterator**迭代器
- **Comparable**和**Comparator**对象排序接口

### List<E><interface extends Collection>

**<u>对付顺序的好帮手</u>**

- 拥有专属**Listiterator**迭代器
- 顺序存储 存放时顺序保持一致 可重复

1. **Vector** 线程安全 效率低  底层结构动态数组同Arraylist但是扩容是2倍
2. **ArrayList<典型实现>** 非线程安全 动态数组结构 随机访问get/set快 自动扩容1.5倍
3. **LinkedList** 非线程安全 双向链表结构 由于移动指针操作 所以插入删除(add/remove)快

---

### Set<E><interface extends Collection>

**<u>注重独一无二的性质</u>**

- 无顺序 不可重复元素 否则插入失败
- 判断对象相等使用`equals()`方法不使用 `==`

1.**HashSet<典型实现>**  <Class implements Set>

HashMap默认初始化容量：16 必须是2的次幂 数组容量达到了3/4(0.75)开始扩容2倍

**Hash算法** Hashmap(数组+链表)实现  **非线程安全** **非有序** **元素可以为NULL但只能有一个** 

实现对象相等需要重写hashcode()和equals()方法 对象相等必须具有相同散列码

存取 查找 删除 性能好

- LinkedHashSet   <class implements Set>

<u>**HashSet的子类**</u> 双向链表数据结构和哈希表 插入性能略低于父类 插入时遍历顺序保持一致

2.SortedSet 接口<interface extends Set>  

- 唯一实现类**TreeSet**<extends AbstractSet> 红黑树数据存储结构 默认自然排序(元素大小排序)或者定制排序 遍历保持由小到大 无重复 不允许放入NULL值

---

### Queue

**<u>实现排队功能的叫号机</u>**

按特定的排队规则来确定先后顺序 存储的元素是**有序**的 **可重复的** 

- queue 单向队列 
- deque 双向队列 ArrayDeque顺序表实现   LinkedList链表实现
- PriorityQueue 非线程安全 非NULL 实现了 `Serializable`

### HashSet插入时步骤？

1.先得到对象的hashcode值

2.判断hashcode值是否相等？

3.再比较对象实现的equals()方法

equals和hashcode分两种情况

- equals：false hashcode：ture 保存元素 数组已有位置通过链表链接
- equals：ture hashcode：false 添加元素成功 存储不同位置

### 如何将ArrayList变成线程安全的？

调用Collections工具类中的 static synchronizedList(List list)方法

### ArrayList如何去重？

- 使用HashSet去重 但是会影响元素原有位置 也可以使用LinkedHashSet保持元素原来的顺序

  ```java
  HashSet<String> objects = new HashSet<>(arr1);
  //或LinkedHashSet<Integer> hashSet = new LinkedHashSet<>(arr1);
  ```

- stream()的distinct()方法返回一个由不同数据组成的流 通过对象的equals()方法进行比较 

  ```java
  List<Integer> listWithoutDuplicates = numbersList.stream().distinct().collect(Collectors.toList());
  ```

- List的contains()循环遍历,重新排序,只添加一次数据,避免重复

  ```java
  for (String str : list) {
      if (!result.contains(str)) {
          result.add(str);
      }}
  ```

- 双重for循环去重

  ```java
  for (int i = 0; i < list.size(); i++) { 
      for (int j = 0; j < list.size(); j++) { 
          if(i!=j&&list.get(i)==list.get(j)) { 
              list.remove(list.get(j)); 
       } } }
  ```


---

## Map <interface>

**用 key 来搜索的专家**

- **双列**数据
- 保存具有映射关系的**K-V集合** key和value皆可以是任何类型
- 不允许重复 同一map对象对应对象必须重写hashcode和equlas方法
- JDK1.8以后的HashMap 当链表长度大于阈值（默认为8）时 会将链表转化为红黑树

1.**HashMap<典型实现>** hash散列算法实现 非线程安全 访问快 无序 以存储NULL的k和v 

2.LinkedHashMap 有序按添加顺序  访问慢 双向指针操作 非线程安全

3.TreeMap 按照添加k-v对进行排序 实现排序遍历 自然排序or定制排序 底层红黑树

4.Hashtable 线程安全的  效率低 不能存储null的key和value

5.Properties 常用来处理配置文件 key和value都是String类型 

---

## 枚举<extends ENUM>

特征：

- 无法继承 构造方法为私有 其他与常规类相同
- 不允许使用`=`复制给枚举常量
- enum可以有任意普通 静态 抽象 构造方法
- enum可以实现接口 

 继承自`java.lang.Enum`提供的常用方法  Enum 实现了**Serializable**和**Comparable**接口

- `values()` 数组顺序返回获取枚举类型的成员
- `ordinal()`方法可以找到每个枚举常量的索引，就像数组索引一样。
- `valueOf()`方法返回指定字符串值的枚举常量。

- `name()` 返回实例名
- `getDeclaringClass()` 返回实例所属的enum类型
- `equals()` 判断是否同一对象也可以使用`==`

工具类：

**Enumset**:枚举类型Set高效实现 要求放入它的枚举常量必须属于同一枚举类型

**EnumMap**:枚举类型Map高效实现 只接受同一枚举类型的实例作为键值 使用数组来存放与枚举类型对应的值

---

## 泛型 <E T K V N ?>

泛型是 JDK 5 中引入的一个新特性, 泛型提供了编译时类型安全检测机制，该机制允许程序员在编译时检测到非法的类型。

泛型的本质是参数化类型，也就是说所操作的数据类型被指定为一个参数。

```xml
假定我们有这样一个需求：写一个排序方法，能够对整型数组、字符串数组甚至其他任何类型的数组进行排序，该如何实现？
答案是可以使用 Java 泛型。
使用 Java 泛型的概念，我们可以写一个泛型方法来对一个对象数组排序。然后，调用该泛型方法来对整型数组、浮点数数组、字符串数组等进行排序。
```

**泛型类型在逻辑上看以看成是多个不同的类型，实际上都是相同的基本类型。**

- **E** - Element (在集合中使用，因为集合中存放的是元素)
- **T** - Type（Java 类）
- **K** - Key（键）
- **V** - Value（值）
- **N** - Number（数值类型）
- **？** - 表示不确定的 java 类型

---

## 线程安全的容器有哪些？

**同步容器类：<synchronized>**

- vector 线程安全的list 几乎不用

- HashTable 线程安全的Map 几乎不用

**并发容器**：

- ConcurrentHashMap: 使用较多 效率高(分段/CAS)再加synchronized保证同步操作 手动实现并发安全 用于并发几率低场景 
- CopyOnWriteArrayList：写时复制 常用于读多写少的并发环境
- CopyOnWriteArraySet：写时复制 常用于读多写少的并发环境

**Queue队列：**

- ConcurrentLinkedQueue **非阻塞**的方式实现的**基于链接节点**的**无界**的线程安全队列，性能非常好。
- ArrayBlockingQueue：基于**数组**的**有界阻塞队列**
- LinkedBlockingQueue：基于**链表**的**有界阻塞队列**
- PriorityBlockingQueue：**支持优先级**的**无界阻塞队列** 默认情况下元素自然升序排序

- DelayQueue： 延时获取元素的无界阻塞队列
- SynchronousQueue ：不存储元素的阻塞队列。每个put操作必须等待一个take操作，否则不能继续添加元素。内部其实没有任何一个元素，容量是0

**Deque：双向对列 允许在队列头和尾部进行入队出队操作**

- ArrayDeque:基于数组的双向非阻塞队列。
- LinkedBlockingDeque:基于链表的双向阻塞队列。

**Sorted容器：**

- ConcurrentSkipListMap：是TreeMap的线程安全版本
- ConcurrentSkipListSet：是TreeSet的线程安全版本

# 多线程与并发

## 多线程编程

多线程能满足程序员编写高效率的程序来达到充分利用 CPU 的目的。

Java 给多线程编程提供了内置的支持。 一条线程指的是进程中一个单一顺序的控制流，一个进程中可以并发多个线程，每条线程并行执行不同的任务。

多线程是多任务的一种特别的形式，但多线程使用了更小的资源开销。

## 进程

**执行程序的一次执行过程 也指正在运行的程序实体**

包括这个运行的程序中占据的所有系统资源，比如说CPU（寄存器），IO,内存，网络资源等。

同样一个程序，同一时刻被两次运行了，那么他们就是两个独立的进程。

一个操作系统中可以有多个进程，一个进程可以开启多个线程，其中有一个主线程来调用本进程中的其他线程。

## [线程](https://blog.csdn.net/qq_35598736/article/details/108431422?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522165984936416781432921249%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=165984936416781432921249&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~top_positive~default-2-108431422-null-null.142^v39^pc_rank_v36,185^v2^control&utm_term=%E5%A4%9A%E7%BA%BF%E7%A8%8B&spm=1018.2226.3001.4187)

JVM 执行任务的**运算调度的最小单位** ，它被**包含在进程之中**，一条线程指的是**进程中一个单一顺序的控制流**。

**多线程**可以让同一个进程同时**并发**处理多个任务

JVM中进程的六种状态 这些状态对应 **Thread.State** 枚举类中的状态 `<java.lang.Thread.State>`

1. **`NEW`**  **创建状态**

2. **`RUNNABLE`** **可运行状态**  运行 Thread 的 start 方法后 线程进入可运行状态

   可运行状态线程并不能马上运行   而是先进入**READY就绪状态**等待线程调度 在获取 CPU 后才能进入**RUNNING运行状态**  运行状态可以随着不同条件转换成除 NEW 以外的其他状态

3. **`BLOCKED`**  **阻塞状态** 运行进程进入 synchronized 同步块或同步方法时 获取锁失败 会进入BLOCKED状态 获取到锁后 会从BLOCKED状态恢复到就绪RUNNABLE状态 

4. **`WAITING` ** **等待状态**  wait()操作之后会释放锁 等待其他线程唤醒 获取到锁才能进入可运行状态

5. **`TIMED_WAITING`**  **有时间的等待 **sleep()或者join()操作先进入阻塞状态不会释放锁 时间结束或者等其他线程结束之前一直是属于等待状态

6. **`TERMINATED` ** **线程运行完成结束状态** 或者有异常发生 线程会进入死亡Dead状态

![多线程状态图](https://img-blog.csdnimg.cn/db36e894a0a843c6a36ca5a76cb3af2d.png)

![](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9wNi1qdWVqaW4uYnl0ZWltZy5jb20vdG9zLWNuLWktazN1MWZicGZjcC9lNGI3YTY3YTE2NDQ0NWYzYWE3ZjA1ZWVkNDAyM2I3OH50cGx2LWszdTFmYnBmY3Atem9vbS0xLmltYWdl?x-oss-process=image/format,png)

![对应枚举类状态](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9wNi1qdWVqaW4uYnl0ZWltZy5jb20vdG9zLWNuLWktazN1MWZicGZjcC8zOTlhNzYzODU5MzM0ZDYwOGYzZGMzMDA0NTgzODVlZX50cGx2LWszdTFmYnBmY3Atem9vbS0xLmltYWdl?x-oss-process=image/format,png)

## 并发与并行

**并发（Concurrent）**：一个时间段中有几个程序都处于已启动运行到运行完毕之间，且这几个程序都是在同一个处理机上运行。
同一时刻只能有一条指令执行，但多个进程指令被**快速的轮换执行**，使得在宏观上具有多个进程同时执行的效果，但在微观上并不是同时执行的，只是把**时间分成若干段，使多个进程快速交替的执行**。

**并行（Parallel）：**当系统有一个以上CPU时，当一个CPU执行一个进程时，另一个CPU可以执行另一个进程，两个进程互不抢占CPU资源，可以同时进行**真正的在同一时刻运行**，这种方式我们称之为并行 。

其实决定并行的因素不是CPU的数量，而是**CPU的核心数量**，比如一个CPU多个核也可以并行。

## 进程与线程的关系

- 进程是操作系统资源分配的基本单位，而线程是CPU的基本调度单位
- 一个进程由一个或多个线程(多线程)组成
- 进程之间相互独立，而线程共享所在进程的地址空间和其它资源(自己的栈和栈指针，程序计数器等寄存器)。
- 一个进程中可以并发多个线程，每条线程并行执行不同的任务
- 线程上下文切换比进程上下文切换要快得多

## 多线程的多种创建方式

### 1.继承Thread类 

- 自定义线程类继承 Thread类

- 重写 run() 方法 编写线程执行体
-  创建线程对象 调用 start() 方法启动线程

```java
public class Demo extends Thread {
    @Override
    public void run() {
        for (int i = 0; i < 20; i++) {
            System.out.println("111111111111111");
        }}
    public static void main(String[] args) {
        for (int i = 0; i < 100; i++) {
            Demo demo = new Demo();
            demo.start();  //一般都是调用start方法
            System.out.println("22222222222222222");
     }}}
```

### 2.实现Runnable接口 

- 定义MyRunnable类实现 Runnable 接口
- 实现 run() 方法,编写线程执行体
- 创建线程对象，调用 start() 方法启动线程

```java
//推荐使用 避免单继承的局限性，灵活方便，方便同一个对象被多个线程使用
public class MyRunnable implements Runnable {
    @Override
    public void run() {
        for (int i = 0; i < 20; i++) {
            System.out.println("111111111111111");
        }}
    public static void main(String[] args) {
        for (int i = 0; i < 100; i++) {
            MyRunnable myRunnable = new MyRunnable();
            new Thread(myRunnable).start();
            System.out.println("22222222222222222");
        }}}
```

```java
//龟兔赛跑实例
public class Race implements Runnable {
    private static String winner;
    @Override
    public void run() {
        for (int i = 0; i <= 100; i++) {
            if (Thread.currentThread().getName().equals("兔子")) {
                try {
                    Thread.sleep(10);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
            boolean gameOver = gameOver(i);
            if (gameOver) {
                break;
            }            System.out.println(Thread.currentThread().getName() + "--->跑了" + i);
        }}
    private boolean gameOver(int i) {
        if (winner != null) {
            return true;
        } else {
            if (i >= 100) {
                winner = Thread.currentThread().getName();
                System.out.println(winner + "赢得了比赛");
                return true;
            }
        }
        return false;
    }
    public static void main(String[] args) {
        Race race = new Race();
        new Thread(race, "兔子").start();
        new Thread(race, "乌龟").start();
    }}
```

### 3.实现Callable接口

- 实现Callable接口，需要返回值类型
- 重写call方法，需要抛出异常
- 创建目标对象
- 创建执行服务：`ExecutorService executorService=Executors.newFixedThreadPool();`
- 提交执行：`Future submit = executorService.submit(t1);`
- 获取结果：`boolean r1 = result.get()`
- 关闭服务: `ser.shutdownNow();`

```java
//实例Callable接口了解即可
public class MTImplementsCallable implements Callable {
    @Override
    public Object call() throws Exception {
        //执行线程业务的方法
        for (int i = 0; i < 10; i++) {
            //返回正在执行的线程实例
            Thread thread = Thread.currentThread();
            //getName（）获取当前线程实例的名称
            System.out.println(thread.getName()+"执行打印"+i);
        }
        //获取随机数
        UUID uuid = UUID.randomUUID();
        System.out.println("随机数字符串为："+uuid);
        System.out.println(1/0);
        return uuid;
    }}
```

### 4.使用线程池

```java
public class MTPool implements Runnable {
    @Override
    public void run() {
        //执行线程业务的方法
        for (int i = 0; i < 10; i++) {
            //返回正在执行的线程实例
            Thread thread = Thread.currentThread();
            //getName（）获取当前线程实例的名称
            System.out.println(thread.getName()+"执行打印"+i);
        }}}
//实例化线程类
MTPool mtPool =new MTPool();
//使用Executors创建固定长度为4的线程池
ExecutorService executorService = Executors.newFixedThreadPool(4);
//调用execute启动线程
executorService.execute(mtPool);
```

### 区别

runnable和callable都是执行多线程 方法名分别为run() 和call()

runnable没有返回值 无法获取线程业务方法执行方法 callable正好相反

Runnable方法没有抛出异常 而Callable有异常处理，并且获取异常

继承thread存在局限性 因为一个类只能继承一个父类 故不能用一个实例建立多个线程 只能共享Thread类的static变量

而一个类可以实现多个接口 例如runnable接口使用同一实例创建的多线程变量也是共享的 故实现接口更适合与资源共享

```java
public class SellTicketExtendsThread extends Thread {
    //定义总票数
    private int ticketNum = 20;
    //卖票人姓名
    private String  name;
    /**
     * 构造方法
     * @param name
     */
public SellTicketExtendsThread(String name) {
        this.name = name;
    }
    @Override
public void run() {
         while(ticketNum>0){
             System.out.println(name+"正在卖票，剩余"+(--ticketNum)+"张");
         }}}
public class SellTicketImplementsRunnable  implements Runnable{
    //定义总票数
    private int ticketNum = 20;
    @Override
    public void run() {
        while(ticketNum>0){
            System.out.println(Thread.currentThread().getName()+"正在卖票，剩余"+(--ticketNum)+"张");
        }}}
class Test {
    public static void main(String[] args) {
      /*  SellTicketExtendsThread sellTicketExtendsThread =new SellTicketExtendsThread("马云");
        sellTicketExtendsThread.start();
       *//* sellTicketExtendsThread.start();
        sellTicketExtendsThread.start();*//*
        SellTicketExtendsThread sellTicketExtendsThread1 =new SellTicketExtendsThread("马化腾");
        sellTicketExtendsThread1.start();
        SellTicketExtendsThread sellTicketExtendsThread2 =new SellTicketExtendsThread("刘强东");
        sellTicketExtendsThread2.start();*/
        SellTicketImplementsRunnable sellTicketImplementsRunnable =new SellTicketImplementsRunnable();
        new Thread(sellTicketImplementsRunnable,"马云").start();
        new Thread(sellTicketImplementsRunnable,"马化腾").start();
        new Thread(sellTicketImplementsRunnable,"刘强东").start();
    }}
```

```java 
//多线程匿名(Anonymous)内部类用法
public class Test8_7 {
        public static void main(String[] args) {
            //继承Thread启动线程
            new Thread(){
                @Override
                public void run() {
                    for (int i = 0; i < 10; i++) {
                        //返回正在执行的线程实例
                        Thread thread = Thread.currentThread();
                        //getName（）获取当前线程实例的名称
                        System.out.println(thread.getName()+"执行打印"+i);
                    }}}.start();
            System.out.println("-------------------------------------");
            //实现Runnable
            new Thread(new Runnable() {
                @Override
                public void run() {
                    for (int i = 0; i < 10; i++) {
                        //返回正在执行的线程实例
                        Thread thread = Thread.currentThread();
                        //getName（）获取当前线程实例的名称
                        System.out.println(thread.getName()+"执行打印"+i);
                    }}}).start();
            System.out.println("-------------------------------------");
            //实现Callable
            new Thread(new FutureTask<String>(
                    new Callable<String>() {
                        @Override
                        public String call() throws Exception {
                            for (int i = 0; i < 10; i++) {
                                //返回正在执行的线程实例
                                Thread thread = Thread.currentThread();
                                //getName（）获取当前线程实例的名称
                                System.out.println(thread.getName()+"执行打印"+i);}
                            return null;
                        }})).start();}}
```

## 多线程有哪些方法？

- start()：启动当前线程并调用线程的run()方法
- run() ：线程执行业务的方法
- currentThread():静态方法 返回当前代码执行的线程象的引用
- getName():获取当前线程的名字
- setName():设置当前线程的名字
- getPriority()：获取线程优先级 默认是5如果不手动指定 那么线程优先级具有继承性
- setpriority()：设置线程优先级 cpu会尽量执行优先级高的线程

继承性：相互启动的两个线程具有同样优先级

`MAX_PRIORITY:10`
`MIN_PRIORITY:1`
`NORM_PRIORITY:5`

- interrupt()： 通知线程中断 具体是否中断情况由被通知的线程自己处理

1.如果此时线程被阻塞状态(sleep wait join等) 立刻退出被阻塞状态并且抛出InterruptedException异常

2.如果线程处于正常活动状态 那么线程中断标志设置为ture 仅此而已 被设置中断标志线程继续正常运行 不受影响

即 ：interrupt()并不能真正中断线程 需要被通知的线程同意配合才行

- join() 等待其他线程终止 

在当前线程调用其他线程的join方法时 当前线程进入阻塞状态 直到其他线程运行结束 当前线程才由阻塞状态转换为就绪状态

- yieId() 暂停当前正执行线程 把执行机会给相同或者优先级级别更高的线程
- sleep() 使线程转入到阻塞状态

millis参数设置睡眠时间 默认以毫秒为单位 当睡眠结束线程自动进入Runnable可运行状态

- ~~stop() 强制停止线程 被废弃方法已过时~~
- isAlive():判断当前线程是否还存活

## 锁

### 同步锁

多个取款机 对应**多个锁**里面的现金互不影响 在多个取款机同时取钱也没有影响 每个来取钱的人对应的都是**线程 **在大厅等待取钱对应**线程状态**  轮到取钱者进入取款机锁上门对应**线程获得锁** 完成对应业务取钱后出门对应**线程释放** 下一个取钱者继续竞争锁 银行工作人员对应一个线程发现取款机里面现金不足通知上级 就会对取款机加钱**调用notifyAll方法<唤醒waitSet中所有的线程>** 取钱服务暂停 取钱大厅所有(**调用wait方法**)线程进入堵塞状态

而需要银行工作人员对取款机完成加钱操作也就是需要**工作人员线程获取到取款机锁**后加钱操作完成后通知大厅所以人来取钱对应的也就是上述的**调用notifyAll方法** 

如果取款机里面的人是取款人对应当前获取到锁的不是工作人员线程 因为取款机没钱了则需要释放锁 进入大厅堵塞状态(**调用wait方法**)

大堂里等待的人都来竞争锁，谁获取到谁进入继续取钱

### ReentrantLock

 ReentrantLock是可重入锁： 一个线程获取到对象的锁后，执行方法内部在需要获取锁的时候是可以获取到的。synchronized 也是可重入锁。

优点：

1. 支持获取锁的超时时间
2. 获取锁时可被打断
3. 可设为公平锁
4. 可以有不同的条件变量，即有多个waitSet，可以指定唤醒

### 死锁

是指多个进程在运行过程中因争夺资源而造成的一种僵局，当进程处于这种僵持状态时，若无外力作用，它们都将无法再向前推进。

例如老王 小李两个进程在运行到某一时刻时 都想获取酒和故事两种资源而两人分别持有酒和故事中一个资源 都想要对方手里的

```java
//example
static Beer beer = new Beer();
static Story story = new Story();
public static void main(String[] args) {
    new Thread(() ->{
        synchronized (beer){
            log.info("我有酒，给我故事");
            try {
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            synchronized (story){
                log.info("小王开始喝酒讲故事");
            }
        }
    },"小王").start();
    new Thread(() ->{
        synchronized (story){
            log.info("我有故事，给我酒");
            try {
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            synchronized (beer){
                log.info("老王开始喝酒讲故事");
            }
        }
    },"老王").start();
}
class Beer {
}
class Story{
}
```

如何避免死锁：

1. 避免一个线程同时获取多个锁
2. 避免一个线程在锁内同时占用多个资源，尽量保证每个锁只占用一个资源
3. 尝试使用超时解锁，从而规避无限期等待

### 内存模型<JMM>

1. 原子性 保证指令不会受到上下文切换的影响

   同步锁的synchronized代码块就是保证了原子性，就是**一段代码是一个整体**，原子性保证了线程安全，不会受到上下文切换的影响。

2. 可见性 保证指令不会受到cpu缓存的影响

   ```java
   static boolean run = true;
   public static void main(String[] args) throws InterruptedException {
       Thread t = new Thread(() -> {
           while (run) {
               // ....
           }});
       t.start();
       Thread.sleep(1000);
      // 线程t不会如预想的停下来
       run = false; }
   //线程有自己的工作缓存，当主线程修改了变量并同步到主内存时，t线程没有读取到，所以程序停不下来
   ```

   ![线程有自己的工作缓存，当主线程修改了变量并同步到主内存时，t线程没有读取到，所以程序停不下来](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9wMS1qdWVqaW4uYnl0ZWltZy5jb20vdG9zLWNuLWktazN1MWZicGZjcC9kODg4MDA0ZTBjMmM0N2JhYjExYjhhNjdiZjc4Zjg4ZH50cGx2LWszdTFmYnBmY3Atem9vbS0xLmltYWdl?x-oss-process=image/format,png)

3. 有序性 保证指令不会受并行优化的影响

   JVM在不影响程序正确性的情况下可能会调整语句的执行顺序，该情况也称为 **指令重排序** 。

### **Volatile**

volatile关键字解决了可见性和有序性，不能解决原子性，volatile通过**内存屏障<读/写屏障>**来实现的。

应用场景：一个线程读取变量，另外的线程操作变量，加了该关键字后保证写变量后，读变量的线程可以及时感知。

### **CAS**<compare and swap>

**轻量级 乐观锁的一种实现方式**

线程读数据时不加锁，在写回数据前，比较原值是否修改，未被其他线程修改则写回，若已被修改，则重新执行读取流程。

这是一种**乐观**策略，认为**并发操作**并不总会发生。

比较并写回的操作是通过操作系统原语实现的，保证执行过程中不会被中断，即不使用同步锁也可以保证操作的原子性。

```java
private AtomicInteger balance;
// 模拟cas的具体操作
@Override
public void withdraw(Integer amount) {
    while (true) {
        // 获取当前值
        int pre = balance.get();
        // 进行操作后得到新值
        int next = pre - amount;
        // 比较并设置成功 则中断 否则自旋重试
        if (balance.compareAndSet(pre, next)) {
            break;
        }}}
```

无锁的效率是要高于之前的锁的，由于无锁不会涉及线程的上下文切换

**cas是乐观锁的思想        sychronized是悲观锁的思想**

### 悲观锁与乐观锁？

悲观锁：在对数据进行修改前，先对数据进行加锁。之所以叫悲观锁，就是因为悲观的认为数据被并发修改的概率大，所需需要先加锁再操作

乐观锁：相对于悲观锁而言，乐观锁乐观的认为被修改数据不会发生并发修改问题，**所以乐观锁不会使用锁机制去主动的对数据进行上锁**，而是在数据修改之后，才正式对数据是否冲突进行校验（使用版本号的方式），如果发现了冲突，则提示错误，由用户决定下一步操作（撤销修改或者覆盖等）

### CAS 导致 的 **<u>ABA 问题</u>**

线程O1读取值之后 发生两次写入 由其他线程修改两次后 值没有发生变化 无法判断是否修改 这种操作不一定会影响结果 但是还是需要**增加额外的标志位或者时间戳**的方法来解决这类问题 <u>JUC并发工具包</u>中提供了这样的类 

1. AtomicInteger/AtomicBoolean/AtomicLong
2. AtomicIntegerArray/AtomicLongArray/AtomicReferenceArray
3. AtomicReference/AtomicStampedReference/AtomicMarkableReference

---

## 线程池

**一种管理线程的工具**

### 作用

1. 降低资源消耗，通过池化思想，减少创建线程和销毁线程的消耗，控制资源
2. 提高响应速度，任务到达时，无需创建线程即可运行
3. 提供更多更强大的功能，可扩展性高

```java
//线程池的构造方法
public ThreadPoolExecutor(int corePoolSize,
                          int maximumPoolSize,
                          long keepAliveTime,
                          TimeUnit unit,
                          BlockingQueue<Runnable> workQueue,
                          ThreadFactory threadFactory,
                          RejectedExecutionHandler handler) {}
```

![关系图](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9wOS1qdWVqaW4uYnl0ZWltZy5jb20vdG9zLWNuLWktazN1MWZicGZjcC85ZGFhMDM2NmY4Y2E0YmU4YWY3NWY3MDg2MTliNmQ2Y350cGx2LWszdTFmYnBmY3Atem9vbS0xLmltYWdl?x-oss-process=image/format,png)

| 参数名          | 参数意义                       |
| --------------- | ------------------------------ |
| corePoolSize    | 核心线程数                     |
| maximumPoolSize | 最大线程数                     |
| keepAliveTime   | 救急线程的空闲时间             |
| unit            | 救急线程的空闲时间单位         |
| workQueue       | 阻塞队列                       |
| threadFactory   | 创建线程的工厂，主要定义线程名 |
| handler         | 拒绝策略                       |

### **线程池案例**

1. 客户到银行时，开启柜台进行办理，柜台相当于线程，客户相当于任务，有两个是常开的柜台，三个是临时柜台。2就是核心线程数，5是最大线程数。即有两个核心线程
2. 当柜台开到第二个后，都还在处理业务。客户再来就到排队大厅排队。排队大厅只有三个座位。
3. 排队大厅坐满时，再来客户就继续开柜台处理，目前最大有三个临时柜台，也就是三个救急线程
4. 此时再来客户，就无法正常为其 提供业务，采用拒绝策略来处理它们
5. 当柜台处理完业务，就会从排队大厅取任务，当柜台隔一段空闲时间都取不到任务时，如果当前线程数大于核心线程数时，就会回收线程。即撤销该柜台。

![银行办理业务](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9wMy1qdWVqaW4uYnl0ZWltZy5jb20vdG9zLWNuLWktazN1MWZicGZjcC82YjUxNjM1OGIwNzk0ZTc0ODIyOTQyYjJlMjUyMWIzOH50cGx2LWszdTFmYnBmY3Atem9vbS0xLmltYWdl?x-oss-process=image/format,png)

### 线程池的主要流程

线程池创建、接收任务、执行任务、回收线程的步骤

1. 创建线程池后，线程池的状态是Running，该状态下才能有下面的步骤
2. 提交任务时，线程池会创建线程去处理任务
3. 当线程池的工作线程数达到corePoolSize时，继续提交任务会进入阻塞队列
4. 当阻塞队列装满时，继续提交任务，会创建救急线程来处理
5. 当线程池中的工作线程数达到maximumPoolSize时，会执行拒绝策略
6. 当线程取任务的时间达到keepAliveTime还没有取到任务，工作线程数大于corePoolSize时，会回收该线程

 注意： 不是刚创建的线程是核心线程，后面创建的线程是非核心线程，线程是没有核心非核心的概念的，这是我长期以来的误解。

拒绝策略：

1. 调用者抛出RejectedExecutionException (默认策略)
2. 让调用者运行任务
3. 丢弃此次任务
4. 丢弃阻塞队列中最早的任务，加入该任务

### 线程池的关闭

- shutdown()

会让线程池状态为shutdown，不能接收任务，但是会将工作线程和阻塞队列里的任务执行完 相当于优雅关闭。

```java
public void shutdown() {
    final ReentrantLock mainLock = this.mainLock;
    mainLock.lock();
    try {
        checkShutdownAccess();
        advanceRunState(SHUTDOWN);
        interruptIdleWorkers();
        onShutdown(); // hook for ScheduledThreadPoolExecutor
    } finally {
        mainLock.unlock();
    }
    tryTerminate();
}
```

- shutdownNow()

会让线程池状态为stop， 不能接收任务，会立即中断执行中的工作线程，并且不会执行阻塞队列里的任务， 会返回阻塞队列的任务列表

```java
public List<Runnable> shutdownNow() {
    List<Runnable> tasks;
    final ReentrantLock mainLock = this.mainLock;
    mainLock.lock();
    try {
        checkShutdownAccess();
        advanceRunState(STOP);
        interruptWorkers();
        tasks = drainQueue();
    } finally {
        mainLock.unlock();
    }
    tryTerminate();
    return tasks;
}
```

---

---

# Redis <redis io>

**开源**的、使用**C语言编写**的、支持**网络交互**的、可基于**内存也可持久化的Key-Value数据库**。

redi是一种高级的**key  :  value**存储数据结构 

其中**value支持以下五种数据**：

1.字符串（Strings）
2.字符串列表（Lists）
3.字符串集合（Sets）
4.有序字符串集合（Sorted Sets）
5.哈希（Hashes）

**key的规范使用**：

1.key不能太长 key也不要太短 尽量不要超过1024字节 太长：消耗内存 降低查找效率 太短： key可读性降低

2.key最好使用统一的命名模式，例如user:10000:passwd

**Strings** ：能存储字符串 并且有持久化操作功能 而遇到数值操作指令时 redis会将字符串类型转换成数值并且计算这个特性来实现业务上计数便利。

```yaml
set mystr "hello world!" //设置字符串类型
get mystr //读取字符串类型
set mynum "2"
OK
get mynum 
"2"
incr mynum 
(integer) 3
get mynum 
"3"
```

**Lists**：底层实现上并不是数组，而是**双端链表**









# REST_ful 风格

---

## REST <Resource Representational State Transfer> 

**对资源的访问状态通过url路径的体现出来 一种交互形式或者说模式风格**

**Resource** ：资源 REST架构核心 整个网络处理核心

**Representational** ：资源表达形式 例如 JSON  XML  JPRG

**State Transfer** ：状态变化 通过HTTP Methods实现

**通俗来讲：就是通过URL就知道要什么资源 通过HTTP Methods就知道要干什么实现什么 通过HTTP State Code就知道结果如何**

```yaml
example: 
GET/tasks			// 获取所有任务
POST/tasks 			// 创建新任务
GET/tasks/{id} 		// 通过任务id获取任务
PUT/tasks/{id}		// 通过任务id更新任务
DELETE/tasks/{id} 	// 通过任务id删除任务
- GET       //一次获取资源
- POST      //一次添加资源
- PUT       //一次修改资源
- DELETE  	//一次删除资源
#常见的HTTP State Code 
1xx：指示信息--表示请求已接收，继续处理
2xx：成功--表示请求已被成功接收
3xx：重定向--要完成请求必须进行更进一步的操作
4xx：客户端错误--请求有语法错误或请求无法实现
5xx：服务器端错误--服务器未能实现合法的请求
```

REST_ful 优点：

- 风格统一 易读
- 面向资源 具有解释性
- 充分利用HTTP协议语义





# Web传输核心协议

## HTTP 



## HTTPS















- 

# 算法





=======
# JAVA 8 新特征

- Lambda表达式 允许把函数作为一个方法的参数

1. Lambda 表达式，也可称为闭包，它是推动 Java 8 发布的最重要新特性。
2. Lambda 允许把函数作为一个方法的参数（函数作为参数传递进方法中）。
3. 使用 Lambda 表达式可以使代码变的更加简洁紧凑。

```java
//Lambda 表达式实例
// 1. 不需要参数,返回值为 5  
() -> 5  
  
// 2. 接收一个参数(数字类型),返回其2倍的值  
x -> 2 * x  
  
// 3. 接受2个参数(数字),并返回他们的差值  
(x, y) -> x – y  
  
// 4. 接收2个int型整数,返回他们的和  
(int x, int y) -> x + y  
  
// 5. 接受一个 string 对象,并在控制台打印,不返回任何值(看起来像是返回void)  
(String s) -> System.out.print(s)
```

```java
public class Java8Tester {
   public static void main(String args[]){
      Java8Tester tester = new Java8Tester();
        
      // 类型声明
      MathOperation addition = (int a, int b) -> a + b;
        
      // 不用类型声明
      MathOperation subtraction = (a, b) -> a - b;
        
      // 大括号中的返回语句
      MathOperation multiplication = (int a, int b) -> { return a * b; };
        
      // 没有大括号及返回语句
      MathOperation division = (int a, int b) -> a / b;
        
      System.out.println("10 + 5 = " + tester.operate(10, 5, addition));
      System.out.println("10 - 5 = " + tester.operate(10, 5, subtraction));
      System.out.println("10 x 5 = " + tester.operate(10, 5, multiplication));
      System.out.println("10 / 5 = " + tester.operate(10, 5, division));
        
      // 不用括号
      GreetingService greetService1 = message ->
      System.out.println("Hello " + message);
        
      // 用括号
      GreetingService greetService2 = (message) ->
      System.out.println("Hello " + message);
        
      greetService1.sayMessage("Runoob");
      greetService2.sayMessage("Google");
   }
    
   interface MathOperation {
      int operation(int a, int b);
   }
    
   interface GreetingService {
      void sayMessage(String message);
   }
    
   private int operate(int a, int b, MathOperation mathOperation){
      return mathOperation.operation(a, b);
   }
}
10 + 5 = 15
10 - 5 = 5
10 x 5 = 50
10 / 5 = 2
Hello Runoob
Hello Google
```

- 新的Stream API    **java.util.stream** 函数式编程风格引入
- 接口拥有默认方法  **支持default和static方法**   不再是传统的 ~~接口中方法都为抽象方法。~~
- Optional类 成为JAVA8自带库一部分 用来解决空指针异常
- Date Time API 加强对日期时间处理

# Java基础概念

一个 Java 程序可以认为是一系列对象的集合，而这些对象通过调用彼此的方法来协同工作。下面简要介绍下**类**、**对象**、**方法**和**实例变量**的概念。

## 基本概念

**对象**：**对象是类的一个实例**，有状态和行为。例如，一条狗是一个对象，它的状态有：颜色、名字、品种；行为有：摇尾巴、叫、吃等。

**类**：类是一个**模板**，它描述一类对象的行为（方法）和状态（属性）。

**方法**：**方法就是行为**，一个类可以有很多方法。逻辑运算、数据修改以及所有动作都是在方法中完成的。

**实例变量**：**每个对象都有独特的实例变量**，对象的状态由这些实例变量的值决定。

## 基本语法规范

1. 大小写敏感规范：Java 区分大小写是**大小写敏感**的，这就意味着标识符 Hello 与 hello 是不同的。
2. 类名规范：对于所有类来说，类名由多个单词组成那么**每个单词首字母应该大写**。例如 **MyFirstJavaClass** 。
3. 方法名规范：对于方法类来说，方法名由多个单词组成那么**首个单词首字母应该小写**，**后续单词则大写开头**。
4. 源文件名规范：**源文件名必须和类名相同**。当保存文件的时候，文件名的后缀为 **.java**。
5. 主方法入口规范：所有的 Java 程序由 <psvm>**public static void main(String[] args)** 方法开始执行。

## Java 标识符规范

- 所有的标识符都应该以字母（A-Z 或者 a-z）,美元符（$）、或者下划线（_）开始
- 首字符之后可以是字母（A-Z 或者 a-z）,美元符（$）、下划线（_）或数字的任何字符组合
- 关键字不能用作标识符
- 标识符是大小写敏感的
- 合法标识符举例：age、$salary、_value、__1_value
- 非法标识符举例：123abc、-salary

## Java修饰符规范

- 访问控制修饰符 : default, public , protected, private。
- 非访问控制修饰符 : final, abstract, static, synchronized。

## Java 枚举规范

枚举限制变量只能是预先设定好的值。使用枚举可以减少代码中的 bug。

例如：我们为果汁店设计一个程序，它将限制果汁为小杯、中杯、大杯。这就意味着它不允许顾客点除了这三种尺寸外的果汁。

```java
class FreshSize {
   enum HotSize{ XXL, XL , L }//三种尺寸的枚举描述类
   HotSize size;//枚举对象
}
public class FreshSizeTest {
   public static void main(String[] args){
      FreshSize fs = new FreshSize();//创建对象
      fs.size = FreshSize.HotSize.L;//赋值给实例
   }
}//枚举可以单独声明或者声明在类里面。方法、变量、构造函数也可以在枚举中定义。
```

## Java 变量规范

### 局部变量

（方法中） 类的方法中的变量。

> 局部变量声明在方法、构造方法或者语句块中；
>
> 局部变量是在栈上分配的。
>
> 访问修饰符不能用于局部变量；
>
> 局部变量在方法、构造方法、或者语句块被执行的时候创建，当它们执行完成后，变量将会被销毁；
>
> 局部变量没有默认值，所以局部变量被声明后，必须经过初始化，才可以使用。
>
> ```java
> public class Test{ 
>    public void pupAge(){
>       int age = 0;
>       age = age + 7;
>       System.out.println("小狗的年龄是: " + age);
>    }
>    
>    public static void main(String[] args){
>       Test test = new Test();
>       test.pupAge();
>    }
> }
> //小狗的年龄是: 7
> ```

### 成员变量

（非静态变量）独立于方法之外的变量，不过没有 static 修饰。

> 当一个对象被实例化之后，每个实例变量的值就跟着确定；
>
> 访问修饰符可以修饰实例变量；
>
> 实例变量在对象创建的时候创建，在对象被销毁的时候销毁；
>
> 实例变量的值应该至少被一个方法、构造方法或者语句块引用，使得外部能够通过这些方式获取实例变量信息；
>
> 实例变量可以声明在使用前或者使用后；
>
> 实例变量具有默认值。数值型变量的默认值是0，布尔型变量的默认值是false，引用类型变量的默认值是null。变量的值可以在声明时指定，也可以在构造方法中指定；
>
> 实例变量对于类中的方法、构造方法或者语句块是可见的。一般情况下应该把实例变量设为私有。通过使用访问修饰符可以使实例变量对子类可见；
>
> 实例变量可以直接通过变量名访问。但在静态方法以及其他类中，就应该使用完全限定名：ObjectReference.VariableName。
>
> ```java
> import java.io.*;
> public class Employee{
>    // 这个实例变量对子类可见
>    public String name;
>    // 私有变量，仅在该类可见
>    private double salary;
>    //在构造器中对name赋值
>    public Employee (String empName){
>       name = empName;
>    }
>    //设定salary的值
>    public void setSalary(double empSal){
>       salary = empSal;
>    }  
>    // 打印信息
>    public void printEmp(){
>       System.out.println("名字 : " + name );
>       System.out.println("薪水 : " + salary);
>    }
> 
>    public static void main(String[] args){
>       Employee empOne = new Employee("RUNOOB");
>       empOne.setSalary(1000.0);
>       empOne.printEmp();
>    }
> }
> //$ javac Employee.java 
> //$ java Employee
> //名字 : RUNOOB
> //薪水 : 1000.0
> ```

### 类变量（静态变量）

> 类变量也称为静态变量，在类中以 static 关键字声明，但必须在方法之外。
>
> **无论一个类创建了多少个对象，类只拥有类变量的一份拷贝。**
>
> 静态变量除了被声明为常量外很少使用，静态变量是指声明为 public/private，final 和 static 类型的变量。静态变量初始化后不可改变。
>
> **静态变量储存在静态存储区。经常被声明为常量，很少单独使用 static 声明变量。**
>
> **静态变量在第一次被访问时创建，在程序结束时销毁。**
>
> 与实例变量具有相似的可见性。但为了对类的使用者可见，大多数静态变量声明为 public 类型。
>
> 默认值和实例变量相似。**数值型变量默认值是 0，布尔型默认值是 false，引用类型默认值是 null。**变量的值可以在声明的时候指定也可以在构造方法中指定。此外，静态变量还可以在静态语句块中初始化。
>
> 静态变量可以通过：*ClassName.VariableName*的方式访问。
>
> 类变量被声明为 public static final 类型时，类变量名称一般建议使用大写字母。如果静态变量不是 public 和 final 类型，其命名方式与实例变量以及局部变量的命名方式一致。
>
> ```java
> public class Employee {
>     //salary是静态的私有变量
>     private static double salary;
>     // DEPARTMENT是一个常量
>     public static final String DEPARTMENT = "开发人员";
>     public static void main(String[] args){
>     salary = 10000;
>         System.out.println(DEPARTMENT+"平均工资:"+salary);
>     }
> }
> //开发人员平均工资:10000.0
> ```

#### 静态方法

（1）静态方法中不需要它所属类的任何实例就可以访问，所以在静态方法中不可以使用this关键字
（2）静态方法中不可直接访问所属类的实例变量和实例方法，但可以直接访问所属类的静态变量和静态方法

## 继承与接口规范

1.继承：在 Java 中，一个类可以由其他类派生。如果你要创建一个类，而且已经存在一个类具有你所需要的属性或方法，那么你可以将新创建的类继承该类。利用继承的方法，可以重用已存在类的方法和属性，而不用重写这些代码。被继承的类称为超类（super class），派生类称为子类（sub class）。

2.接口：在 Java 中，接口可理解为对象间相互通信的协议。接口在继承中扮演着很重要的角色。接口只定义派生要用到的方法，但是方法的具体实现完全取决于派生类。

## 基本数据类型

变量就是申请内存来存储值。也就是说，当创建变量的时候，需要在内存中申请空间。内存管理系统根据变量的类型为变量分配存储空间，分配的空间只能用来储存该类型数据。

![img](https://www.runoob.com/wp-content/uploads/2013/12/2020-10-27-code-mem.png)

Java 的两大数据类型:

- **内置数据类型**
- **引用数据类型**

### **内置数据类型**

Java语言提供了**八种基本类型**。六种数字类型（**四个整数型，两个浮点型**），**一种字符类型**，还有一种**布尔**型。

> - **byte**：8位有符号的以二进制补码表示的整数；最小值是 **-128（-2^7）**最大值是 **127（2^7-1）**默认值是 **0**；
>
> byte 类型用在大型数组中节约空间，主要代替整数，因为 byte 变量占用的空间只有 int 类型的四分之一；
>
> - **short：**16 位、有符号的以二进制补码表示的整数，最小值是 **-32768（-2^15）**最大值是 **32767（2^15 - 1）**默认值是 **0** 
>
> Short 数据类型也可以像 byte 那样节省空间。一个short变量是int型变量所占空间的二分之一；
>
> - **int**：32位、有符号的以二进制补码表示的整数；最小值是 **-2,147,483,648（-2^31）**最大值是 **2,147,483,647（2^31 - 1）**默认值是 **0**
>
> 一般地整型变量默认为 int 类型
>
> - **long：** 64 位、有符号的以二进制补码表示的整数；最小值是 **-9,223,372,036,854,775,808（-2^63）**；最大值是 **9,223,372,036,854,775,807（2^63 -1）**；
>
> 默认值是 **0L **这种类型主要使用在需要比较大整数的系统上；
>
> - **float：**单精度、32位、符合IEEE 754标准的浮点数；默认值是 **0.0f**；
>
> 浮点数不能用来表示精确的值，如货币；float 在储存大型浮点数组的时候可节省内存空间；
>
> - **double：**双精度、64 位、符合 IEEE 754 标准的浮点数；double类型同样不能表示精确的值，如货币；
>
> 默认值是 **0.0d**；浮点数的默认类型为 double 类型；
>
> - **char**：一个单一的 16 位 Unicode 字符；最小值是 **\u0000**（十进制等效值为 0）；最大值是 **\uffff**（即为 65535）；char 数据类型可以储存任何字符；例子：char letter = 'A';
>
> - **boolean：**只有两个取值：true 和 false；**默认值是 false**

### **引用数据类型**

> 在Java中，引用类型的变量非常类似于C/C++的指针。引用类型指向一个对象，指向对象的变量是引用变量。这些变量在声明时被指定为一个特定的类型，比如 Employee、Puppy 等。变量一旦声明后，类型就不能被改变了。
>
> 所有引用类型的默认值都是null；对象、数组都是引用数据类型；一个引用变量可以用来引用任何与之兼容的类型。
>
> ### 引用类型
>
> > 引用是一个对象别名，与被引用的对象共享同一块内存区域。例如“鹿晗”这个对象，他的原名是“刘壮实”，但两者其实都是指同一个人（内存）。对象在创建时会请求一块内存空间来保存数据，会根据对象大小分配存储空间大小不等的内存区域。在Java中，访问对象时，不会直接访问对象在内存中的数据，而是通过引用去访问。因此，引用也是一种数据类型，类似于C/C++ 语言中的指针。引用定义时在栈中分配内存，引用变量在程序运行到作用域外释。
> >
> > java的引用类型有：1、强引用；2、软引用；3、弱引用；4、虚引用。

### 类型转换规范

<u>整数的默认类型是 int ; 小数默认是 double 类型浮点型，在定义 float 类型时必须在数字后面跟上 F 或者 f。</u>

**整型、实型（常量）、字符型数据可以混合运算。运算中，不同类型的数据先转化为同一类型，然后进行运算。**

```xml
转换从低级到高级。
低  ------------------------------------>  高
byte,short,char—> int —> long—> float —> double 
```

1.  不能对boolean类型进行类型转换。

2.  不能把对象类型转换成不相关类的对象。

3. 在把容量大的类型转换为容量小的类型时必须使用强制类型转换。

4. 转换过程中可能导致溢出或损失精度，例如：

   ```java
   int i =128;   
   byte b = (byte)i;
   //因为 byte 类型是 8 位，最大值为127，所以当 int 强制转换为 byte 类型时，值 128 时候就会导致溢出。
   ```

5. 浮点数到整数的转换是通过舍弃小数得到，而不是四舍五入，例如：

   ```java
   (int)23.7 == 23;        
   (int)-45.89f == -45
   ```

**java中的类型转换大致分为两种：1.自动类型转换  2.强制类型转换** 

#### 1.自动类型转换

必须满足转换前的数据类型的位数要低于转换后的数据类型，例如: short数据类型的位数为16位，就可以自动转换位数为32的int类型，同样float数据类型的位数为32，可以自动转换为64位的double类型。

```java
public class ZiDongLeiZhuan{
        public static void main(String[] args){
            char c1='a';//定义一个char类型
            int i1 = c1;//char自动类型转换为int
            System.out.println("char自动类型转换为int后的值等于"+i1);
            char c2 = 'A';//定义一个char类型
            int i2 = c2+1;//char 类型和 int 类型计算
            System.out.println("char类型和int计算后的值等于"+i2);
        }
}
//char自动类型转换为int后的值等于97
//char类型和int计算后的值等于66
解析：c1 的值为字符 a ,查 ASCII 码表可知对应的 int 类型值为 97， A 对应值为 65，所以 i2=65+1=66。
```

#### 2.强制类型转换

条件是转换的数据类型必须是兼容的。格式：(type)value type是要强制类型转换后的数据类型 实例：

```java
public class QiangZhiZhuanHuan{
    public static void main(String[] args){
        int i1 = 123;
        byte b = (byte)i1;//强制类型转换为byte
        System.out.println("int强制类型转换为byte后的值等于"+b);
    }
}
//int强制类型转换为byte后的值等于123
```

## Java 异常处理

异常是程序中的一些错误，但并不是所有的错误都是异常，并且错误有时候是可以避免的。

异常发生的原因有很多，通常包含以下几大类：

- **用户输入了非法数据。**
- **要打开的文件不存在。**
- **网络通信时连接中断，或者JVM内存溢出。**

这些异常有的是因为用户错误引起，有的是程序错误引起的，还有其它一些是因为物理错误引起的。

要理解Java异常处理是如何工作的，你需要掌握以下三种类型的异常：

- **检查性异常：**最具代表的检查性异常是用户错误或问题引起的异常，这是程序员无法预见的。例如要打开一个不存在文件时，一个异常就发生了，这些异常在编译时不能被简单地忽略。
- **运行时异常：** 运行时异常是可能被程序员避免的异常。与检查性异常相反，运行时异常可以在编译时被忽略。
- **错误：** 错误不是异常，而是脱离程序员控制的问题。错误在代码中通常被忽略。例如，当栈溢出时，一个错误就发生了，它们在编译也检查不到的。

### Exception 类

所有的异常类是从 java.lang.Exception 类继承的子类。

Exception 类是 Throwable 类的子类。除了Exception类外，Throwable还有一个子类Error 。

Java 程序通常不捕获错误。错误一般发生在严重故障时，它们在Java程序处理的范畴之外。

Error 用来指示运行时环境发生的错误。

例如，JVM 内存溢出。一般地，程序不会从错误中恢复。

异常类有两个主要的子类：IOException 类和 RuntimeException 类。![img](https://www.runoob.com/wp-content/uploads/2013/12/exception-hierarchy.png)

### Java 内置异常类

Java 语言定义了一些异常类在 java.lang 标准包中。

标准运行时异常类的子类是最常见的异常类。由于 java.lang 包是默认加载到所有的 Java 程序的，所以大部分从运行时异常类继承而来的异常都可以直接使用。

Java 根据各个类库也定义了一些其他的异常，下面的表中列出了 Java 的**非检查性异常**。

| **异常**                        | **描述**                                                     |
| :------------------------------ | :----------------------------------------------------------- |
| ArithmeticException             | 当出现异常的运算条件时，抛出此异常。例如，一个整数"除以零"时，抛出此类的一个实例。 |
| ArrayIndexOutOfBoundsException  | 用非法索引访问数组时抛出的异常。如果索引为负或大于等于数组大小，则该索引为非法索引。 |
| ArrayStoreException             | 试图将错误类型的对象存储到一个对象数组时抛出的异常。         |
| ClassCastException              | 当试图将对象强制转换为不是实例的子类时，抛出该异常。         |
| IllegalArgumentException        | 抛出的异常表明向方法传递了一个不合法或不正确的参数。         |
| IllegalMonitorStateException    | 抛出的异常表明某一线程已经试图等待对象的监视器，或者试图通知其他正在等待对象的监视器而本身没有指定监视器的线程。 |
| IllegalStateException           | 在非法或不适当的时间调用方法时产生的信号。换句话说，即 Java 环境或 Java 应用程序没有处于请求操作所要求的适当状态下。 |
| IllegalThreadStateException     | 线程没有处于请求操作所要求的适当状态时抛出的异常。           |
| IndexOutOfBoundsException       | 指示某排序索引（例如对数组、字符串或向量的排序）超出范围时抛出。 |
| NegativeArraySizeException      | 如果应用程序试图创建大小为负的数组，则抛出该异常。           |
| NullPointerException            | 当应用程序试图在需要对象的地方使用 `null` 时，抛出该异常     |
| NumberFormatException           | 当应用程序试图将字符串转换成一种数值类型，但该字符串不能转换为适当格式时，抛出该异常。 |
| SecurityException               | 由安全管理器抛出的异常，指示存在安全侵犯。                   |
| StringIndexOutOfBoundsException | 此异常由 `String` 方法抛出，指示索引或者为负，或者超出字符串的大小。 |
| UnsupportedOperationException   | 当不支持请求的操作时，抛出该异常。                           |

下面的表中列出了 Java 定义在 java.lang 包中的**检查性异常类**。

| **异常**                   | **描述**                                                     |
| :------------------------- | :----------------------------------------------------------- |
| ClassNotFoundException     | 应用程序试图加载类时，找不到相应的类，抛出该异常。           |
| CloneNotSupportedException | 当调用 `Object` 类中的 `clone` 方法克隆对象，但该对象的类无法实现 `Cloneable` 接口时，抛出该异常。 |
| IllegalAccessException     | 拒绝访问一个类的时候，抛出该异常。                           |
| InstantiationException     | 当试图使用 `Class` 类中的 `newInstance` 方法创建一个类的实例，而指定的类对象因为是一个接口或是一个抽象类而无法实例化时，抛出该异常。 |
| InterruptedException       | 一个线程被另一个线程中断，抛出该异常。                       |
| NoSuchFieldException       | 请求的变量不存在                                             |
| NoSuchMethodException      | 请求的方法不存在                                             |

### 异常方法

下面的列表是 Throwable 类的主要方法:

| **序号** | **方法及说明**                                               |
| :------- | :----------------------------------------------------------- |
| 1        | **public String getMessage()** 返回关于发生的异常的详细信息。这个消息在Throwable 类的构造函数中初始化了。 |
| 2        | **public Throwable getCause()** 返回一个 Throwable 对象代表异常原因。 |
| 3        | **public String toString()** 返回此 Throwable 的简短描述。   |
| 4        | **public void printStackTrace()** 将此 Throwable 及其回溯打印到标准错误流。。 |
| 5        | **public StackTraceElement [] getStackTrace()** 返回一个包含堆栈层次的数组。下标为0的元素代表栈顶，最后一个元素代表方法调用堆栈的栈底。 |
| 6        | **public Throwable fillInStackTrace()** 用当前的调用栈层次填充Throwable 对象栈层次，添加到栈层次任何先前信息中。 |

### 捕获异常<重要>

使用 try 和 catch 关键字可以捕获异常。try/catch 代码块放在异常可能发生的地方。

try/catch代码块中的代码称为保护代码，使用 try/catch 的语法如下：

```
try
{
   // 程序代码
}catch(ExceptionName e1)
{
   //Catch 块
}
```

Catch 语句包含要捕获异常类型的声明。当保护代码块中发生一个异常时，try 后面的 catch 块就会被检查。

如果发生的异常包含在 catch 块中，异常会被传递到该 catch 块，这和传递一个参数到方法是一样。

```java
// 文件名 : ExcepTest.java
import java.io.*;
public class ExcepTest{
 
   public static void main(String args[]){
      try{
         int a[] = new int[2];
         System.out.println("Access element three :" + a[3]);
      }catch(ArrayIndexOutOfBoundsException e){
         System.out.println("Exception thrown  :" + e);
      }
      System.out.println("Out of the block");
   }
}
//Exception thrown  :java.lang.ArrayIndexOutOfBoundsException: 3
//Out of the block
```

### 多重捕获块

一个 try 代码块后面跟随多个 catch 代码块的情况就叫多重捕获。

多重捕获块的语法如下所示：

```java
try{
   // 程序代码
}catch(异常类型1 异常的变量名1){
  // 程序代码
}catch(异常类型2 异常的变量名2){
  // 程序代码
}catch(异常类型3 异常的变量名3){
  // 程序代码
}
```

上面的代码段包含了 3 个 catch块。

可以在 try 语句后面添加任意数量的 catch 块。

如果保护代码中发生异常，异常被抛给第一个 catch 块。

如果抛出异常的数据类型与 ExceptionType1 匹配，它在这里就会被捕获。

如果不匹配，它会被传递给第二个 catch 块。

如此，直到异常被捕获或者通过所有的 catch 块。

```java
#实例:
    try {
    file = new FileInputStream(fileName);
    x = (byte) file.read();
} catch(FileNotFoundException f) { // Not valid!
    f.printStackTrace();
    return -1;
} catch(IOException i) {
    i.printStackTrace();
    return -1;
}
```

### throws/throw 关键字

如果一个方法没有捕获到一个检查性异常，那么该方法必须使用 throws 关键字来声明。throws 关键字放在方法签名的尾部。

也可以使用 throw 关键字抛出一个异常，无论它是新实例化的还是刚捕获到的。

**一个方法可以声明抛出多个异常，多个异常之间用逗号隔开。**

例如，下面的方法声明抛出 RemoteException 和 InsufficientFundsException：

```java
import java.io.*;
public class className
{
   public void withdraw(double amount) throws RemoteException,
                              InsufficientFundsException
   {
       // Method implementation
   }
   //Remainder of class definition
}
```

### finally关键字

finally 关键字用来创建在 try 代码块后面执行的代码块。

无论是否发生异常，finally 代码块中的代码总会被执行。

在 finally 代码块中，可以运行清理类型等收尾善后性质的语句。

finally 代码块出现在 catch 代码块最后，语法如下：

```java
try{
  // 程序代码
}catch(异常类型1 异常的变量名1){
  // 程序代码
}catch(异常类型2 异常的变量名2){
  // 程序代码
}finally{
  // 程序代码
}
```

```java
//实例：
public class ExcepTest{
  public static void main(String args[]){
    int a[] = new int[2];
    try{
       System.out.println("Access element three :" + a[3]);
    }catch(ArrayIndexOutOfBoundsException e){
       System.out.println("Exception thrown  :" + e);
    }
    finally{
       a[0] = 6;
       System.out.println("First element value: " +a[0]);
       System.out.println("The finally statement is executed");
    }
  }
}
//Exception thrown  :java.lang.ArrayIndexOutOfBoundsException: 3
//First element value: 6
//The finally statement is executed
```

### try-with-resources语法糖

JDK7 之后，Java 新增的 **try-with-resource** 语法糖来打开资源，并且可以在语句执行完毕后确保每个资源都被自动关闭 。

JDK7 之前所有被打开的系统资源，比如流、文件或者 Socket 连接等，都需要被开发者手动关闭，否则将会造成资源泄露。

```java
try (resource declaration) {
  // 使用的资源
} catch (ExceptionType e1) {
  // 异常块
}
```

以上的语法中 try 用于声明和实例化资源，catch 用于处理关闭资源时可能引发的所有异常。

**注意：**try-with-resources 语句关闭所有实现 AutoCloseable 接口的资源。

```java
public class RunoobTest {

    public static void main(String[] args) {
    String line;
        try(BufferedReader br = new BufferedReader(new FileReader("test.txt"))) {
            while ((line = br.readLine()) != null) {
                System.out.println("Line =>"+line);
            }
        } catch (IOException e) {
            System.out.println("IOException in try block =>" + e.getMessage());
        }
    }
}
```

以上实例输出结果为：

```
IOException in try block =>test.txt (No such file or directory)
```

### 通用异常

在Java中定义了两种类型的异常和错误。

- **JVM(Java虚拟机)**异常：**由 JVM 抛出的异常或错误。例如：NullPointerException 类，ArrayIndexOutOfBoundsException 类，ClassCastException 类。
- **程序级异常：**由程序或者API程序抛出的异常。例如 IllegalArgumentException 类，IllegalStateException 类。

# Spring

**全面的企业应用开发一站式的解决方案 (与其他框架兼容 例如MyBatis,Hibernate,Shrio)**

**特点 ：轻量级(仅需2M JAR文件)  非入侵式(无捆绑的)  应用中的对象不依赖与spring特定类 支持junit4测试**![spring-overview](https://www.runoob.com/wp-content/uploads/2015/07/673670c9a34075831373b711cb8f21b7.png)

## Spring的核心机制

**管理Bean**

程序主要是通过Spring容器来访问容器中的Bean，ApplicationContext是Spring容器最常用的接口，该接口有如下两个实现类：

- ClassPathXmlApplicationContext: 从类加载路径下搜索配置文件，并根据配置文件来创建Spring容器。
- FileSystemXmlApplicationContext: 从文件系统的相对路径或绝对路径下去搜索配置文件，并根据配置文件来创建Spring容器。

```java
public class BeanTest{
    public static void main(String args[]) throws Exception{
        ApplicationContext ctx = new ClassPathXmlApplicationContext("beans.xml");
        Person p = ctx.getBean("person", Person.class);
        p.say();
    }
}
```





## **1.控制反转IOC  **

**由spring容器管理整个bean的生命周期 通过<u>反射</u>实现对其它对象控制 包括初始化 创建 销毁等 无需手动管理对象过程**

> **1.1依赖注入DI**   促进低耦合 常用@Autowired根据属性自动装配无需字段的 set 方法 
>
> ```java
> //成员属性字段使用 @Autowired，无需字段的 set 方法
> @Autowired
> private AdminServiceImpl adminService;
> //set 方法使用 @Autowired
> private AdminServiceImpl adminService1;
> @Autowired
> public void setAdminService1(AdminServiceImpl adminService){
>   this.adminService1 = adminService;
> }
> //构造方法使用 @Autowired
> private AdminServiceImpl adminService2;
> @Autowired
> AdminController(AdminServiceImpl adminService){
>   this.adminService2 = adminService;
> }
> ```
>
> ----
>
> **1.2依赖查询DL** 
>
> **一个对象依赖的其他对象会以被动的方式传递进来 即无需创建查找依赖对象**
>
> **实现：容器中的受控对象通过容器的 API 来查找自己所依赖的资源和协作对象。**
>
> 依赖查询DL也有两种方式
>
> - 依赖拖拽：注入的对象如何与组件发生联系，这个过程就是通过依赖拖拽实现；
>
> - 上下文依赖查找：在某些方面跟依赖拖拽类似，但是上下文依赖查找中，查找的过程是在容器管理的资源中进行的，而不是从集中注册表中，并且通常是作用在某些设置点上；
>
>   ---
>

### **<u>简述IOC初始化过程？</u>**

> > 1. 首先要看你是怎么声明注入bean的  常见的**xml 配置 注解  bean配置** 我最常用的是**AnnotationConfigApplication**注解容器，也就是使用**@Configuration**进行注册 然后解析成Bean
> > 2. 将Bean解析成**BeanDefinition** 一个对bean信息进行包装的类 会对bean配置的参数进行或者是XML配置的property标签注入到BeanDefinition的实例中
> > 3. 再将对应的**beanDefinition**实例注册到容器**beanDefinitionMap**中
> > 4. **beanfactory**根据BeanDefinition创建实例化和初始化bean
>
> ----
>

### <u>**spring加载bean有哪些方式？**</u>

> > 1.首先要通过@Configuration+@Bean
> >
> > @Configuration用来声明一个配置类 然后使用@Bean声明一个bean 将其加入spring容器
> >
> > ```java
> > @Configuration
> > public class TestConfiguration {
> > @Bean
> > public Admin admin(){
> >   return new Admin();
> > }
> > }
> > ```
> >
> > 2.包扫描特定注解的方式 使用@Component或者@ComponentScan 
> >
> > @Component声明自己是个等待spring将自己实例化到spring容器中的类 让spring容器来统一管理 用起来不需要new了 相当于:
> >
> > ```java
> > <bean id="" class=""/>
> > ```
> >
> > 而@ComponentScan会指定一个路径 扫描路径内带有特定注解的bean 相当于告诉spring容器去哪里找自己需要的bean 添加进容器中 其中特定的注解会包括@Controller @Service @Repository @Component
> >
> > ```java
> > // 控制层
> > @Controller
> > public class UserController {
> > }
> > 
> > // 业务层
> > @Service
> > public class UserService {
> > }
> > 
> > // 持久层
> > @Repository
> > public class UserDao {
> > }
> > ```
> >
> > ```java
> > public class TestConfiguration {
> > @Test
> > public void Test() {
> >   AnnotationConfigApplicationContext applicationContext = new AnnotationConfigApplicationContext(AppConfig.class);
> >   String[] beanNames = applicationContext.getBeanDefinitionNames();
> >   for (String beanName:beanNames) {
> >       System.out.println("容器中对象名称："+beanName);
> >   }
> > 
> > }
> > }
> > @Configuration
> > @ComponentScan(value = "com.example.app.goodjobdemo.Test")
> > class AppConfig {
> > }
> > //容器中对象名称：appConfig
> > //容器中对象名称：userController
> > //容器中对象名称：userDao
> > //容器中对象名称：userService
> > ```
> >
> > 3.@Import注解导入 开发中很少使用 对spring扩展的时候才会经常用到 通常搭配自定义注解使用往容器导入配置类文件
> >
> > ```java
> > public class TestConfiguration {
> > @Test
> > public void Test() {
> >   AnnotationConfigApplicationContext applicationContext = new AnnotationConfigApplicationContext(AppConfig.class);
> >   String[] beanNames = applicationContext.getBeanDefinitionNames();
> >   for (String beanName:beanNames) {
> >       System.out.println("容器中对象名称："+beanName);
> >   }
> > 
> > }
> > }
> > @Configuration
> > @Import({UserController.class,UserDao.class,UserService.class})
> > class AppConfig {
> > }
> > //容器中对象名称：appConfig
> > //容器中对象名称：com.example.app.goodjobdemo.Test.UserController
> > //容器中对象名称：com.example.app.goodjobdemo.Test.UserDao
> > //容器中对象名称：com.example.app.goodjobdemo.Test.UserService
> > ```
> >
> > 4.实现BeanDefinitionRegistryPostProcessor进行后置处理
> >
> > ```java
> > //源码 BeanFactoryPostProcessor接口中只有一个方法 就是postProcessBeanDefinitionRegistry
> > public interface BeanDefinitionRegistryPostProcessor extends BeanFactoryPostProcessor {
> > 	void postProcessBeanDefinitionRegistry(BeanDefinitionRegistry registry) throws BeansException;
> > }
> > ```
> >
> > spring容器启动会执行postProcessBeanDefinitionRegistry方法 
> >
> > 即 等BeanDefinition加载完毕后进行后置处理 在此调整BeanDefinition就可以干扰到后面初始化bean操作
> >
> > 5.使用FactoryBean接口 
> >
> > 使用@Configuration+@Bean方式将AdminFactoryBean加入到容器中
> >
> > 代码如下 并没有向容器中直接注入Admin 而是注入AdminFactoryBean然后再从容器中拿到Admin这个类型的Bean
> >
> > ```java
> > @Configuration
> > public class TestConfiguration {
> > @Bean
> > public AdminFactoryBean adminFactoryBean(){
> >   return new AdminFactoryBean();
> > }
> > @Test
> > public void Test() {
> >   AnnotationConfigApplicationContext applicationContext = new AnnotationConfigApplicationContext(TestConfiguration.class);
> >   Admin bean = applicationContext.getBean(Admin.class);
> >   System.out.println(bean);
> > }
> > }
> > @Component
> > class AdminFactoryBean implements FactoryBean {
> > @Override
> > public Admin getObject() throws Exception {
> >   return new Admin();
> > }
> > @Override
> > public Class<?> getObjectType() {
> >   return Admin.class;
> > }
> > }
> > //Admin(id=null, name=null, password=null)
> > ```
> >
> > 还有很多实现注入Bean的方法
> >
> > `1.xml；2.扫描加注解；3.配置类@bean；4.实现factorybean；5.annotationapplicationcontext的register注册；6.import类；7.selectimport实现类；8.实现importbeandefinitionregister自定义bean；9.实现beandefinitionregisterpostprocessor后置注册修改bean`
>
> ---
>

### <u>**Spring bean 的生命周期？**</u>

> 1.调用Bean的构造方法创建Bean
>
> 2.通过反射调用setter方法进行属性依赖注入
>
> 2.1如果bean实现了BeanNameAware接口 spring将调用setBeanName()方法设置Bean的name(对应xml文件中bean的标签id)
>
> 2.2如果bean实现实现了BeanFacoryAware接口spring就将调用2.3setBeanFactory()把beanfactory设置给bean
>
> 2.4如果存在beanPostProcessor spring将会调用postProcessBeforeLinitialization预处理方法在bean初始化之前对其处理
>
> 2.5如果bean实现了InitialigBean接口spring将调用tafterPropertiesSet()方法 然后调用xml定义的init-method方法 两个方法作用类似 都是再初始化bean的时候执行
>
> 2.6如果存在beanPostProcessor spring将会调用postProcessAfterLinitialization初始化后方法在bean初始化之后对其处理
>
> 3.bean初始化完成 供应用使用 分为两种情况：
>
> 3.1如果bean为单例的话那么容器返回bean给用户并存入缓存池
>
> 如果实现了DisposableBean接口 spring将调用他的destory()然后调用xml中定义的destory-mothod方法 这两个方法作用类似都是在bean实例销毁前执行
>
> 3.2如说bean是多例的话 容器将bean返回给用户 剩下的生命周期将由用户控制
>
> ---

### <u>**Spring怎么解决循环依赖的？**</u>

> **Spring通过三级缓存来解决缓存依赖** 
>
> #example:两个对象互相形成依赖
> 创建Bean-A时 对Bean-A进行构造方法后就将Bean-A对象放入Spring的三级缓存**singletonFactories**
>
> 发现Bean-A依赖Bean-B，开始创建Bean-B并执行完Bean-B的构造方法后，放入三级缓存
>
> 处理Bean-B的依赖Bean-A时，发现三级缓存中有一个Bean-A，拿到这个BeanA完成B的注入，同时也完成A的注入

### **<u>Spring Bean如何保证并发安全？</u>**

> > ```yaml
> > example:
> > spring的bean默认都是单例的 singleton 某些情况下单例并发是不安全的
> > 假如我们在Controller控制层定义了成员变量 多个请求来临时进入的都是同一单例对象并且对成员变量进行修改会有并发安全风险
> > 如何解决？
> > ```
> >
> > 1.单例变原型
> >
> > 如果是web应用在controller类上加**@Scope("prototype")**或者**@Scope("request")**
> >
> > 如果不是web应用在Component类上加注解**@Scope("prototype")**
> >
> > 这种方式实现起虽然简单 但是会增加服务器资源中bean创建销毁实例的开销
> >
> > 2.尽量避免使用成员变量
> >
> > 在业务允许范围内 使用RequsetMapping方法中的局部变量替换控制层的成员 这种方式比较恰当
> >
> > 3.使用并发安全类
> >
> > 如果如果一定需要在单例bean使用成员变量 可以使用并发安全的容器
> >
> > 例如 ConcurrentHashMap  ConcurrentHashSet
> >
> > 4.分布式或者微服务 项目的并发安全解决方案
> >
> > 如果还需要考虑到微服务或者分布式服务的并发安全解决 第三种方法便不太合适
> >
> > 借助于可以共享某些信息的分布式缓存中间件 例如Redis等
> >
> > 这样既可以保证统一服务 不同服务实例 且都有同一共享信息
>
> ---
>

### **<u>Spring用到了那些设计模式？</u>**

> > **1.工厂模式** IOC容器可以使用BeanFactory 或 ApplicationContext创建 bean 对象 
> >
> > - BeanFactory 是bean合集工厂类 懒加载或者延时加载 (使用到某个 bean 的时候才会注入) 启动速度快占用内存少
> >
> > - ApplicationContext 是BeanFactory的扩展(接口提供额外功能)  即使加载(容器启动的时候 不管你用没用到 一次性创建所有 bean) 开发人员使用ApplicationContext会更多 
> >
> >   ```yaml
> >   #ApplicationContext的三个实现类
> >   -ClassPathXmlApplication：从类的根路径下加载配置文件（推荐使用这种）
> >   -FileSystemXmlApplication：它是从磁盘路径上加载配置文件，配置文件可以在磁盘的任意位置。
> >   -XmlWebApplicationContext：从Web系统中的XML文件载入上下文定义信息。
> >   -AnnotationConfigApplicationContext：当使用注解配置容器对象时，需要使用此类来创建 spring 容器。它用来读取注解
> >   ```
> >
> >   ```java
> >   //example
> >   ApplicationContext applicationContext = new ClassPathXmlApplicationContext("applicationContext.xml");
> >   UserService userService = (UserService) applicationContext.getBean("userService");
> >   userService.save();
> >   ```
> >
> > ---
> >
> > **2.单例模式** 一个类仅有一个实例 提供一个访问它的全局访问点
> >
> > **由于Spring中bean的默认作用域就是singleton(单例)的 优点如下：**
> >
> > - 对于频繁使用的对象，可以**省略创建对象所花费的时间**
> > - 由于new操作的次数减少，因而**对系统内存的使用频率也会降低 **减轻GC压力，缩短GC停顿时间
> >
> > **除了singleton作用域，Spring中bean还有下面几种作用域**
> >
> > - prototype : **每次**请求都会创建一个新的 bean 实例。
> > - request : 每一次HTTP请求都会产生一个新的bean，该bean仅在当前**HTTP request**内有效。
> > - session : 每一次HTTP请求都会产生一个新的 bean，该bean仅在当前**HTTP session**内有效。
> >
> > ---
> >
> > **3.代理模式**
> >
> > **1.Spring AOP**(Aspect-Oriented Programming:面向切面编程) **基于代理操作** 提供了两种动态代理实现 且都是**运行时增强** 
> >
> > - JDK Proxy 
> > - CGLIB Proxy
> >
> > **2.AspectJ AOP**  **是编译时增强**   基于**字节码操作(Bytecode Manipulation)**
> >
> > Spring AOP 已经集成了 AspectJ  相比于 Spring AOP 功能更加强大，但是 Spring AOP 相对来说更简单。如果我们的切面比较少，那么两者性能差异不大。但是，当切面太多的话，最好选择 AspectJ ，它比Spring AOP 快很多。
> >
> > ----
> >
> > **4.适配器模式 <Adapter Pattern>**
> >
> > **将一个接口转换成客户希望的另一个接口，适配器模式使接口不兼容的那些类可以一起工作，其别名为包装器(<u>Wrapper</u>)。**
> >
> > 比如 Spring MVC 中适配器HandlerAdatper，应用会有多个不同类型的Controller实现。如果需要调用方法会先判断是哪个Controller 再对应处理
> >
> > 如果增加一个 Controller就需要修改原来的判断逻辑 不利于维护 违反了模式设计开闭原则 <对扩展开放，对修改关闭>
> >
> > 为此Spring提供了该适配器接口 每个Controller对应一种HandlerAdatper实现类 对应请求时SpringMVC会通过getHandler()指定对应的Controller获取HandlerAdatper最后调用Handle()方法处理请求 实际是调用Controller的HandleRequest()方法
> >
> > 这种方法处理每次添加新的Controller时 只需增加一个适配器类即可 无需修改原有逻辑
> >
> > ---
> >
> > **5.观察者模式**      一种对象与对象之间具有依赖关系，当一个对象发生改变的时候，这个对象所依赖的对象也会做出反应
> >
> > - 事件角色 ：ApplicationEvent (org.springframework.context包下)抽象类
> >
> >    继承了java.util.EventObject并实现了 java.io.Serializable接口。
> >
> >   ```yaml
> >   #对ApplicationContextEvent的实现(继承自ApplicationContextEvent)
> >   - ContextStartedEvent：ApplicationContext 启动后触发的事件;
> >   - ContextStoppedEvent：ApplicationContext 停止后触发的事件;
> >   - ContextRefreshedEvent：ApplicationContext 初始化或刷新完成后触发的事件;
> >   - ContextClosedEvent：ApplicationContext 关闭后触发的事件。
> >   ```
> >
> > - 事件监听者角色  ApplicationListener接口 <java.util.EventListener>
> >
> >   里面只定义了一个 onApplicationEvent()方法来处理ApplicationEvent
> >
> >   我们只要实现 ApplicationListener 接口实现 onApplicationEvent() 方法即可完成监听事件
> >
> >   ```java
> >   package org.springframework.context;
> >   import java.util.EventListener;
> >   @FunctionalInterface
> >   public interface ApplicationListener<E extends ApplicationEvent> extends EventListener {
> >       void onApplicationEvent(E var1);
> >   }
> >   ```
> >
> > - 事件发布者角色 ApplicationEventPublisher  事件的发布者，它也是一个接口
> >
> >   ApplicationEventPublisher 接口的publishEvent()这个方法在AbstractApplicationContext类中被实现
> >
> >   实际是通过ApplicationEventMulticaster来广播出去的
> >
> >   ```java
> >   @FunctionalInterface
> >   public interface ApplicationEventPublisher {
> >       default void publishEvent(ApplicationEvent event) {
> >           this.publishEvent((Object)event);
> >       }
> >                                 
> >       void publishEvent(Object var1);
> >   }
> >   ```
> >
> > ---
> >
> > **6.模板模式 **
> >
> > 一个操作中的算法的骨架，而将一些步骤延迟到子类中。 
> >
> > 模板方法使得子类可以不改变一个算法的结构即可重定义该算法的某些特定步骤的实现方式。
> >
> > Spring 中 jdbcTemplate、hibernateTemplate 等以 Template 结尾的对数据库操作的类，它们就使用到了模板模式。一般情况下，我们都是使用继承的方式来实现模板模式，但是 Spring 并没有使用这种方式，而是使用Callback 模式与模板方法模式配合，既达到了代码复用的效果，同时增加了灵活性。
> >
> > ---
> >
> > ### 概括总结：
> >
> > 工厂设计模式 : Spring使用工厂模式通过 BeanFactory、ApplicationContext 创建 bean 对象。
> > 代理设计模式 : Spring AOP 功能的实现。
> > 单例设计模式 : Spring 中的 Bean 默认都是单例的。
> > 模板方法模式 : Spring 中 jdbcTemplate hibernateTemplate 等以 Template 结尾的对数据库操作的类，它们就使用到了模板模式。
> > 观察者模式: Spring 事件驱动模型就是观察者模式很经典的一个应用。
> > 适配器模式 :Spring AOP 的增强或通知(Advice)使用到了适配器模式、spring MVC 中也是用到了适配器模式适配Controller。
> > 装饰者(包装器)设计模式 : 我们的项目需要连接多个数据库，而且不同的客户在每次访问中根据需要会去访问不同的数据库。这种模式让我们可以根据客户的需求能够动态切换不同的数据源。
> >
> > ---
> >
> > 装饰者模式和适配器模式都是包装模式（Wrapper Pattern），装饰者模式是一种特殊的代理模式，二者对比如下：
> >
> > |      |          装饰者模式          |                          适配器模式                          |
> > | :--: | :--------------------------: | :----------------------------------------------------------: |
> > | 形式 |       非常特别的适配器       |              没有层级关系，装饰者模式有层级关系              |
> > | 定义 | 装饰者和被装饰着实现同一接口 | 适配器和被适配这没有必然的关系，通常采用继承或代理的形式进行包装 |
> > | 关系 |         满足is-a关系         |                        满足has-a关系                         |
> > | 功能 |        注重覆盖、扩展        |                        注重兼容、转换                        |
> > | 设计 |           前置考虑           |                           后置考虑                           |

## **2.面向切面AOP**  

**目的是业务逻辑与系统服务分开**

> 将一些公共逻辑(例如日志，事务管理等)封装成切面**@aspect** 跟业务代码进行分开 减少系统重复代码以及降低模板之间的耦合度
>
> **AOP：**
>
> 1. Aspect(切面): 是通知和切入点的结合,通知和切入点共同定义了关于切面的全部内容—它的功能、在何时和何地完成其功能
> 2. joinpoint(连接点):所谓连接点是指那些被拦截到的点。在spring中,这些点指的是方法,因为spring只支持方法类型的连接点.
> 3. Pointcut(切入点):所谓切入点是指我们要对哪些joinpoint进行拦截的定义.（何地）
>
> **Spring框架提供以下几种类型的通知：**
>
> 1. 前置通知：先执行方面功能再执行目标功能
> 2. 后置通知：先执行目标功能再执行方面功能（目标无异常才执行方面）
> 3. 最终通知：先执行目标功能再执行方面功能(目标功能有无异常都执行方面)
> 4. 异常通知：先执行目标，抛出后执行方面
> 5. 环绕通知：先执行方面强制部分，然后执行目标，最后再执行方面后置部分
>
> ```java
> /*可以按照下面的try...catch...finally结构来理解/*/        
> 		try {
> //            前置通知-执行部分
> //            环绕通知前置部分
> //            环绕目标组件方法
> //            环绕通知后置部分
> //            后置通知执行部分
>         }catch(){
> //            异常通知执行部分
>         }finally {
> //            最终通知执行部分
> 
>         }
> ```
>
> 实现方式有两种 **静态代理和动态代理**
>

### **静态代理**：

代理类编译阶段生成 编译时增强 AspectJ就是静态代理  简单实现如下：

> ```java
>public class ProxyTest implements TestInterface {
>     //也实现目标接口，但是还包含目标对象的引用。
>    TestInterface Interface;
>     ProxyTest(TestInterface testInterface){
>         this.Interface=testInterface;
>     }
>    @Override
>     public void s_out() {
>        System.out.println("切面方法a");
>         this.Interface.s_out();//目标类的目标方法 (横向业务流：对应示意图的方法5();
>         System.out.println("切面方法f");
>     }
> }
> class ProxyTestMain{
>    public static void main(String[] args) {
>         //横向业务流：方法1();
>         TestInterface face = new ProxyTest(new TestObject());
>         face.s_out();///代理对象来代理目标对象，执行目标方法。
>         //横向业务流：方法7();
>     }
> }
> class TestObject implements TestInterface {
>     @Override//实现目标接口
>     public void s_out() {
>         System.out.println("实现方法");
>     }
> }
> interface TestInterface {
>     void s_out();//定义目标方法
> }
>```
> 
>**实现步骤：**
> 
>![](https://img-blog.csdn.net/20161009162557378)
> 
> ```java
> //完整案例
> interface TestInterface {//接口定义抽象想做的事 比如说批发钟薛糕
>     float initPrice =2;//单件钟薛糕成本原料价
>     float Initial(int count);//定义批发的这件事
> }
> class TestObject implements TestInterface {//商家最先实现生产
>     //实现接口 已知厂家的单件成本价2
>     float Price = initPrice + 5;//加价五元做批发
>     @Override//实现目标接口批发方法
>     public float Initial(int count) {
>         System.out.println("商家：");
>         System.out.println("我这里批发单件钟薛糕"+Price+"元");
>         System.out.println("你在我这批发了"+count+"件");
>         System.out.println("收你"+Price *count+"元");
>         System.out.println("实际上我赚取了"+(Price-initPrice)*count+"件");
>         return Price *count;
>     }
> }
> public class ProxyTest extends TestObject implements TestInterface {//开超市
>     float Price = super.Price+ 5;//加价五元做零售
>     //也实现目标接口，但是还包含目标对象的引用。
>     TestInterface Interface;
>     ProxyTest(TestInterface testInterface){//找到联系厂家的方式
>         this.Interface=testInterface;
>     }
>     @Override//实现目标接口批发方法
>     public float Initial(int count) {
>         //切面方法a();
>         System.out.println("超市：");
>         System.out.println("我这里卖单件钟薛糕"+Price+"元");
>        System.out.println("你在我这买了"+count+"件");
>         System.out.println("收你"+Price *count+"元");
>        System.out.println("实际上我赚取了"+5*count+"元");
>         //切面方法f();
>        return Price *count;
>     }
> }
> class ProxyTestMain{
>     public static void main(String[] args) {
>         System.out.println("买多少根钟薛糕？？");
>         Scanner scanner = new Scanner(System.in);
>         int count = scanner.nextInt();
>         System.out.println("每卖"+count+"跟钟薛糕产生的数据：");
>         TestObject testObject = new TestObject();
>         testObject.Initial(count);
>         //横向业务流：方法1();
>         TestInterface face = new ProxyTest(testObject);//开了个超市做代理 参数是商家
>         face.Initial(count);///代理对象来代理目标对象，执行目标方法。
>         //横向业务流：方法7();
>     }
> }
> /**买多少根钟薛糕？？
> 10
> 每卖10跟钟薛糕
> 商家：
> 我这里批发单件钟薛糕7.0元
> 你在我这批发了10件
> 收你70.0元
> 实际上我赚取了50.0件
> 超市：
> 我这里卖单件钟薛糕12.0元
> 你在我这买了10件
> 收你120.0元
> 实际上我赚取了50元**/
> ```
> 

### **动态代理：**

> 代理类运行时创建 aop框架不会修改字节码 在内存中临时生成一个代理对象 在运行期间对业务进行增强 不会产生新的类
>
> 而Spring AOP是基于**动态代理**的，基于两种动态代理机制： **JDK动态代理**和**CGLIB动态代理**
>

####  **JDK动态代理**：

> **目标类如果实现了接口 SpringAOP会自动采用JDK动态代理方式代理目标类**
>
> - 动态代理类跟目标类实现的接口动态生成 无需编写 
>
> - 生成的目标类和动态代理类都实现同样的
> 
> - JDK动态代理的核心是java.lang.reflect(反射包)里面有三个类：InvocationHandler, Method, Proxy
>
> - 没有实现接口就无法使用JDK动态代理
>
>   ```java
>   //JDK动态代理实例
>   public class ServiceProxy {
>   /**
>    * 基于接口的动态代理
>   * 对于一些需要重复执行的验证功能或下一步操作,
>    * 在核心方法执行前后都会执行增强的功能
>    */
>       public static Object newProxyInstance(Object target){
>       return Proxy.newProxyInstance(target.getClass().getClassLoader(),target.getClass().getInterfaces(), (proxy, method, args) -> {
>           System.out.println("动态增强功能1:登录权限认证");
>           System.out.println("动态增强功能2:黑名单验证");
>           System.out.println("----------------------");
>           Object invoke = method.invoke(target, args);//执行被代理的核心业务功能
>           System.out.println("----------------------");
>           System.out.println("动态增强功能3:进入订单中心");
>           return invoke;
>       });}}
>   interface UserServiceTest {//User业务方法
>       void testUserService();
>   }
>    @Service
>   class UServiceImpl implements UserServiceTest {//User业务方法实现
>      @Override
>       public void testUserService() {
>          System.out.println("User核心功能业务Service");
>       }
>   }
>   interface OrderServiceTest {//Order业务方法
>       void testOrderService();
>   }
>   @Service
>   class OServiceImpl implements OrderServiceTest {//Order业务方法实现
>       @Override
>       public void testOrderService() {
>           System.out.println("Order核心功能业务Service");
>       }
>   }
>   class ServiceProxyTest{//Test类
>       public static void main(String[] args) {
>           UserServiceTest userService= new UServiceImpl();
>           userService = (UserServiceTest)ServiceProxy.newProxyInstance(userService);
>           userService.testUserService();
>           System.out.println("==========================");
>           OrderServiceTest orderService=new OServiceImpl();
>           orderService = (OrderServiceTest)ServiceProxy.newProxyInstance(orderService);
>           orderService.testOrderService();
>       }
>   }
>   /**动态增强功能1:登录权限认证
>   动态增强功能2:黑名单验证
>   ----------------------
>   User核心功能业务Service
>   ----------------------
>   动态增强功能3:进入订单中心
>   ==========================
>   动态增强功能1:登录权限认证
>   动态增强功能2:黑名单验证
> ----------------------
>   Order核心功能业务Service
>  ----------------------
>   动态增强功能3:进入订单中心**/
>  ```
> 

#### **CGLIB动态代理：**

> **如果目标类没有实现接口 SpringAOP会自动采用CGLIB动态代理方式代理目标类**
>
> - 通过继承实现
>
> - 运行时动态生成类的字节码 动态创建目标类子类对象 在子类对象中增强目标类
> 
> - 无需实现特定接口 更加灵活
>
>   ```java
>    //CGLIB动态代理实例
>   public class CGLIBProxy {//CGLIB动态代理类
>       public static Object newProxyInstance(Object target) {
>           //1.工具类
>           Enhancer enhancer = new Enhancer();
>           //2.设置父类,传递类对象
>          enhancer.setSuperclass(target.getClass());
>           //3.设置回调函数
>           enhancer.setCallback((MethodInterceptor) (o, method, objects, methodProxy) -> {
>               System.out.println("cglib增强功能1");
>               System.out.println("cglib增强功能2");
>               System.out.println("-------------");
>               return method.invoke(target, objects);
>           });
>           //4.功能增强后，返回代理对象
>           return enhancer.create();
>       }
>   }
>   class UserServiceCGLIB{
>       public void testUserService() {
>           System.out.println("User核心功能业务Service");
>       }
>    }
>   class OrderServiceCGLIB {
>      public void testOrderService() {
>           System.out.println("Order核心功能业务Service");
>      }
>   }
>   class CGLIBTest {
>       public static void main(String[] args) {
>           UserServiceCGLIB us_cglib = new UserServiceCGLIB();
>           us_cglib= (UserServiceCGLIB)CGLIBProxy.newProxyInstance(us_cglib);
>           us_cglib.testUserService();
>           System.out.println("======================");
>           OrderServiceCGLIB os_cglib=new OrderServiceCGLIB();
>           os_cglib=(OrderServiceCGLIB)CGLIBProxy.newProxyInstance(os_cglib);
>           os_cglib.testOrderService();
>       }
>   }
>   /**cglib增强功能1
>   cglib增强功能2
>   -------------
>   User核心功能业务Service
>   ======================
>   cglib增强功能1
>   cglib增强功能2
>   -------------
>   Order核心功能业务Service**/
>   ```

-----------------------

---

# SpringBoot

1. 简化配置，SpringBoot的核心思想就是**约定大于配置**，省去xml配置

2. 简化部署，内置Tomcat，可以快速启动应用，以jar包的形式

3. 简化依赖，开发web应用，我们只需要在pom文件中添加如下一个 starter-web 依赖即可

   ```java
   <dependency>
       <groupId>org.springframework.boot</groupId>
       <artifactId>spring-boot-starter-web</artifactId>
   </dependency>
   ```

---

## Springboot的核心注解

**@SpringBootApplication ** 包含如下组合注解

- **@SpringBootConfiguration**：声明当前类是SpringBoot应用的配置类 又包括：

  @Configuration **主类上使用的注解** 等同于spring的XML<beans></beans>配置文件 指出该类是 **Bean 配置的信息源**

  @Bean 在**方法上使用的注解** 等同于<bean></bean> **声明一个Bean并且交给Spring管理**

  @ComPonent 声明 泛指各种组件 类不属于各种归类时(Controller services Repository等) 就用该注解标记此类

- **@EnableAutoConfiguration**：开启自动配置 也可以通过exclude属性关闭某个自动配置的Class

  ```yaml
  如关闭数据源自动配置功能： @SpringBootApplication(exclude = { DataSourceAutoConfiguration.class })；
  ```

  @AutoConfiggurationPackage 保存标注相关注解的类的所在包路径 使用一个BasePackage类保存路径 使用@Import注解将其注入到ioc容器中 < @Import(AutoConfiguartionPackages.Registrar.Class) >

  @Import 用来**导入其他配置类 **<@Import (AutoConfiguartionImportSelector.Class)>

- **@ComponentScan**：扫描Spring组件 通过**basePackageClasses**或者**basePackages**属性来指定要扫描包的路径 不指定我就扫自己包以及子包

- @ImportResource 加载xml配置文件

- @Autowired 自动注入依赖的bean 通过类型bytype方式 自动装配属性方法

- @Resource 默认byName方式注入 

---

## Starters

stater作用就是加载项目启动所需要的的相关jar包，不用去一个个找jar包pom了，一键式 只需要添加对应依赖即可。

---

## SpringBoot容器功能

### 1.组件添加 

- @Configuration  配置类 == 配置文件 **默认单例Full模式** 配置类本身也是组件

  属性 proxyBeanMethods 

  **Full模式**：`@Configuration(proxyBeanMethods = true)` 保证@Bean组件多少次使用返回都是单实例
  **Lite模式**：`@Configuration(proxyBeanMethods = false)  `保证@Bean组件多少次使用返回都是新建的

- @Bean 给容器中添加组件。以方法名作为组件的id。返回类型就是组件类型。返回的值，就是组件在容器中的实例。

- @ComponentScan Spring 组件扫描
- @Import 导入其他配置类
- @Conditional 条件装配

### 2.原生配置文件引入

- @ImportResource 导入原生配置文件 `@ImportResource("classpath:beans.xml")`

### 3.配置绑定 

读取properties文件内容 并封装到 JavaBean 中 供随时使用

- @ConfigurationProperties + @EnableConfigurationProperties
- @Component + @Configurationproperties

---

## 异常处理

- 在Controller方法中使用 @ExceptionHandler 处理**局部异常 **controller外的异常无法处理
- 使用@ControllerAdvice + @ExceptionHandler 注解处理**全局异常**（开发中常用）
- 配置 **SimpleMappingExceptionResolver** 类处理异常
- 实现 **HandlerExceptionResolver** 接口处理异常

---

## 事务   <Transactional>

- **声明式事务**： 通过**<u>AOP面向切面</u>**在方法前开启事务 方法后**提交**或**回滚 **通常用用配置文件或注解**@Transactional**控制事务
- **编程式事务**：**手动** 开启、提交、回滚事务。

操作：事务提交 or 事务回滚

```yaml
#example小明给如花转账：
开启事务--- 1.从小明的账户扣除1000块 2.给如花的账户增加1000块
事务提交--- 以上两步骤任意一个步骤出现问题 都会导致事务回滚
通俗来讲 从搭讪到结婚就是事务提交，女方要求男方重新追求她一次，就是事务回滚。
```

### 事务的四大特性 

1. **原子性(Atomicity):**事务中所有操作是不可分割的原子单位。事务中所有操作要么全部执行成功，要么全部执行失败。
2. **一致性(Consistency):**事务执行后，数据库状态与其它业务规则保持一致。如转正业务，无论事务执行成功与否，参与转账的两个账号余额之和应该是不变的。
3. **隔离性(Isolation):**隔离性是指在并发操作中，不同事务之间应该隔离开来，使每个并发中的事务不会相互干扰。
4. **持久性(Durability):**一旦事务提交成功，事务中所有的数据操作都必须被持久化到数据库中，即使提交事务后，数据库马上崩溃，在数据库重启时，也必须你能保证通过某种机制恢复数据。

### 事务的传播特性

指的就是当一个事务方法被另一个事务方法调用时，这个事务方法应该**如何进行**。

spring总共给出了7种事务传播特性：

1.**死活不要事务的**

- propagation_never: 没有就非事务执行，有就抛出异常。
- propagation_not_supported: 没有就非事务执行，有就直接挂起，然后非事务执行。

2.**可有可无**

- propagation_supports: 有就用，没有就算了

3.**必须有事务的**

- propagation_requires_new: 有没有都新建事务，如果原来有，就将原来的挂起。**里面的事务，和外面事务是完全隔离的，互不影响的，外面事务不影响里面的事务，里面的事务也不影响外面的事务。**

- propagation_nested: 如果没有，就新建一个事务，如果有，就在当前事务中嵌套其他事务。**外面的事务回滚的时候会影响里面的事务，但是，里面的事务不影响外面的事务。**
- propagation_requered: 如果没有，就新建一个事务，如果有，就加入当前事务。
- propagation_mandatory: 如果没有，就抛出异常，如果有，就使用当前事务。

### 事务的隔离级别

数据库事务的隔离级别**由低到高**有4种，

1. Read uncommitted(**读未提交**)  一个事务可以读取另一个未提交事务的数据，会产生**脏读**。
2. Read committed(**读已提交**) 一个事务要等另一个事务提交后才能读取数据，会产生**不可重复读**。
3. Repeatable read(**可重复**）就是在开始读取数据(事务开启)时，不再允许修改操作。可能会产生**幻读**。
4. Serializable(**可串行化**)  **最高的事务隔离级别**  可以**避免脏读，不可重复读、与幻读**。效率低下 一般不使用。

```yaml
#数据库默认隔离等级知识
Sql Server Oracle ：读已提交 Read committed
Mysql ：可重复 Repeatable read
```

*在事务的**并发操作中**可能会出现**脏读**，**不可重复读**、**幻读**、**事务丢失**。*

**脏读**：读取了未提交的新事物，然后被回滚了

**不可重复读**：读取了提交的新事务，指更新操作

**幻读**：也是读取了提交的新事务，指增删操作

**事务丢失**：

- 回滚丢失

A和B同时在执行一个数据，然后B事务已经提交了，然后A事务回滚了，这样B事务的操作就因A事务回滚而丢失了。

- 提交覆盖丢失

A和B一起执行一个数据，两个同时取到一个数据，然后，B事务首先提交，但是，A事务接下来又提交，这样就覆盖了B事务。

### **事务总结**

- 读未提交：别人改数据的事务尚未提交，我在我的事务中也能读到。
- 读已提交：别人改数据的事务已经提交，我在我的事务中才能读到。
- 可重复读：别人改数据的事务已经提交，我在我的事务中也不去读。
- 串行：我的事务尚未提交，别人就别想改数据。
- 这4种隔离级别，并行性能依次降低，安全性依次提高。

---

## *Spring Boot自动配置原理？*

Spring Boot通过@EnableAutoConfiguration注解开启自动配置，对jar包下的META-INF/spring.factories文件进行扫描，这个文件中包含了可以进行自动配置的类，当满足@Condition注解指定的条件时，便在依赖的支持下进行实例化，注册到Spring容器中。

简单点说以上过程就是：getCandidateConfigurations()方法通过SpringFactoriesLoader加载器加载META-INF/spring.factories文件——>通过这个文件获取到每个配置类的url——>通过这些url将它们封装成Properties对象——>解析内容存于Map<String,List>中——>通过loadFactoryNames传递过来的class名称作为Key从Map中获得该类的配置列表——>getCandidateConfigurations（）方法获取到了配置类并存于List中——>通过selectImports（）方法返回一个自动配置类的全限定名数组。配置类需要在满足@Condition后才能真正的被注册到Spring容器之中。

**<u>如何在SpringBoot启动的时候运行一些特定的代码？</u>**

可以实现接口**ApplicationRunner**或者**CommandLineRunner**的run()方法

## *Spring  MVC 的处理流程？*

1. **DispatcherServlet** 前端处理器处理收到请求
2. 请求 **HandlerMapping** 找出容器中被 @Controler 注解修饰的 Bean 以及被 @RequestMapping 修饰的方法和类 生成 **Handler 和 HandlerInterceptor** 并返回一个**处理器执行链**。
3. 之后 DispatcherServlet **使用 Handler 找到对应的 HandlerApapter**，通过 HandlerApapter 调用 Handler的方法，**将请求参数绑定到方法的形参上**，执行方法处理请求并得到 ModelAndView。
4. 最后 DispatcherServlet 根据使用 ViewResolver 视图解析器对得到的 ModelAndView 逻辑视图进行解析得到 View 物理视图，然后对视图渲染，将数据填充到视图中并返回给客户端。

## *Spring事务失效问题?*

Spring事务：数据库对**事务 <u>@Transactional</u> **的支持

1. 获取连接 Connection con = DriverManager.getConnection()
2. 开启事务con.setAutoCommit(true/false);
3. 执行CRUD
4. 提交事务/回滚事务 con.commit() / con.rollback();
5. 关闭连接 conn.close();

失效原因:

- 数据库引擎不支持事务

Spring事务生效的前提是连接的数据库底层要支持事务 

例如 Mysql默认引擎MyISAM就不支持事务 InnoDB和BDB就支持事务

- 事务方法未被Spring管理

事务方法所在的类没有加载到Spring IOC容器中 没有被加载为Bean 即没有被Spring管理

```java
public class ProductService {
 @Autowired
 private ProductDao productDao;
 
 @Transactional(propagation = Propagation.REQUIRES_NEW)
 public void updateProductStockCountById(Integer stockCount, Long id){
  productDao.updateProductStockCountById(stockCount, id);
 }
}
//ProductService类上没有标注@Service注解，Product的实例没有加载到Spring IOC容器中
```

- 方法没有被public修饰

如果事务所在的方法没有被public修饰，此时Spring的事务会失效  Spring 官方文档规定

- 同一类中方法调用

自身调用问题 同一个类中的两个方法分别为A和B，方法A上没有添加事务注解，方法B上添加了 @Transactional事务注解，方法A调用方法B，则方法B的事务会失效

- 未配置事务管理器

如果在项目中没有配置Spring的事务管理器，即使使用了Spring的事务管理功能，Spring的事务也不会生效。

```java
//未在配置类配置如下代码
@Bean
public PlatformTransactionManager transactionManager(DataSource dataSource) {
 return new DataSourceTransactionManager(dataSource);
}
```

- 不正确的捕获异常

把异常吃了，然后又不抛出来，事务怎么回滚吧！ 

```java
@Service
public class OrderService {
 @Autowired
 private OrderDao orderDao;
 @Autowired
 private ProductDao productDao;
 @Transactional(propagation = Propagation.REQUIRED)
 public void submitOrder(){
  //生成订单
  Order order = new Order();
  long number = Math.abs(new Random().nextInt(500));
  order.setId(number);
  order.setOrderNo("order_" + number);
  orderDao.saveOrder(order);
  //减库存
  this.updateProductStockCountById(1, 1L);
 }
 
 @Transactional(propagation = Propagation.REQUIRED)
 public void updateProductStockCountById(Integer stockCount, Long id){
  try{
   productDao.updateProductStockCountById(stockCount, id);
   int i = 1 / 0;
  }catch(Exception e){
   logger.error("扣减库存异常:", e.getMesaage());
  }}}
```

updateProductStockCountById()方法中使用try-catch代码块捕获了异常，即使updateProductStockCountById()方法内部会抛出异常，但也会被catch代码块捕获到，此时updateProductStockCountById()方法的事务会提交而不会回滚，并且submitOrder()方法的事务会提交而不会回滚，这就造成了Spring事务的回滚失效问题。

- 错误的标注异常类型

```java
@Transactional(propagation = Propagation.REQUIRED)
public void updateProductStockCountById(Integer stockCount, Long id){
 try{
  productDao.updateProductStockCountById(stockCount, id);
 }catch(Exception e){
  logger.error("扣减库存异常:", e.getMesaage());
  throw new Exception("扣减库存异常");
 }
}
```

因为Spring中对于默认回滚的事务异常类型为RuntimeException，上述代码抛出的是Exception异常。即事务回滚会失效

解决方法：手动指定标注的事务异常类型

```java
@Transactional(propagation = Propagation.REQUIRED,rollbackFor = Exception.class)
//Spring事务注解@Transactional中的rollbackFor属性可以指定 Throwable 异常类及其子类。
```

---

---

# 容器集合

Java中集合框架被设计成要满足以下几个目标。

- 该框架必须是高性能的。基本集合（动态数组，链表，树，哈希表）的实现也必须是高效的。
- 该框架允许不同类型的集合，以类似的方式工作，具有高度的互操作性。
- 对一个集合的扩展和适应必须是简单的。

为此，整个集合框架就围绕一组标准接口而设计。你可以直接使用这些接口的标准实现，诸如： **LinkedList**, **HashSet**, 和 **TreeSet** 等,除此之外你也可以通过这些接口实现自己的集合。

![img](https://www.runoob.com/wp-content/uploads/2014/01/2243690-9cd9c896e0d512ed.gif)

从上面的集合框架图可以看到，Java 集合框架主要包括两种类型的容器，**一种是集合（Collection）**，存储一个元素集合，**另一种是图（Map）**，存储键/值对映射。**Collection 接口又有 3 种子类型，List、Set 和 Queue，**再下面是一些抽象类，最后是具体实现类，常用的有 <u>ArrayList、LinkedList、HashSet、LinkedHashSet、HashMap、LinkedHashMap</u> 等等。

集合框架是一个用来代表和操纵集合的统一架构。所有的集合框架都包含如下内容：

- **接口：**是代表集合的抽象数据类型。例如 Collection、List、Set、Map 等。之所以定义多个接口，是为了以不同的方式操作集合对象
- **实现（类）：**是集合接口的具体实现。从本质上讲，它们是可重复使用的数据结构，例如：ArrayList、LinkedList、HashSet、HashMap。
- **算法：**是实现集合接口的对象里的方法执行的一些有用的计算，例如：搜索和排序。这些算法被称为多态，那是因为相同的方法可以在相似的接口上有着不同的实现。

除了集合，该框架也定义了几个 Map 接口和类。Map 里存储的是键/值对。尽管 Map 不是集合，但是它们完全整合在集合中。

**集合框架体系如图所示**：

![img](https://www.runoob.com/wp-content/uploads/2014/01/java-coll-2020-11-16.png)

## 集合接口

集合框架定义了一些接口。本节提供了每个接口的概述：

| 序号 | 接口描述                                                     |
| :--- | :----------------------------------------------------------- |
| 1    | **Collection 接口** ：Collection 是最基本的集合接口，一个 Collection 代表一组 Object，即 Collection 的元素, Java不提供直接继承自Collection的类，只提供继承于的子接口(如List和set)。Collection 接口存储一组不唯一，无序的对象。 |
| 2    | **List 接口：** List接口是一个有序的 Collection，使用此接口能够精确的控制每个元素插入的位置，能够通过索引(元素在List中位置，类似于数组的下标)来访问List中的元素，第一个元素的索引为 0，而且允许有相同的元素。List 接口存储一组不唯一，有序（插入顺序）的对象。 |
| 3    | **Set：** Set 具有与 Collection 完全一样的接口，只是行为上不同，Set 不保存重复的元素。Set 接口存储一组唯一，无序的对象。 |
| 4    | **SortedSet：** 继承于Set保存有序的集合。                    |
| 5    | **Map：** Map 接口存储一组键值对象，提供key（键）到value（值）的映射。 |
| 6    | **Map.Entry：** 描述在一个Map中的一个元素（键/值对）。是一个 Map 的内部接口。 |
| 7    | **SortedMap：** 继承于 Map，使 Key 保持在升序排列。          |
| 8    | **Enumeration**： 这是一个传统的接口和定义的方法，通过它可以枚举（一次获得一个）对象集合中的元素。这个传统接口已被迭代器取代。 |

### Set和List的区别

1. Set 接口实例存储的是无序的，不重复的数据。List 接口实例存储的是有序的，可以重复的元素。
2. Set 检索效率低下，删除和插入效率高，插入和删除不会引起元素位置改变 **<实现类有HashSet,TreeSet>**。
3. List 和数组类似，可以动态增长，根据实际存储的数据的长度自动增长 List 的长度。查找元素效率高，插入删除效率低，因为会引起其他元素位置改变 **<实现类有ArrayList,LinkedList,Vector>** 。

## 集合实现类（集合类）

Java提供了一套实现了Collection接口的标准集合类。其中一些是具体类，这些类可以直接拿来使用，而另外一些是抽象类，提供了接口的部分实现。

标准集合类汇总于下表：

| 序号 | 类描述                                                       |
| :--- | :----------------------------------------------------------- |
| 1    | **AbstractCollection**  实现了大部分的集合接口。             |
| 2    | **AbstractList**  继承于AbstractCollection 并且实现了大部分List接口。 |
| 3    | **AbstractSequentialList**  继承于 AbstractList ，提供了对数据元素的链式访问而不是随机访问。 |
| 4    | [LinkedList](https://www.runoob.com/java/java-linkedlist.html) 该类实现了List接口，允许有null（空）元素。主要用于创建链表数据结构，该类没有同步方法，如果多个线程同时访问一个List，则必须自己实现访问同步，解决方法就是在创建List时候构造一个同步的List。例如：`List list=Collections.synchronizedList(newLinkedList(...));`LinkedList 查找效率低。 |
| 5    | [ArrayList](https://www.runoob.com/java/java-arraylist.html) 该类也是实现了List的接口，实现了可变大小的数组，随机访问和遍历元素时，提供更好的性能。该类也是非同步的,在多线程的情况下不要使用。ArrayList 增长当前长度的50%，插入删除效率低。 |
| 6    | **AbstractSet**  继承于AbstractCollection 并且实现了大部分Set接口。 |
| 7    | [HashSet](https://www.runoob.com/java/java-hashset.html) 该类实现了Set接口，不允许出现重复元素，不保证集合中元素的顺序，允许包含值为null的元素，但最多只能一个。 |
| 8    | LinkedHashSet 具有可预知迭代顺序的 `Set` 接口的哈希表和链接列表实现。 |
| 9    | TreeSet 该类实现了Set接口，可以实现排序等功能。              |
| 10   | **AbstractMap**  实现了大部分的Map接口。                     |
| 11   | [HashMap](https://www.runoob.com/java/java-hashmap.html) HashMap 是一个散列表，它存储的内容是键值对(key-value)映射。 该类实现了Map接口，根据键的HashCode值存储数据，具有很快的访问速度，最多允许一条记录的键为null，不支持线程同步。 |
| 12   | TreeMap 继承了AbstractMap，并且使用一颗树。                  |
| 13   | WeakHashMap 继承AbstractMap类，使用弱密钥的哈希表。          |
| 14   | LinkedHashMap 继承于HashMap，使用元素的自然顺序对元素进行排序. |
| 15   | IdentityHashMap 继承AbstractMap类，比较文档时使用引用相等。  |

在前面的教程中已经讨论通过java.util包中定义的类，如下所示：

| 序号 | 类描述                                                       |
| :--- | :----------------------------------------------------------- |
| 1    | Vector 该类和ArrayList非常相似，但是该类是同步的，可以用在多线程的情况，该类允许设置默认的增长长度，默认扩容方式为原来的2倍。 |
| 2    | Stack 栈是Vector的一个子类，它实现了一个标准的后进先出的栈。 |
| 3    | Dictionary Dictionary 类是一个抽象类，用来存储键/值对，作用和Map类相似。 |
| 4    | Hashtable Hashtable 是 Dictionary(字典) 类的子类，位于 java.util 包中。 |
| 5    | Properties Properties 继承于 Hashtable，表示一个持久的属性集，属性列表中每个键及其对应值都是一个字符串。 |
| 6    | BitSet 一个Bitset类创建一种特殊类型的数组来保存位值。BitSet中数组大小会随需要增加。 |

## 如何使用迭代器？

通常情况下，你会希望遍历一个集合中的元素。例如，显示集合中的每个元素。

一般遍历数组都是采用for循环或者增强for，这两个方法也可以用在集合框架，但是还有一种方法是采用迭代器遍历集合框架，它是一个对象，实现了[Iterator](https://www.runoob.com/java/java-iterator.html) 接口或 ListIterator接口。

迭代器，使你能够通过循环来得到或删除集合的元素。ListIterator 继承了 Iterator，以允许双向遍历列表和修改元素。

| 序号 | 迭代器方法描述                                               |
| :--- | :----------------------------------------------------------- |
| 1    | [使用 Java Iterator](https://www.runoob.com/java/java-iterator.html) 这里通过实例列出 Iterator 和 ListIterator 接口提供的所有方法。 |

### 遍历 ArrayList

```java
//实例
import java.util.*;
 
public class Test{
 public static void main(String[] args) {
     List<String> list=new ArrayList<String>();
     list.add("Hello");
     list.add("World");
     list.add("HAHAHAHA");
     //第一种遍历方法使用 For-Each 遍历 List
     for (String str : list) {            //也可以改写 for(int i=0;i<list.size();i++) 这种形式
        System.out.println(str);
     }
 
     //第二种遍历，把链表变为数组相关的内容进行遍历
     String[] strArray=new String[list.size()];
     list.toArray(strArray);
     for(int i=0;i<strArray.length;i++) //这里也可以改写为  for(String str:strArray) 这种形式
     {
        System.out.println(strArray[i]);
     }
     
    //第三种遍历 使用迭代器进行相关遍历
     
     Iterator<String> ite=list.iterator();
     while(ite.hasNext())//判断下一个元素之后有值
     {
         System.out.println(ite.next());
     }
 }
}
//解析：
//三种方法都是用来遍历ArrayList集合，第三种方法是采用迭代器的方法，该方法可以不用担心在遍历的过程中会超出集合的长度。
```

### 遍历 Map

```java
//实例
import java.util.*;
 
public class Test{
     public static void main(String[] args) {
      Map<String, String> map = new HashMap<String, String>();
      map.put("1", "value1");
      map.put("2", "value2");
      map.put("3", "value3");
      
      //第一种：普遍使用，二次取值
      System.out.println("通过Map.keySet遍历key和value：");
      for (String key : map.keySet()) {
       System.out.println("key= "+ key + " and value= " + map.get(key));
      }
      
      //第二种
      System.out.println("通过Map.entrySet使用iterator遍历key和value：");
      Iterator<Map.Entry<String, String>> it = map.entrySet().iterator();
      while (it.hasNext()) {
       Map.Entry<String, String> entry = it.next();
       System.out.println("key= " + entry.getKey() + " and value= " + entry.getValue());
      }
      
      //第三种：推荐，尤其是容量大时
      System.out.println("通过Map.entrySet遍历key和value");
      for (Map.Entry<String, String> entry : map.entrySet()) {
       System.out.println("key= " + entry.getKey() + " and value= " + entry.getValue());
      }
    
      //第四种
      System.out.println("通过Map.values()遍历所有的value，但不能遍历key");
      for (String v : map.values()) {
       System.out.println("value= " + v);
      }
     }
}
```

## 如何使用比较器？

TreeSet和TreeMap的按照排序顺序来存储元素. 然而，这是通过比较器来精确定义按照什么样的排序顺序。

这个接口可以让我们以不同的方式来排序一个集合。

| 序号 | 比较器方法描述                                               |
| :--- | :----------------------------------------------------------- |
| 1    | 使用 Java Comparator 这里通过实例列出Comparator接口提供的所有方法 |

## 总结

Java集合框架为程序员提供了预先包装的数据结构和算法来操纵他们。

集合是一个对象，可容纳其他对象的引用。集合接口声明对每一种类型的集合可以执行的操作。

集合框架的类和接口均在java.util包中。

任何对象加入集合类后，自动转变为Object类型，所以在取出的时候，需要进行强制类型转换。

## ArrayList

**ArrayList 继承了 AbstractList.class ，并实现了 List 接口。**<u>非线程安全 动态数组结构 随机访问get/set快 自动扩容1.5倍</u>

![img](https://www.runoob.com/wp-content/uploads/2020/06/ArrayList-1-768x406-1.png)

ArrayList 类是一个可以动态修改的数组，与普通数组的区别就是它是没有固定大小的限制，我们可以添加或删除元素。

```java
//E: 泛型数据类型，用于设置 objectName 的数据类型，只能为引用数据类型,例如一些基本数据类型的包装类和一些常用的引用类型对象。
import java.util.ArrayList; // 引入 ArrayList 类
ArrayList<E> objectName =new ArrayList<>();　 // 初始化
```

## LinkedList

链表（Linked list）是一种常见的基础数据结构，是一种线性表，但是并不会按线性的顺序存储数据，而是在每一个节点里存到下一个节点的地址。

```java
// 引入 LinkedList 类
import java.util.LinkedList; 
LinkedList<E> list = new LinkedList<E>();   // 普通创建方法
//或者
LinkedList<E> list = new LinkedList(Collection<? extends E> c); // 使用集合创建链表
```

<u>非线程安全 双向链表结构 由于移动指针操作 所以插入删除(add/remove)快</u>

与 ArrayList 相比，LinkedList 的增加和删除的操作效率更高，而查找和修改的操作效率较低。

![img](https://www.runoob.com/wp-content/uploads/2020/06/linkedlist-2020-11-16.png)

1. LinkedList 继承了 AbstractSequentialList 类。
2. LinkedList 实现了 Queue 接口，可作为队列使用。
3. LinkedList 实现了 List 接口，可进行列表的相关操作。
4. LinkedList 实现了 Deque 接口，可作为队列使用。
5. LinkedList 实现了 Cloneable 接口，可实现克隆。
6. LinkedList 实现了 java.io.Serializable 接口，即可支持序列化，能通过序列化去传输。

## HashSet

**Hash算法** Hashmap(数组+链表)实现

 **非线程安全** **非有序 ** **元素可以为NULL  但只能有一个** 

HashMap默认初始化容量：16 必须是2的次幂 数组容量达到了3/4(0.75)开始扩容2倍

HashSet 是无序的，即不会记录插入的顺序。

实现对象相等需要重写hashcode()和equals()方法 对象相等必须具有相同散列码

**存取 查找 删除 性能好**

![img](https://www.runoob.com/wp-content/uploads/2020/07/java-hashset-hierarchy.png)

## HashMap

HashMap 是一个散列(hash)表，它存储的内容是键值对(key-value)映射。

JDK1.8以后的HashMap 当链表长度大于阈值（默认为8）时 会将链表转化为红黑树

HashMap 实现了 Map 接口，根据键的 HashCode 值存储数据，具有很快的访问速度，**最多允许一条记录的键为 null**，非线程安全。

HashMap 是无序的，即不会记录插入的顺序。

HashMap 继承于AbstractMap，实现了 Map、Cloneable、java.io.Serializable 接口。![img](https://www.runoob.com/wp-content/uploads/2020/07/WV9wXLl.png)

```java
HashMap<Integer, String> Sites = new HashMap<Integer, String>();
```

## Iterator（迭代器）

Java Iterator（迭代器）不是一个集合，它是一种用于访问集合的方法接口，可用于迭代 [ArrayList](https://www.runoob.com/java/java-arraylist.html) 和 [HashSet](https://www.runoob.com/java/java-hashset.html) 等集合。

![img](https://www.runoob.com/wp-content/uploads/2020/07/ListIterator-Class-Diagram.jpg)

迭代器 it 的两个基本操作是 next 、hasNext 和 remove。

调用 it.next() 会返回迭代器的下一个元素，并且更新迭代器的状态。

调用 it.hasNext() 用于检测集合中是否还有元素。

调用 it.remove() 将迭代器返回的元素删除。

```java
// 引入 ArrayList 和 Iterator 类
import java.util.ArrayList;
import java.util.Iterator;

public class RunoobTest {
    public static void main(String[] args) {
        // 创建集合
        ArrayList<String> sites = new ArrayList<String>();
        sites.add("Google");
        sites.add("Runoob");
        sites.add("Taobao");
        sites.add("Zhihu");
        // 获取迭代器
        Iterator<String> it = sites.iterator();

        // 输出集合中的所有元素
        while(it.hasNext()) {
            System.out.println(it.next());
        }
    }
}
```

## Serializable序列化

Java 提供了一种对象序列化的机制，该机制中，一个对象可以被表示为一个字节序列，该字节序列包括该对象的数据、有关对象的类型的信息和存储在对象中数据的类型。

将序列化对象写入文件之后，可以从文件中读取出来，并且对它进行反序列化，也就是说，对象的类型信息、对象的数据，还有对象中的数据类型可以用来在内存中新建对象。

整个过程都是 Java 虚拟机（JVM）独立的，也就是说，在一个平台上序列化的对象可以在另一个完全不同的平台上反序列化该对象。

请注意，一个类的对象要想序列化成功，必须满足两个条件：

1. 该类必须实现 java.io.Serializable 接口。
2. 该类的所有属性必须是可序列化的。如果有一个属性不是可序列化的，则该属性必须注明是短暂的。

```java
public class Employee implements java.io.Serializable
{
   public String name;
   public String address;
   public transient int SSN;
   public int number;
   public void mailCheck()
   {
      System.out.println("Mailing a check to " + name
                           + " " + address);
   }
}
```

序列化对象:

```java
import java.io.*;
 
public class SerializeDemo
{
   public static void main(String [] args)
   {
      Employee e = new Employee();
      e.name = "Reyan Ali";
      e.address = "Phokka Kuan, Ambehta Peer";
      e.SSN = 11122333;
      e.number = 101;
      try
      {
         FileOutputStream fileOut =
         new FileOutputStream("/tmp/employee.ser");
         ObjectOutputStream out = new ObjectOutputStream(fileOut);
         out.writeObject(e);
         out.close();
         fileOut.close();
         System.out.printf("Serialized data is saved in /tmp/employee.ser");
      }catch(IOException i)
      {
          i.printStackTrace();
      }
   }
}
```

反序列化对象:

```java
import java.io.*;
 
public class DeserializeDemo
{
   public static void main(String [] args)
   {
      Employee e = null;
      try
      {
         FileInputStream fileIn = new FileInputStream("/tmp/employee.ser");
         ObjectInputStream in = new ObjectInputStream(fileIn);
         e = (Employee) in.readObject();
         in.close();
         fileIn.close();
      }catch(IOException i)
      {
         i.printStackTrace();
         return;
      }catch(ClassNotFoundException c)
      {
         System.out.println("Employee class not found");
         c.printStackTrace();
         return;
      }
      System.out.println("Deserialized Employee...");
      System.out.println("Name: " + e.name);
      System.out.println("Address: " + e.address);
      System.out.println("SSN: " + e.SSN);
      System.out.println("Number: " + e.number);
    }
}
Deserialized Employee...
Name: Reyan Ali
Address:Phokka Kuan, Ambehta Peer
SSN: 0
Number:101
```

这里要注意以下要点：

readObject() 方法中的 try/catch代码块尝试捕获 ClassNotFoundException 异常。对于 JVM 可以反序列化对象，它必须是能够找到字节码的类。如果JVM在反序列化对象的过程中找不到该类，则抛出一个 ClassNotFoundException 异常。

注意，readObject() 方法的返回值被转化成 Employee 引用。

当对象被序列化时，属性 SSN 的值为 111222333，但是因为该属性是短暂的，该值没有被发送到输出流。所以反序列化后 Employee 对象的 SSN 属性为 0。



























































## Collection interface <extends Iterable>

- **单列**数据容器

- 实现了**collections**工具类以及**iterator**迭代器
- **Comparable**和**Comparator**对象排序接口

### List<E><interface extends Collection>

**<u>对付顺序的好帮手</u>**

- 拥有专属**Listiterator**迭代器
- 顺序存储 存放时顺序保持一致 可重复

1. **Vector** 线程安全 效率低  底层结构动态数组同Arraylist但是扩容是2倍
2. **ArrayList<典型实现>** 非线程安全 动态数组结构 随机访问get/set快 自动扩容1.5倍
3. **LinkedList** 非线程安全 双向链表结构 由于移动指针操作 所以插入删除(add/remove)快

---

### Set<E><interface extends Collection>

**<u>注重独一无二的性质</u>**

- 无顺序 不可重复元素 否则插入失败
- 判断对象相等使用`equals()`方法不使用 `==`

1.**HashSet<典型实现>**  <Class implements Set>

HashMap默认初始化容量：16 必须是2的次幂 数组容量达到了3/4(0.75)开始扩容2倍

**Hash算法** Hashmap(数组+链表)实现  **非线程安全** **非有序** **元素可以为NULL但只能有一个** 

实现对象相等需要重写hashcode()和equals()方法 对象相等必须具有相同散列码

存取 查找 删除 性能好

- LinkedHashSet   <class implements Set>

<u>**HashSet的子类**</u> 双向链表数据结构和哈希表 插入性能略低于父类 插入时遍历顺序保持一致

2.SortedSet 接口<interface extends Set>  

- 唯一实现类**TreeSet**<extends AbstractSet> 红黑树数据存储结构 默认自然排序(元素大小排序)或者定制排序 遍历保持由小到大 无重复 不允许放入NULL值

---

### Queue

**<u>实现排队功能的叫号机</u>**

按特定的排队规则来确定先后顺序 存储的元素是**有序**的 **可重复的** 

- queue 单向队列 
- deque 双向队列 ArrayDeque顺序表实现   LinkedList链表实现
- PriorityQueue 非线程安全 非NULL 实现了 `Serializable`

### HashSet插入时步骤？

1.先得到对象的hashcode值

2.判断hashcode值是否相等？

3.再比较对象实现的equals()方法

equals和hashcode分两种情况

- equals：false hashcode：ture 保存元素 数组已有位置通过链表链接
- equals：ture hashcode：false 添加元素成功 存储不同位置

### 如何将ArrayList变成线程安全的？

调用Collections工具类中的 static synchronizedList(List list)方法

### ArrayList如何去重？

- 使用HashSet去重 但是会影响元素原有位置 也可以使用LinkedHashSet保持元素原来的顺序

  ```java
  HashSet<String> objects = new HashSet<>(arr1);
  //或LinkedHashSet<Integer> hashSet = new LinkedHashSet<>(arr1);
  ```

- stream()的distinct()方法返回一个由不同数据组成的流 通过对象的equals()方法进行比较 

  ```java
  List<Integer> listWithoutDuplicates = numbersList.stream().distinct().collect(Collectors.toList());
  ```

- List的contains()循环遍历,重新排序,只添加一次数据,避免重复

  ```java
  for (String str : list) {
      if (!result.contains(str)) {
          result.add(str);
      }}
  ```

- 双重for循环去重

  ```java
  for (int i = 0; i < list.size(); i++) { 
      for (int j = 0; j < list.size(); j++) { 
          if(i!=j&&list.get(i)==list.get(j)) { 
              list.remove(list.get(j)); 
       } } }
  ```


---

## Map <interface>

**用 key 来搜索的专家**

- **双列**数据
- 保存具有映射关系的**K-V集合** key和value皆可以是任何类型
- 不允许重复 同一map对象对应对象必须重写hashcode和equlas方法
- JDK1.8以后的HashMap 当链表长度大于阈值（默认为8）时 会将链表转化为红黑树

1.**HashMap<典型实现>** hash散列算法实现 非线程安全 访问快 无序 以存储NULL的k和v 

2.LinkedHashMap 有序按添加顺序  访问慢 双向指针操作 非线程安全

3.TreeMap 按照添加k-v对进行排序 实现排序遍历 自然排序or定制排序 底层红黑树

4.Hashtable 线程安全的  效率低 不能存储null的key和value

5.Properties 常用来处理配置文件 key和value都是String类型 

---

## 枚举<extends ENUM>

特征：

- 无法继承 构造方法为私有 其他与常规类相同
- 不允许使用`=`复制给枚举常量
- enum可以有任意普通 静态 抽象 构造方法
- enum可以实现接口 

 继承自`java.lang.Enum`提供的常用方法  Enum 实现了**Serializable**和**Comparable**接口

- `values()` 数组顺序返回获取枚举类型的成员
- `ordinal()`方法可以找到每个枚举常量的索引，就像数组索引一样。
- `valueOf()`方法返回指定字符串值的枚举常量。

- `name()` 返回实例名
- `getDeclaringClass()` 返回实例所属的enum类型
- `equals()` 判断是否同一对象也可以使用`==`

工具类：

**Enumset**:枚举类型Set高效实现 要求放入它的枚举常量必须属于同一枚举类型

**EnumMap**:枚举类型Map高效实现 只接受同一枚举类型的实例作为键值 使用数组来存放与枚举类型对应的值

---

## 泛型 <E T K V N ?>

泛型是 JDK 5 中引入的一个新特性, 泛型提供了编译时类型安全检测机制，该机制允许程序员在编译时检测到非法的类型。

泛型的本质是参数化类型，也就是说所操作的数据类型被指定为一个参数。

```xml
假定我们有这样一个需求：写一个排序方法，能够对整型数组、字符串数组甚至其他任何类型的数组进行排序，该如何实现？
答案是可以使用 Java 泛型。
使用 Java 泛型的概念，我们可以写一个泛型方法来对一个对象数组排序。然后，调用该泛型方法来对整型数组、浮点数数组、字符串数组等进行排序。
```

**泛型类型在逻辑上看以看成是多个不同的类型，实际上都是相同的基本类型。**

- **E** - Element (在集合中使用，因为集合中存放的是元素)
- **T** - Type（Java 类）
- **K** - Key（键）
- **V** - Value（值）
- **N** - Number（数值类型）
- **？** - 表示不确定的 java 类型

---

## 线程安全的容器有哪些？

**同步容器类：<synchronized>**

- vector 线程安全的list 几乎不用

- HashTable 线程安全的Map 几乎不用

**并发容器**：

- ConcurrentHashMap: 使用较多 效率高(分段/CAS)再加synchronized保证同步操作 手动实现并发安全 用于并发几率低场景 
- CopyOnWriteArrayList：写时复制 常用于读多写少的并发环境
- CopyOnWriteArraySet：写时复制 常用于读多写少的并发环境

**Queue队列：**

- ConcurrentLinkedQueue **非阻塞**的方式实现的**基于链接节点**的**无界**的线程安全队列，性能非常好。
- ArrayBlockingQueue：基于**数组**的**有界阻塞队列**
- LinkedBlockingQueue：基于**链表**的**有界阻塞队列**
- PriorityBlockingQueue：**支持优先级**的**无界阻塞队列** 默认情况下元素自然升序排序

- DelayQueue： 延时获取元素的无界阻塞队列
- SynchronousQueue ：不存储元素的阻塞队列。每个put操作必须等待一个take操作，否则不能继续添加元素。内部其实没有任何一个元素，容量是0

**Deque：双向对列 允许在队列头和尾部进行入队出队操作**

- ArrayDeque:基于数组的双向非阻塞队列。
- LinkedBlockingDeque:基于链表的双向阻塞队列。

**Sorted容器：**

- ConcurrentSkipListMap：是TreeMap的线程安全版本
- ConcurrentSkipListSet：是TreeSet的线程安全版本

# 多线程与并发

## 多线程编程

多线程能满足程序员编写高效率的程序来达到充分利用 CPU 的目的。

Java 给多线程编程提供了内置的支持。 一条线程指的是进程中一个单一顺序的控制流，一个进程中可以并发多个线程，每条线程并行执行不同的任务。

多线程是多任务的一种特别的形式，但多线程使用了更小的资源开销。

## 进程

**执行程序的一次执行过程 也指正在运行的程序实体**

包括这个运行的程序中占据的所有系统资源，比如说CPU（寄存器），IO,内存，网络资源等。

同样一个程序，同一时刻被两次运行了，那么他们就是两个独立的进程。

一个操作系统中可以有多个进程，一个进程可以开启多个线程，其中有一个主线程来调用本进程中的其他线程。

## [线程](https://blog.csdn.net/qq_35598736/article/details/108431422?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522165984936416781432921249%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=165984936416781432921249&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~top_positive~default-2-108431422-null-null.142^v39^pc_rank_v36,185^v2^control&utm_term=%E5%A4%9A%E7%BA%BF%E7%A8%8B&spm=1018.2226.3001.4187)

JVM 执行任务的**运算调度的最小单位** ，它被**包含在进程之中**，一条线程指的是**进程中一个单一顺序的控制流**。

**多线程**可以让同一个进程同时**并发**处理多个任务

JVM中进程的六种状态 这些状态对应 **Thread.State** 枚举类中的状态 `<java.lang.Thread.State>`

1. **`NEW`**  **创建状态**

2. **`RUNNABLE`** **可运行状态**  运行 Thread 的 start 方法后 线程进入可运行状态

   可运行状态线程并不能马上运行   而是先进入**READY就绪状态**等待线程调度 在获取 CPU 后才能进入**RUNNING运行状态**  运行状态可以随着不同条件转换成除 NEW 以外的其他状态

3. **`BLOCKED`**  **阻塞状态** 运行进程进入 synchronized 同步块或同步方法时 获取锁失败 会进入BLOCKED状态 获取到锁后 会从BLOCKED状态恢复到就绪RUNNABLE状态 

4. **`WAITING` ** **等待状态**  wait()操作之后会释放锁 等待其他线程唤醒 获取到锁才能进入可运行状态

5. **`TIMED_WAITING`**  **有时间的等待 **sleep()或者join()操作先进入阻塞状态不会释放锁 时间结束或者等其他线程结束之前一直是属于等待状态

6. **`TERMINATED` ** **线程运行完成结束状态** 或者有异常发生 线程会进入死亡Dead状态

![多线程状态图](https://img-blog.csdnimg.cn/db36e894a0a843c6a36ca5a76cb3af2d.png)

![](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9wNi1qdWVqaW4uYnl0ZWltZy5jb20vdG9zLWNuLWktazN1MWZicGZjcC9lNGI3YTY3YTE2NDQ0NWYzYWE3ZjA1ZWVkNDAyM2I3OH50cGx2LWszdTFmYnBmY3Atem9vbS0xLmltYWdl?x-oss-process=image/format,png)

![对应枚举类状态](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9wNi1qdWVqaW4uYnl0ZWltZy5jb20vdG9zLWNuLWktazN1MWZicGZjcC8zOTlhNzYzODU5MzM0ZDYwOGYzZGMzMDA0NTgzODVlZX50cGx2LWszdTFmYnBmY3Atem9vbS0xLmltYWdl?x-oss-process=image/format,png)

## 并发与并行

**并发（Concurrent）**：一个时间段中有几个程序都处于已启动运行到运行完毕之间，且这几个程序都是在同一个处理机上运行。
同一时刻只能有一条指令执行，但多个进程指令被**快速的轮换执行**，使得在宏观上具有多个进程同时执行的效果，但在微观上并不是同时执行的，只是把**时间分成若干段，使多个进程快速交替的执行**。

**并行（Parallel）：**当系统有一个以上CPU时，当一个CPU执行一个进程时，另一个CPU可以执行另一个进程，两个进程互不抢占CPU资源，可以同时进行**真正的在同一时刻运行**，这种方式我们称之为并行 。

其实决定并行的因素不是CPU的数量，而是**CPU的核心数量**，比如一个CPU多个核也可以并行。

## 进程与线程的关系

- 进程是操作系统资源分配的基本单位，而线程是CPU的基本调度单位
- 一个进程由一个或多个线程(多线程)组成
- 进程之间相互独立，而线程共享所在进程的地址空间和其它资源(自己的栈和栈指针，程序计数器等寄存器)。
- 一个进程中可以并发多个线程，每条线程并行执行不同的任务
- 线程上下文切换比进程上下文切换要快得多

## 多线程的多种创建方式

### 1.继承Thread类 

- 自定义线程类继承 Thread类

- 重写 run() 方法 编写线程执行体
-  创建线程对象 调用 start() 方法启动线程

```java
public class Demo extends Thread {
    @Override
    public void run() {
        for (int i = 0; i < 20; i++) {
            System.out.println("111111111111111");
        }}
    public static void main(String[] args) {
        for (int i = 0; i < 100; i++) {
            Demo demo = new Demo();
            demo.start();  //一般都是调用start方法
            System.out.println("22222222222222222");
     }}}
```

### 2.实现Runnable接口 

- 定义MyRunnable类实现 Runnable 接口
- 实现 run() 方法,编写线程执行体
- 创建线程对象，调用 start() 方法启动线程

```java
//推荐使用 避免单继承的局限性，灵活方便，方便同一个对象被多个线程使用
public class MyRunnable implements Runnable {
    @Override
    public void run() {
        for (int i = 0; i < 20; i++) {
            System.out.println("111111111111111");
        }}
    public static void main(String[] args) {
        for (int i = 0; i < 100; i++) {
            MyRunnable myRunnable = new MyRunnable();
            new Thread(myRunnable).start();
            System.out.println("22222222222222222");
        }}}
```

```java
//龟兔赛跑实例
public class Race implements Runnable {
    private static String winner;
    @Override
    public void run() {
        for (int i = 0; i <= 100; i++) {
            if (Thread.currentThread().getName().equals("兔子")) {
                try {
                    Thread.sleep(10);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
            boolean gameOver = gameOver(i);
            if (gameOver) {
                break;
            }            System.out.println(Thread.currentThread().getName() + "--->跑了" + i);
        }}
    private boolean gameOver(int i) {
        if (winner != null) {
            return true;
        } else {
            if (i >= 100) {
                winner = Thread.currentThread().getName();
                System.out.println(winner + "赢得了比赛");
                return true;
            }
        }
        return false;
    }
    public static void main(String[] args) {
        Race race = new Race();
        new Thread(race, "兔子").start();
        new Thread(race, "乌龟").start();
    }}
```

### 3.实现Callable接口

- 实现Callable接口，需要返回值类型
- 重写call方法，需要抛出异常
- 创建目标对象
- 创建执行服务：`ExecutorService executorService=Executors.newFixedThreadPool();`
- 提交执行：`Future submit = executorService.submit(t1);`
- 获取结果：`boolean r1 = result.get()`
- 关闭服务: `ser.shutdownNow();`

```java
//实例Callable接口了解即可
public class MTImplementsCallable implements Callable {
    @Override
    public Object call() throws Exception {
        //执行线程业务的方法
        for (int i = 0; i < 10; i++) {
            //返回正在执行的线程实例
            Thread thread = Thread.currentThread();
            //getName（）获取当前线程实例的名称
            System.out.println(thread.getName()+"执行打印"+i);
        }
        //获取随机数
        UUID uuid = UUID.randomUUID();
        System.out.println("随机数字符串为："+uuid);
        System.out.println(1/0);
        return uuid;
    }}
```

### 4.使用线程池

```java
public class MTPool implements Runnable {
    @Override
    public void run() {
        //执行线程业务的方法
        for (int i = 0; i < 10; i++) {
            //返回正在执行的线程实例
            Thread thread = Thread.currentThread();
            //getName（）获取当前线程实例的名称
            System.out.println(thread.getName()+"执行打印"+i);
        }}}
//实例化线程类
MTPool mtPool =new MTPool();
//使用Executors创建固定长度为4的线程池
ExecutorService executorService = Executors.newFixedThreadPool(4);
//调用execute启动线程
executorService.execute(mtPool);
```

### 区别

runnable和callable都是执行多线程 方法名分别为run() 和call()

runnable没有返回值 无法获取线程业务方法执行方法 callable正好相反

Runnable方法没有抛出异常 而Callable有异常处理，并且获取异常

继承thread存在局限性 因为一个类只能继承一个父类 故不能用一个实例建立多个线程 只能共享Thread类的static变量

而一个类可以实现多个接口 例如runnable接口使用同一实例创建的多线程变量也是共享的 故实现接口更适合与资源共享

```java
public class SellTicketExtendsThread extends Thread {
    //定义总票数
    private int ticketNum = 20;
    //卖票人姓名
    private String  name;
    /**
     * 构造方法
     * @param name
     */
public SellTicketExtendsThread(String name) {
        this.name = name;
    }
    @Override
public void run() {
         while(ticketNum>0){
             System.out.println(name+"正在卖票，剩余"+(--ticketNum)+"张");
         }}}
public class SellTicketImplementsRunnable  implements Runnable{
    //定义总票数
    private int ticketNum = 20;
    @Override
    public void run() {
        while(ticketNum>0){
            System.out.println(Thread.currentThread().getName()+"正在卖票，剩余"+(--ticketNum)+"张");
        }}}
class Test {
    public static void main(String[] args) {
      /*  SellTicketExtendsThread sellTicketExtendsThread =new SellTicketExtendsThread("马云");
        sellTicketExtendsThread.start();
       *//* sellTicketExtendsThread.start();
        sellTicketExtendsThread.start();*//*
        SellTicketExtendsThread sellTicketExtendsThread1 =new SellTicketExtendsThread("马化腾");
        sellTicketExtendsThread1.start();
        SellTicketExtendsThread sellTicketExtendsThread2 =new SellTicketExtendsThread("刘强东");
        sellTicketExtendsThread2.start();*/
        SellTicketImplementsRunnable sellTicketImplementsRunnable =new SellTicketImplementsRunnable();
        new Thread(sellTicketImplementsRunnable,"马云").start();
        new Thread(sellTicketImplementsRunnable,"马化腾").start();
        new Thread(sellTicketImplementsRunnable,"刘强东").start();
    }}
```

```java 
//多线程匿名(Anonymous)内部类用法
public class Test8_7 {
        public static void main(String[] args) {
            //继承Thread启动线程
            new Thread(){
                @Override
                public void run() {
                    for (int i = 0; i < 10; i++) {
                        //返回正在执行的线程实例
                        Thread thread = Thread.currentThread();
                        //getName（）获取当前线程实例的名称
                        System.out.println(thread.getName()+"执行打印"+i);
                    }}}.start();
            System.out.println("-------------------------------------");
            //实现Runnable
            new Thread(new Runnable() {
                @Override
                public void run() {
                    for (int i = 0; i < 10; i++) {
                        //返回正在执行的线程实例
                        Thread thread = Thread.currentThread();
                        //getName（）获取当前线程实例的名称
                        System.out.println(thread.getName()+"执行打印"+i);
                    }}}).start();
            System.out.println("-------------------------------------");
            //实现Callable
            new Thread(new FutureTask<String>(
                    new Callable<String>() {
                        @Override
                        public String call() throws Exception {
                            for (int i = 0; i < 10; i++) {
                                //返回正在执行的线程实例
                                Thread thread = Thread.currentThread();
                                //getName（）获取当前线程实例的名称
                                System.out.println(thread.getName()+"执行打印"+i);}
                            return null;
                        }})).start();}}
```

## 多线程有哪些方法？

- start()：启动当前线程并调用线程的run()方法
- run() ：线程执行业务的方法
- currentThread():静态方法 返回当前代码执行的线程象的引用
- getName():获取当前线程的名字
- setName():设置当前线程的名字
- getPriority()：获取线程优先级 默认是5如果不手动指定 那么线程优先级具有继承性
- setpriority()：设置线程优先级 cpu会尽量执行优先级高的线程

继承性：相互启动的两个线程具有同样优先级

`MAX_PRIORITY:10`
`MIN_PRIORITY:1`
`NORM_PRIORITY:5`

- interrupt()： 通知线程中断 具体是否中断情况由被通知的线程自己处理

1.如果此时线程被阻塞状态(sleep wait join等) 立刻退出被阻塞状态并且抛出InterruptedException异常

2.如果线程处于正常活动状态 那么线程中断标志设置为ture 仅此而已 被设置中断标志线程继续正常运行 不受影响

即 ：interrupt()并不能真正中断线程 需要被通知的线程同意配合才行

- join() 等待其他线程终止 

在当前线程调用其他线程的join方法时 当前线程进入阻塞状态 直到其他线程运行结束 当前线程才由阻塞状态转换为就绪状态

- yieId() 暂停当前正执行线程 把执行机会给相同或者优先级级别更高的线程
- sleep() 使线程转入到阻塞状态

millis参数设置睡眠时间 默认以毫秒为单位 当睡眠结束线程自动进入Runnable可运行状态

- ~~stop() 强制停止线程 被废弃方法已过时~~
- isAlive():判断当前线程是否还存活

## 锁

### 同步锁

多个取款机 对应**多个锁**里面的现金互不影响 在多个取款机同时取钱也没有影响 每个来取钱的人对应的都是**线程 **在大厅等待取钱对应**线程状态**  轮到取钱者进入取款机锁上门对应**线程获得锁** 完成对应业务取钱后出门对应**线程释放** 下一个取钱者继续竞争锁 银行工作人员对应一个线程发现取款机里面现金不足通知上级 就会对取款机加钱**调用notifyAll方法<唤醒waitSet中所有的线程>** 取钱服务暂停 取钱大厅所有(**调用wait方法**)线程进入堵塞状态

而需要银行工作人员对取款机完成加钱操作也就是需要**工作人员线程获取到取款机锁**后加钱操作完成后通知大厅所以人来取钱对应的也就是上述的**调用notifyAll方法** 

如果取款机里面的人是取款人对应当前获取到锁的不是工作人员线程 因为取款机没钱了则需要释放锁 进入大厅堵塞状态(**调用wait方法**)

大堂里等待的人都来竞争锁，谁获取到谁进入继续取钱

### ReentrantLock

 ReentrantLock是可重入锁： 一个线程获取到对象的锁后，执行方法内部在需要获取锁的时候是可以获取到的。synchronized 也是可重入锁。

优点：

1. 支持获取锁的超时时间
2. 获取锁时可被打断
3. 可设为公平锁
4. 可以有不同的条件变量，即有多个waitSet，可以指定唤醒

### 死锁

是指多个进程在运行过程中因争夺资源而造成的一种僵局，当进程处于这种僵持状态时，若无外力作用，它们都将无法再向前推进。

例如老王 小李两个进程在运行到某一时刻时 都想获取酒和故事两种资源而两人分别持有酒和故事中一个资源 都想要对方手里的

```java
//example
static Beer beer = new Beer();
static Story story = new Story();
public static void main(String[] args) {
    new Thread(() ->{
        synchronized (beer){
            log.info("我有酒，给我故事");
            try {
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            synchronized (story){
                log.info("小王开始喝酒讲故事");
            }
        }
    },"小王").start();
    new Thread(() ->{
        synchronized (story){
            log.info("我有故事，给我酒");
            try {
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            synchronized (beer){
                log.info("老王开始喝酒讲故事");
            }
        }
    },"老王").start();
}
class Beer {
}
class Story{
}
```

如何避免死锁：

1. 避免一个线程同时获取多个锁
2. 避免一个线程在锁内同时占用多个资源，尽量保证每个锁只占用一个资源
3. 尝试使用超时解锁，从而规避无限期等待

### 内存模型<JMM>

1. 原子性 保证指令不会受到上下文切换的影响

   同步锁的synchronized代码块就是保证了原子性，就是**一段代码是一个整体**，原子性保证了线程安全，不会受到上下文切换的影响。

2. 可见性 保证指令不会受到cpu缓存的影响

   ```java
   static boolean run = true;
   public static void main(String[] args) throws InterruptedException {
       Thread t = new Thread(() -> {
           while (run) {
               // ....
           }});
       t.start();
       Thread.sleep(1000);
      // 线程t不会如预想的停下来
       run = false; }
   //线程有自己的工作缓存，当主线程修改了变量并同步到主内存时，t线程没有读取到，所以程序停不下来
   ```

   ![线程有自己的工作缓存，当主线程修改了变量并同步到主内存时，t线程没有读取到，所以程序停不下来](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9wMS1qdWVqaW4uYnl0ZWltZy5jb20vdG9zLWNuLWktazN1MWZicGZjcC9kODg4MDA0ZTBjMmM0N2JhYjExYjhhNjdiZjc4Zjg4ZH50cGx2LWszdTFmYnBmY3Atem9vbS0xLmltYWdl?x-oss-process=image/format,png)

3. 有序性 保证指令不会受并行优化的影响

   JVM在不影响程序正确性的情况下可能会调整语句的执行顺序，该情况也称为 **指令重排序** 。

### **Volatile**

volatile关键字解决了可见性和有序性，不能解决原子性，volatile通过**内存屏障<读/写屏障>**来实现的。

应用场景：一个线程读取变量，另外的线程操作变量，加了该关键字后保证写变量后，读变量的线程可以及时感知。

### **CAS**<compare and swap>

**轻量级 乐观锁的一种实现方式**

线程读数据时不加锁，在写回数据前，比较原值是否修改，未被其他线程修改则写回，若已被修改，则重新执行读取流程。

这是一种**乐观**策略，认为**并发操作**并不总会发生。

比较并写回的操作是通过操作系统原语实现的，保证执行过程中不会被中断，即不使用同步锁也可以保证操作的原子性。

```java
private AtomicInteger balance;
// 模拟cas的具体操作
@Override
public void withdraw(Integer amount) {
    while (true) {
        // 获取当前值
        int pre = balance.get();
        // 进行操作后得到新值
        int next = pre - amount;
        // 比较并设置成功 则中断 否则自旋重试
        if (balance.compareAndSet(pre, next)) {
            break;
        }}}
```

无锁的效率是要高于之前的锁的，由于无锁不会涉及线程的上下文切换

**cas是乐观锁的思想        sychronized是悲观锁的思想**

### 悲观锁与乐观锁？

悲观锁：在对数据进行修改前，先对数据进行加锁。之所以叫悲观锁，就是因为悲观的认为数据被并发修改的概率大，所需需要先加锁再操作

乐观锁：相对于悲观锁而言，乐观锁乐观的认为被修改数据不会发生并发修改问题，**所以乐观锁不会使用锁机制去主动的对数据进行上锁**，而是在数据修改之后，才正式对数据是否冲突进行校验（使用版本号的方式），如果发现了冲突，则提示错误，由用户决定下一步操作（撤销修改或者覆盖等）

### CAS 导致 的 **<u>ABA 问题</u>**

线程O1读取值之后 发生两次写入 由其他线程修改两次后 值没有发生变化 无法判断是否修改 这种操作不一定会影响结果 但是还是需要**增加额外的标志位或者时间戳**的方法来解决这类问题 <u>JUC并发工具包</u>中提供了这样的类 

1. AtomicInteger/AtomicBoolean/AtomicLong
2. AtomicIntegerArray/AtomicLongArray/AtomicReferenceArray
3. AtomicReference/AtomicStampedReference/AtomicMarkableReference

---

## 线程池

**一种管理线程的工具**

### 作用

1. 降低资源消耗，通过池化思想，减少创建线程和销毁线程的消耗，控制资源
2. 提高响应速度，任务到达时，无需创建线程即可运行
3. 提供更多更强大的功能，可扩展性高

```java
//线程池的构造方法
public ThreadPoolExecutor(int corePoolSize,
                          int maximumPoolSize,
                          long keepAliveTime,
                          TimeUnit unit,
                          BlockingQueue<Runnable> workQueue,
                          ThreadFactory threadFactory,
                          RejectedExecutionHandler handler) {}
```

![关系图](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9wOS1qdWVqaW4uYnl0ZWltZy5jb20vdG9zLWNuLWktazN1MWZicGZjcC85ZGFhMDM2NmY4Y2E0YmU4YWY3NWY3MDg2MTliNmQ2Y350cGx2LWszdTFmYnBmY3Atem9vbS0xLmltYWdl?x-oss-process=image/format,png)

| 参数名          | 参数意义                       |
| --------------- | ------------------------------ |
| corePoolSize    | 核心线程数                     |
| maximumPoolSize | 最大线程数                     |
| keepAliveTime   | 救急线程的空闲时间             |
| unit            | 救急线程的空闲时间单位         |
| workQueue       | 阻塞队列                       |
| threadFactory   | 创建线程的工厂，主要定义线程名 |
| handler         | 拒绝策略                       |

### **线程池案例**

1. 客户到银行时，开启柜台进行办理，柜台相当于线程，客户相当于任务，有两个是常开的柜台，三个是临时柜台。2就是核心线程数，5是最大线程数。即有两个核心线程
2. 当柜台开到第二个后，都还在处理业务。客户再来就到排队大厅排队。排队大厅只有三个座位。
3. 排队大厅坐满时，再来客户就继续开柜台处理，目前最大有三个临时柜台，也就是三个救急线程
4. 此时再来客户，就无法正常为其 提供业务，采用拒绝策略来处理它们
5. 当柜台处理完业务，就会从排队大厅取任务，当柜台隔一段空闲时间都取不到任务时，如果当前线程数大于核心线程数时，就会回收线程。即撤销该柜台。

![银行办理业务](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9wMy1qdWVqaW4uYnl0ZWltZy5jb20vdG9zLWNuLWktazN1MWZicGZjcC82YjUxNjM1OGIwNzk0ZTc0ODIyOTQyYjJlMjUyMWIzOH50cGx2LWszdTFmYnBmY3Atem9vbS0xLmltYWdl?x-oss-process=image/format,png)

### 线程池的主要流程

线程池创建、接收任务、执行任务、回收线程的步骤

1. 创建线程池后，线程池的状态是Running，该状态下才能有下面的步骤
2. 提交任务时，线程池会创建线程去处理任务
3. 当线程池的工作线程数达到corePoolSize时，继续提交任务会进入阻塞队列
4. 当阻塞队列装满时，继续提交任务，会创建救急线程来处理
5. 当线程池中的工作线程数达到maximumPoolSize时，会执行拒绝策略
6. 当线程取任务的时间达到keepAliveTime还没有取到任务，工作线程数大于corePoolSize时，会回收该线程

 注意： 不是刚创建的线程是核心线程，后面创建的线程是非核心线程，线程是没有核心非核心的概念的，这是我长期以来的误解。

拒绝策略：

1. 调用者抛出RejectedExecutionException (默认策略)
2. 让调用者运行任务
3. 丢弃此次任务
4. 丢弃阻塞队列中最早的任务，加入该任务

### 线程池的关闭

- shutdown()

会让线程池状态为shutdown，不能接收任务，但是会将工作线程和阻塞队列里的任务执行完 相当于优雅关闭。

```java
public void shutdown() {
    final ReentrantLock mainLock = this.mainLock;
    mainLock.lock();
    try {
        checkShutdownAccess();
        advanceRunState(SHUTDOWN);
        interruptIdleWorkers();
        onShutdown(); // hook for ScheduledThreadPoolExecutor
    } finally {
        mainLock.unlock();
    }
    tryTerminate();
}
```

- shutdownNow()

会让线程池状态为stop， 不能接收任务，会立即中断执行中的工作线程，并且不会执行阻塞队列里的任务， 会返回阻塞队列的任务列表

```java
public List<Runnable> shutdownNow() {
    List<Runnable> tasks;
    final ReentrantLock mainLock = this.mainLock;
    mainLock.lock();
    try {
        checkShutdownAccess();
        advanceRunState(STOP);
        interruptWorkers();
        tasks = drainQueue();
    } finally {
        mainLock.unlock();
    }
    tryTerminate();
    return tasks;
}
```

---

---

# Redis <redis io>

**开源**的、使用**C语言编写**的、支持**网络交互**的、可基于**内存也可持久化的Key-Value数据库**。

redi是一种高级的**key  :  value**存储数据结构 

其中**value支持以下五种数据**：

1.字符串（Strings）
2.字符串列表（Lists）
3.字符串集合（Sets）
4.有序字符串集合（Sorted Sets）
5.哈希（Hashes）

**key的规范使用**：

1.key不能太长 key也不要太短 尽量不要超过1024字节 太长：消耗内存 降低查找效率 太短： key可读性降低

2.key最好使用统一的命名模式，例如user:10000:passwd

**Strings** ：能存储字符串 并且有持久化操作功能 而遇到数值操作指令时 redis会将字符串类型转换成数值并且计算这个特性来实现业务上计数便利。

```yaml
set mystr "hello world!" //设置字符串类型
get mystr //读取字符串类型
set mynum "2"
OK
get mynum 
"2"
incr mynum 
(integer) 3
get mynum 
"3"
```

**Lists**：底层实现上并不是数组，而是**双端链表**









# REST_ful 风格

---

## REST <Resource Representational State Transfer> 

**对资源的访问状态通过url路径的体现出来 一种交互形式或者说模式风格**

**Resource** ：资源 REST架构核心 整个网络处理核心

**Representational** ：资源表达形式 例如 JSON  XML  JPRG

**State Transfer** ：状态变化 通过HTTP Methods实现

**通俗来讲：就是通过URL就知道要什么资源 通过HTTP Methods就知道要干什么实现什么 通过HTTP State Code就知道结果如何**

```yaml
example: 
GET/tasks			// 获取所有任务
POST/tasks 			// 创建新任务
GET/tasks/{id} 		// 通过任务id获取任务
PUT/tasks/{id}		// 通过任务id更新任务
DELETE/tasks/{id} 	// 通过任务id删除任务
- GET       //一次获取资源
- POST      //一次添加资源
- PUT       //一次修改资源
- DELETE  	//一次删除资源
#常见的HTTP State Code 
1xx：指示信息--表示请求已接收，继续处理
2xx：成功--表示请求已被成功接收
3xx：重定向--要完成请求必须进行更进一步的操作
4xx：客户端错误--请求有语法错误或请求无法实现
5xx：服务器端错误--服务器未能实现合法的请求
```

REST_ful 优点：

- 风格统一 易读
- 面向资源 具有解释性
- 充分利用HTTP协议语义





# Web传输核心协议

## HTTP 



## HTTPS















- 

# 算法





>>>>>>> 09f8323f93f3c6296a31f21af9c14a7520624d6b
=======
# JAVA 8 新特征

- Lambda表达式 允许把函数作为一个方法的参数

1. Lambda 表达式，也可称为闭包，它是推动 Java 8 发布的最重要新特性。
2. Lambda 允许把函数作为一个方法的参数（函数作为参数传递进方法中）。
3. 使用 Lambda 表达式可以使代码变的更加简洁紧凑。

```java
//Lambda 表达式实例
// 1. 不需要参数,返回值为 5  
() -> 5  
  
// 2. 接收一个参数(数字类型),返回其2倍的值  
x -> 2 * x  
  
// 3. 接受2个参数(数字),并返回他们的差值  
(x, y) -> x – y  
  
// 4. 接收2个int型整数,返回他们的和  
(int x, int y) -> x + y  
  
// 5. 接受一个 string 对象,并在控制台打印,不返回任何值(看起来像是返回void)  
(String s) -> System.out.print(s)
```

```java
public class Java8Tester {
   public static void main(String args[]){
      Java8Tester tester = new Java8Tester();
        
      // 类型声明
      MathOperation addition = (int a, int b) -> a + b;
        
      // 不用类型声明
      MathOperation subtraction = (a, b) -> a - b;
        
      // 大括号中的返回语句
      MathOperation multiplication = (int a, int b) -> { return a * b; };
        
      // 没有大括号及返回语句
      MathOperation division = (int a, int b) -> a / b;
        
      System.out.println("10 + 5 = " + tester.operate(10, 5, addition));
      System.out.println("10 - 5 = " + tester.operate(10, 5, subtraction));
      System.out.println("10 x 5 = " + tester.operate(10, 5, multiplication));
      System.out.println("10 / 5 = " + tester.operate(10, 5, division));
        
      // 不用括号
      GreetingService greetService1 = message ->
      System.out.println("Hello " + message);
        
      // 用括号
      GreetingService greetService2 = (message) ->
      System.out.println("Hello " + message);
        
      greetService1.sayMessage("Runoob");
      greetService2.sayMessage("Google");
   }
    
   interface MathOperation {
      int operation(int a, int b);
   }
    
   interface GreetingService {
      void sayMessage(String message);
   }
    
   private int operate(int a, int b, MathOperation mathOperation){
      return mathOperation.operation(a, b);
   }
}
10 + 5 = 15
10 - 5 = 5
10 x 5 = 50
10 / 5 = 2
Hello Runoob
Hello Google
```

- 新的Stream API    **java.util.stream** 函数式编程风格引入
- 接口拥有默认方法  **支持default和static方法**   不再是传统的 ~~接口中方法都为抽象方法。~~
- Optional类 成为JAVA8自带库一部分 用来解决空指针异常
- Date Time API 加强对日期时间处理

# Java基础概念

一个 Java 程序可以认为是一系列对象的集合，而这些对象通过调用彼此的方法来协同工作。下面简要介绍下**类**、**对象**、**方法**和**实例变量**的概念。

## 基本概念

**对象**：**对象是类的一个实例**，有状态和行为。例如，一条狗是一个对象，它的状态有：颜色、名字、品种；行为有：摇尾巴、叫、吃等。

**类**：类是一个**模板**，它描述一类对象的行为（方法）和状态（属性）。

**方法**：**方法就是行为**，一个类可以有很多方法。逻辑运算、数据修改以及所有动作都是在方法中完成的。

**实例变量**：**每个对象都有独特的实例变量**，对象的状态由这些实例变量的值决定。

## 基本语法规范

1. 大小写敏感规范：Java 区分大小写是**大小写敏感**的，这就意味着标识符 Hello 与 hello 是不同的。
2. 类名规范：对于所有类来说，类名由多个单词组成那么**每个单词首字母应该大写**。例如 **MyFirstJavaClass** 。
3. 方法名规范：对于方法类来说，方法名由多个单词组成那么**首个单词首字母应该小写**，**后续单词则大写开头**。
4. 源文件名规范：**源文件名必须和类名相同**。当保存文件的时候，文件名的后缀为 **.java**。
5. 主方法入口规范：所有的 Java 程序由 <psvm>**public static void main(String[] args)** 方法开始执行。

## Java 标识符规范

- 所有的标识符都应该以字母（A-Z 或者 a-z）,美元符（$）、或者下划线（_）开始
- 首字符之后可以是字母（A-Z 或者 a-z）,美元符（$）、下划线（_）或数字的任何字符组合
- 关键字不能用作标识符
- 标识符是大小写敏感的
- 合法标识符举例：age、$salary、_value、__1_value
- 非法标识符举例：123abc、-salary

## Java修饰符规范

- 访问控制修饰符 : default, public , protected, private。
- 非访问控制修饰符 : final, abstract, static, synchronized。

## Java 枚举规范

枚举限制变量只能是预先设定好的值。使用枚举可以减少代码中的 bug。

例如：我们为果汁店设计一个程序，它将限制果汁为小杯、中杯、大杯。这就意味着它不允许顾客点除了这三种尺寸外的果汁。

```java
class FreshSize {
   enum HotSize{ XXL, XL , L }//三种尺寸的枚举描述类
   HotSize size;//枚举对象
}
public class FreshSizeTest {
   public static void main(String[] args){
      FreshSize fs = new FreshSize();//创建对象
      fs.size = FreshSize.HotSize.L;//赋值给实例
   }
}//枚举可以单独声明或者声明在类里面。方法、变量、构造函数也可以在枚举中定义。
```

## Java 变量规范

### 局部变量

（方法中） 类的方法中的变量。

> 局部变量声明在方法、构造方法或者语句块中；
>
> 局部变量是在栈上分配的。
>
> 访问修饰符不能用于局部变量；
>
> 局部变量在方法、构造方法、或者语句块被执行的时候创建，当它们执行完成后，变量将会被销毁；
>
> 局部变量没有默认值，所以局部变量被声明后，必须经过初始化，才可以使用。
>
> ```java
> public class Test{ 
>    public void pupAge(){
>       int age = 0;
>       age = age + 7;
>       System.out.println("小狗的年龄是: " + age);
>    }
>    
>    public static void main(String[] args){
>       Test test = new Test();
>       test.pupAge();
>    }
> }
> //小狗的年龄是: 7
> ```

### 成员变量

（非静态变量）独立于方法之外的变量，不过没有 static 修饰。

> 当一个对象被实例化之后，每个实例变量的值就跟着确定；
>
> 访问修饰符可以修饰实例变量；
>
> 实例变量在对象创建的时候创建，在对象被销毁的时候销毁；
>
> 实例变量的值应该至少被一个方法、构造方法或者语句块引用，使得外部能够通过这些方式获取实例变量信息；
>
> 实例变量可以声明在使用前或者使用后；
>
> 实例变量具有默认值。数值型变量的默认值是0，布尔型变量的默认值是false，引用类型变量的默认值是null。变量的值可以在声明时指定，也可以在构造方法中指定；
>
> 实例变量对于类中的方法、构造方法或者语句块是可见的。一般情况下应该把实例变量设为私有。通过使用访问修饰符可以使实例变量对子类可见；
>
> 实例变量可以直接通过变量名访问。但在静态方法以及其他类中，就应该使用完全限定名：ObjectReference.VariableName。
>
> ```java
> import java.io.*;
> public class Employee{
>    // 这个实例变量对子类可见
>    public String name;
>    // 私有变量，仅在该类可见
>    private double salary;
>    //在构造器中对name赋值
>    public Employee (String empName){
>       name = empName;
>    }
>    //设定salary的值
>    public void setSalary(double empSal){
>       salary = empSal;
>    }  
>    // 打印信息
>    public void printEmp(){
>       System.out.println("名字 : " + name );
>       System.out.println("薪水 : " + salary);
>    }
> 
>    public static void main(String[] args){
>       Employee empOne = new Employee("RUNOOB");
>       empOne.setSalary(1000.0);
>       empOne.printEmp();
>    }
> }
> //$ javac Employee.java 
> //$ java Employee
> //名字 : RUNOOB
> //薪水 : 1000.0
> ```

### 类变量（静态变量）

> 类变量也称为静态变量，在类中以 static 关键字声明，但必须在方法之外。
>
> **无论一个类创建了多少个对象，类只拥有类变量的一份拷贝。**
>
> 静态变量除了被声明为常量外很少使用，静态变量是指声明为 public/private，final 和 static 类型的变量。静态变量初始化后不可改变。
>
> **静态变量储存在静态存储区。经常被声明为常量，很少单独使用 static 声明变量。**
>
> **静态变量在第一次被访问时创建，在程序结束时销毁。**
>
> 与实例变量具有相似的可见性。但为了对类的使用者可见，大多数静态变量声明为 public 类型。
>
> 默认值和实例变量相似。**数值型变量默认值是 0，布尔型默认值是 false，引用类型默认值是 null。**变量的值可以在声明的时候指定也可以在构造方法中指定。此外，静态变量还可以在静态语句块中初始化。
>
> 静态变量可以通过：*ClassName.VariableName*的方式访问。
>
> 类变量被声明为 public static final 类型时，类变量名称一般建议使用大写字母。如果静态变量不是 public 和 final 类型，其命名方式与实例变量以及局部变量的命名方式一致。
>
> ```java
> public class Employee {
>     //salary是静态的私有变量
>     private static double salary;
>     // DEPARTMENT是一个常量
>     public static final String DEPARTMENT = "开发人员";
>     public static void main(String[] args){
>     salary = 10000;
>         System.out.println(DEPARTMENT+"平均工资:"+salary);
>     }
> }
> //开发人员平均工资:10000.0
> ```

#### 静态方法

（1）静态方法中不需要它所属类的任何实例就可以访问，所以在静态方法中不可以使用this关键字
（2）静态方法中不可直接访问所属类的实例变量和实例方法，但可以直接访问所属类的静态变量和静态方法

## 继承与接口规范

1.继承：在 Java 中，一个类可以由其他类派生。如果你要创建一个类，而且已经存在一个类具有你所需要的属性或方法，那么你可以将新创建的类继承该类。利用继承的方法，可以重用已存在类的方法和属性，而不用重写这些代码。被继承的类称为超类（super class），派生类称为子类（sub class）。

2.接口：在 Java 中，接口可理解为对象间相互通信的协议。接口在继承中扮演着很重要的角色。接口只定义派生要用到的方法，但是方法的具体实现完全取决于派生类。

## 基本数据类型

变量就是申请内存来存储值。也就是说，当创建变量的时候，需要在内存中申请空间。内存管理系统根据变量的类型为变量分配存储空间，分配的空间只能用来储存该类型数据。

![img](https://www.runoob.com/wp-content/uploads/2013/12/2020-10-27-code-mem.png)

Java 的两大数据类型:

- **内置数据类型**
- **引用数据类型**

### **内置数据类型**

Java语言提供了**八种基本类型**。六种数字类型（**四个整数型，两个浮点型**），**一种字符类型**，还有一种**布尔**型。

> - **byte**：8位有符号的以二进制补码表示的整数；最小值是 **-128（-2^7）**最大值是 **127（2^7-1）**默认值是 **0**；
>
> byte 类型用在大型数组中节约空间，主要代替整数，因为 byte 变量占用的空间只有 int 类型的四分之一；
>
> - **short：**16 位、有符号的以二进制补码表示的整数，最小值是 **-32768（-2^15）**最大值是 **32767（2^15 - 1）**默认值是 **0** 
>
> Short 数据类型也可以像 byte 那样节省空间。一个short变量是int型变量所占空间的二分之一；
>
> - **int**：32位、有符号的以二进制补码表示的整数；最小值是 **-2,147,483,648（-2^31）**最大值是 **2,147,483,647（2^31 - 1）**默认值是 **0**
>
> 一般地整型变量默认为 int 类型
>
> - **long：** 64 位、有符号的以二进制补码表示的整数；最小值是 **-9,223,372,036,854,775,808（-2^63）**；最大值是 **9,223,372,036,854,775,807（2^63 -1）**；
>
> 默认值是 **0L **这种类型主要使用在需要比较大整数的系统上；
>
> - **float：**单精度、32位、符合IEEE 754标准的浮点数；默认值是 **0.0f**；
>
> 浮点数不能用来表示精确的值，如货币；float 在储存大型浮点数组的时候可节省内存空间；
>
> - **double：**双精度、64 位、符合 IEEE 754 标准的浮点数；double类型同样不能表示精确的值，如货币；
>
> 默认值是 **0.0d**；浮点数的默认类型为 double 类型；
>
> - **char**：一个单一的 16 位 Unicode 字符；最小值是 **\u0000**（十进制等效值为 0）；最大值是 **\uffff**（即为 65535）；char 数据类型可以储存任何字符；例子：char letter = 'A';
>
> - **boolean：**只有两个取值：true 和 false；**默认值是 false**

### **引用数据类型**

> 在Java中，引用类型的变量非常类似于C/C++的指针。引用类型指向一个对象，指向对象的变量是引用变量。这些变量在声明时被指定为一个特定的类型，比如 Employee、Puppy 等。变量一旦声明后，类型就不能被改变了。
>
> 所有引用类型的默认值都是null；对象、数组都是引用数据类型；一个引用变量可以用来引用任何与之兼容的类型。
>
> ### 引用类型
>
> > 引用是一个对象别名，与被引用的对象共享同一块内存区域。例如“鹿晗”这个对象，他的原名是“刘壮实”，但两者其实都是指同一个人（内存）。对象在创建时会请求一块内存空间来保存数据，会根据对象大小分配存储空间大小不等的内存区域。在Java中，访问对象时，不会直接访问对象在内存中的数据，而是通过引用去访问。因此，引用也是一种数据类型，类似于C/C++ 语言中的指针。引用定义时在栈中分配内存，引用变量在程序运行到作用域外释。
> >
> > java的引用类型有：1、强引用；2、软引用；3、弱引用；4、虚引用。

### 类型转换规范

<u>整数的默认类型是 int ; 小数默认是 double 类型浮点型，在定义 float 类型时必须在数字后面跟上 F 或者 f。</u>

**整型、实型（常量）、字符型数据可以混合运算。运算中，不同类型的数据先转化为同一类型，然后进行运算。**

```xml
转换从低级到高级。
低  ------------------------------------>  高
byte,short,char—> int —> long—> float —> double 
```

1.  不能对boolean类型进行类型转换。

2.  不能把对象类型转换成不相关类的对象。

3. 在把容量大的类型转换为容量小的类型时必须使用强制类型转换。

4. 转换过程中可能导致溢出或损失精度，例如：

   ```java
   int i =128;   
   byte b = (byte)i;
   //因为 byte 类型是 8 位，最大值为127，所以当 int 强制转换为 byte 类型时，值 128 时候就会导致溢出。
   ```

5. 浮点数到整数的转换是通过舍弃小数得到，而不是四舍五入，例如：

   ```java
   (int)23.7 == 23;        
   (int)-45.89f == -45
   ```

**java中的类型转换大致分为两种：1.自动类型转换  2.强制类型转换** 

#### 1.自动类型转换

必须满足转换前的数据类型的位数要低于转换后的数据类型，例如: short数据类型的位数为16位，就可以自动转换位数为32的int类型，同样float数据类型的位数为32，可以自动转换为64位的double类型。

```java
public class ZiDongLeiZhuan{
        public static void main(String[] args){
            char c1='a';//定义一个char类型
            int i1 = c1;//char自动类型转换为int
            System.out.println("char自动类型转换为int后的值等于"+i1);
            char c2 = 'A';//定义一个char类型
            int i2 = c2+1;//char 类型和 int 类型计算
            System.out.println("char类型和int计算后的值等于"+i2);
        }
}
//char自动类型转换为int后的值等于97
//char类型和int计算后的值等于66
解析：c1 的值为字符 a ,查 ASCII 码表可知对应的 int 类型值为 97， A 对应值为 65，所以 i2=65+1=66。
```

#### 2.强制类型转换

条件是转换的数据类型必须是兼容的。格式：(type)value type是要强制类型转换后的数据类型 实例：

```java
public class QiangZhiZhuanHuan{
    public static void main(String[] args){
        int i1 = 123;
        byte b = (byte)i1;//强制类型转换为byte
        System.out.println("int强制类型转换为byte后的值等于"+b);
    }
}
//int强制类型转换为byte后的值等于123
```

## Java 异常处理

异常是程序中的一些错误，但并不是所有的错误都是异常，并且错误有时候是可以避免的。

异常发生的原因有很多，通常包含以下几大类：

- **用户输入了非法数据。**
- **要打开的文件不存在。**
- **网络通信时连接中断，或者JVM内存溢出。**

这些异常有的是因为用户错误引起，有的是程序错误引起的，还有其它一些是因为物理错误引起的。

要理解Java异常处理是如何工作的，你需要掌握以下三种类型的异常：

- **检查性异常：**最具代表的检查性异常是用户错误或问题引起的异常，这是程序员无法预见的。例如要打开一个不存在文件时，一个异常就发生了，这些异常在编译时不能被简单地忽略。
- **运行时异常：** 运行时异常是可能被程序员避免的异常。与检查性异常相反，运行时异常可以在编译时被忽略。
- **错误：** 错误不是异常，而是脱离程序员控制的问题。错误在代码中通常被忽略。例如，当栈溢出时，一个错误就发生了，它们在编译也检查不到的。

### Exception 类

所有的异常类是从 java.lang.Exception 类继承的子类。

Exception 类是 Throwable 类的子类。除了Exception类外，Throwable还有一个子类Error 。

Java 程序通常不捕获错误。错误一般发生在严重故障时，它们在Java程序处理的范畴之外。

Error 用来指示运行时环境发生的错误。

例如，JVM 内存溢出。一般地，程序不会从错误中恢复。

异常类有两个主要的子类：IOException 类和 RuntimeException 类。![img](https://www.runoob.com/wp-content/uploads/2013/12/exception-hierarchy.png)

### Java 内置异常类

Java 语言定义了一些异常类在 java.lang 标准包中。

标准运行时异常类的子类是最常见的异常类。由于 java.lang 包是默认加载到所有的 Java 程序的，所以大部分从运行时异常类继承而来的异常都可以直接使用。

Java 根据各个类库也定义了一些其他的异常，下面的表中列出了 Java 的**非检查性异常**。

| **异常**                        | **描述**                                                     |
| :------------------------------ | :----------------------------------------------------------- |
| ArithmeticException             | 当出现异常的运算条件时，抛出此异常。例如，一个整数"除以零"时，抛出此类的一个实例。 |
| ArrayIndexOutOfBoundsException  | 用非法索引访问数组时抛出的异常。如果索引为负或大于等于数组大小，则该索引为非法索引。 |
| ArrayStoreException             | 试图将错误类型的对象存储到一个对象数组时抛出的异常。         |
| ClassCastException              | 当试图将对象强制转换为不是实例的子类时，抛出该异常。         |
| IllegalArgumentException        | 抛出的异常表明向方法传递了一个不合法或不正确的参数。         |
| IllegalMonitorStateException    | 抛出的异常表明某一线程已经试图等待对象的监视器，或者试图通知其他正在等待对象的监视器而本身没有指定监视器的线程。 |
| IllegalStateException           | 在非法或不适当的时间调用方法时产生的信号。换句话说，即 Java 环境或 Java 应用程序没有处于请求操作所要求的适当状态下。 |
| IllegalThreadStateException     | 线程没有处于请求操作所要求的适当状态时抛出的异常。           |
| IndexOutOfBoundsException       | 指示某排序索引（例如对数组、字符串或向量的排序）超出范围时抛出。 |
| NegativeArraySizeException      | 如果应用程序试图创建大小为负的数组，则抛出该异常。           |
| NullPointerException            | 当应用程序试图在需要对象的地方使用 `null` 时，抛出该异常     |
| NumberFormatException           | 当应用程序试图将字符串转换成一种数值类型，但该字符串不能转换为适当格式时，抛出该异常。 |
| SecurityException               | 由安全管理器抛出的异常，指示存在安全侵犯。                   |
| StringIndexOutOfBoundsException | 此异常由 `String` 方法抛出，指示索引或者为负，或者超出字符串的大小。 |
| UnsupportedOperationException   | 当不支持请求的操作时，抛出该异常。                           |

下面的表中列出了 Java 定义在 java.lang 包中的**检查性异常类**。

| **异常**                   | **描述**                                                     |
| :------------------------- | :----------------------------------------------------------- |
| ClassNotFoundException     | 应用程序试图加载类时，找不到相应的类，抛出该异常。           |
| CloneNotSupportedException | 当调用 `Object` 类中的 `clone` 方法克隆对象，但该对象的类无法实现 `Cloneable` 接口时，抛出该异常。 |
| IllegalAccessException     | 拒绝访问一个类的时候，抛出该异常。                           |
| InstantiationException     | 当试图使用 `Class` 类中的 `newInstance` 方法创建一个类的实例，而指定的类对象因为是一个接口或是一个抽象类而无法实例化时，抛出该异常。 |
| InterruptedException       | 一个线程被另一个线程中断，抛出该异常。                       |
| NoSuchFieldException       | 请求的变量不存在                                             |
| NoSuchMethodException      | 请求的方法不存在                                             |

### 异常方法

下面的列表是 Throwable 类的主要方法:

| **序号** | **方法及说明**                                               |
| :------- | :----------------------------------------------------------- |
| 1        | **public String getMessage()** 返回关于发生的异常的详细信息。这个消息在Throwable 类的构造函数中初始化了。 |
| 2        | **public Throwable getCause()** 返回一个 Throwable 对象代表异常原因。 |
| 3        | **public String toString()** 返回此 Throwable 的简短描述。   |
| 4        | **public void printStackTrace()** 将此 Throwable 及其回溯打印到标准错误流。。 |
| 5        | **public StackTraceElement [] getStackTrace()** 返回一个包含堆栈层次的数组。下标为0的元素代表栈顶，最后一个元素代表方法调用堆栈的栈底。 |
| 6        | **public Throwable fillInStackTrace()** 用当前的调用栈层次填充Throwable 对象栈层次，添加到栈层次任何先前信息中。 |

### 捕获异常<重要>

使用 try 和 catch 关键字可以捕获异常。try/catch 代码块放在异常可能发生的地方。

try/catch代码块中的代码称为保护代码，使用 try/catch 的语法如下：

```
try
{
   // 程序代码
}catch(ExceptionName e1)
{
   //Catch 块
}
```

Catch 语句包含要捕获异常类型的声明。当保护代码块中发生一个异常时，try 后面的 catch 块就会被检查。

如果发生的异常包含在 catch 块中，异常会被传递到该 catch 块，这和传递一个参数到方法是一样。

```java
// 文件名 : ExcepTest.java
import java.io.*;
public class ExcepTest{
 
   public static void main(String args[]){
      try{
         int a[] = new int[2];
         System.out.println("Access element three :" + a[3]);
      }catch(ArrayIndexOutOfBoundsException e){
         System.out.println("Exception thrown  :" + e);
      }
      System.out.println("Out of the block");
   }
}
//Exception thrown  :java.lang.ArrayIndexOutOfBoundsException: 3
//Out of the block
```

### 多重捕获块

一个 try 代码块后面跟随多个 catch 代码块的情况就叫多重捕获。

多重捕获块的语法如下所示：

```java
try{
   // 程序代码
}catch(异常类型1 异常的变量名1){
  // 程序代码
}catch(异常类型2 异常的变量名2){
  // 程序代码
}catch(异常类型3 异常的变量名3){
  // 程序代码
}
```

上面的代码段包含了 3 个 catch块。

可以在 try 语句后面添加任意数量的 catch 块。

如果保护代码中发生异常，异常被抛给第一个 catch 块。

如果抛出异常的数据类型与 ExceptionType1 匹配，它在这里就会被捕获。

如果不匹配，它会被传递给第二个 catch 块。

如此，直到异常被捕获或者通过所有的 catch 块。

```java
#实例:
    try {
    file = new FileInputStream(fileName);
    x = (byte) file.read();
} catch(FileNotFoundException f) { // Not valid!
    f.printStackTrace();
    return -1;
} catch(IOException i) {
    i.printStackTrace();
    return -1;
}
```

### throws/throw 关键字

如果一个方法没有捕获到一个检查性异常，那么该方法必须使用 throws 关键字来声明。throws 关键字放在方法签名的尾部。

也可以使用 throw 关键字抛出一个异常，无论它是新实例化的还是刚捕获到的。

**一个方法可以声明抛出多个异常，多个异常之间用逗号隔开。**

例如，下面的方法声明抛出 RemoteException 和 InsufficientFundsException：

```java
import java.io.*;
public class className
{
   public void withdraw(double amount) throws RemoteException,
                              InsufficientFundsException
   {
       // Method implementation
   }
   //Remainder of class definition
}
```

### finally关键字

finally 关键字用来创建在 try 代码块后面执行的代码块。

无论是否发生异常，finally 代码块中的代码总会被执行。

在 finally 代码块中，可以运行清理类型等收尾善后性质的语句。

finally 代码块出现在 catch 代码块最后，语法如下：

```java
try{
  // 程序代码
}catch(异常类型1 异常的变量名1){
  // 程序代码
}catch(异常类型2 异常的变量名2){
  // 程序代码
}finally{
  // 程序代码
}
```

```java
//实例：
public class ExcepTest{
  public static void main(String args[]){
    int a[] = new int[2];
    try{
       System.out.println("Access element three :" + a[3]);
    }catch(ArrayIndexOutOfBoundsException e){
       System.out.println("Exception thrown  :" + e);
    }
    finally{
       a[0] = 6;
       System.out.println("First element value: " +a[0]);
       System.out.println("The finally statement is executed");
    }
  }
}
//Exception thrown  :java.lang.ArrayIndexOutOfBoundsException: 3
//First element value: 6
//The finally statement is executed
```

### try-with-resources语法糖

JDK7 之后，Java 新增的 **try-with-resource** 语法糖来打开资源，并且可以在语句执行完毕后确保每个资源都被自动关闭 。

JDK7 之前所有被打开的系统资源，比如流、文件或者 Socket 连接等，都需要被开发者手动关闭，否则将会造成资源泄露。

```java
try (resource declaration) {
  // 使用的资源
} catch (ExceptionType e1) {
  // 异常块
}
```

以上的语法中 try 用于声明和实例化资源，catch 用于处理关闭资源时可能引发的所有异常。

**注意：**try-with-resources 语句关闭所有实现 AutoCloseable 接口的资源。

```java
public class RunoobTest {

    public static void main(String[] args) {
    String line;
        try(BufferedReader br = new BufferedReader(new FileReader("test.txt"))) {
            while ((line = br.readLine()) != null) {
                System.out.println("Line =>"+line);
            }
        } catch (IOException e) {
            System.out.println("IOException in try block =>" + e.getMessage());
        }
    }
}
```

以上实例输出结果为：

```
IOException in try block =>test.txt (No such file or directory)
```

### 通用异常

在Java中定义了两种类型的异常和错误。

- **JVM(Java虚拟机)**异常：**由 JVM 抛出的异常或错误。例如：NullPointerException 类，ArrayIndexOutOfBoundsException 类，ClassCastException 类。
- **程序级异常：**由程序或者API程序抛出的异常。例如 IllegalArgumentException 类，IllegalStateException 类。

# Spring

**全面的企业应用开发一站式的解决方案 (与其他框架兼容 例如MyBatis,Hibernate,Shrio)**

**特点 ：轻量级(仅需2M JAR文件)  非入侵式(无捆绑的)  应用中的对象不依赖与spring特定类 支持junit4测试**![spring-overview](https://www.runoob.com/wp-content/uploads/2015/07/673670c9a34075831373b711cb8f21b7.png)

## Spring的核心机制

**管理Bean**

程序主要是通过Spring容器来访问容器中的Bean，ApplicationContext是Spring容器最常用的接口，该接口有如下两个实现类：

- ClassPathXmlApplicationContext: 从类加载路径下搜索配置文件，并根据配置文件来创建Spring容器。
- FileSystemXmlApplicationContext: 从文件系统的相对路径或绝对路径下去搜索配置文件，并根据配置文件来创建Spring容器。

```java
public class BeanTest{
    public static void main(String args[]) throws Exception{
        ApplicationContext ctx = new ClassPathXmlApplicationContext("beans.xml");
        Person p = ctx.getBean("person", Person.class);
        p.say();
    }
}
```





## **1.控制反转IOC  **

**由spring容器管理整个bean的生命周期 通过<u>反射</u>实现对其它对象控制 包括初始化 创建 销毁等 无需手动管理对象过程**

> **1.1依赖注入DI**   促进低耦合 常用@Autowired根据属性自动装配无需字段的 set 方法 
>
> ```java
> //成员属性字段使用 @Autowired，无需字段的 set 方法
> @Autowired
> private AdminServiceImpl adminService;
> //set 方法使用 @Autowired
> private AdminServiceImpl adminService1;
> @Autowired
> public void setAdminService1(AdminServiceImpl adminService){
>   this.adminService1 = adminService;
> }
> //构造方法使用 @Autowired
> private AdminServiceImpl adminService2;
> @Autowired
> AdminController(AdminServiceImpl adminService){
>   this.adminService2 = adminService;
> }
> ```
>
> ----
>
> **1.2依赖查询DL** 
>
> **一个对象依赖的其他对象会以被动的方式传递进来 即无需创建查找依赖对象**
>
> **实现：容器中的受控对象通过容器的 API 来查找自己所依赖的资源和协作对象。**
>
> 依赖查询DL也有两种方式
>
> - 依赖拖拽：注入的对象如何与组件发生联系，这个过程就是通过依赖拖拽实现；
>
> - 上下文依赖查找：在某些方面跟依赖拖拽类似，但是上下文依赖查找中，查找的过程是在容器管理的资源中进行的，而不是从集中注册表中，并且通常是作用在某些设置点上；
>
>   ---
>

### **<u>简述IOC初始化过程？</u>**

> > 1. 首先要看你是怎么声明注入bean的  常见的**xml 配置 注解  bean配置** 我最常用的是**AnnotationConfigApplication**注解容器，也就是使用**@Configuration**进行注册 然后解析成Bean
> > 2. 将Bean解析成**BeanDefinition** 一个对bean信息进行包装的类 会对bean配置的参数进行或者是XML配置的property标签注入到BeanDefinition的实例中
> > 3. 再将对应的**beanDefinition**实例注册到容器**beanDefinitionMap**中
> > 4. **beanfactory**根据BeanDefinition创建实例化和初始化bean
>
> ----
>

### <u>**spring加载bean有哪些方式？**</u>

> > 1.首先要通过@Configuration+@Bean
> >
> > @Configuration用来声明一个配置类 然后使用@Bean声明一个bean 将其加入spring容器
> >
> > ```java
> > @Configuration
> > public class TestConfiguration {
> > @Bean
> > public Admin admin(){
> >   return new Admin();
> > }
> > }
> > ```
> >
> > 2.包扫描特定注解的方式 使用@Component或者@ComponentScan 
> >
> > @Component声明自己是个等待spring将自己实例化到spring容器中的类 让spring容器来统一管理 用起来不需要new了 相当于:
> >
> > ```java
> > <bean id="" class=""/>
> > ```
> >
> > 而@ComponentScan会指定一个路径 扫描路径内带有特定注解的bean 相当于告诉spring容器去哪里找自己需要的bean 添加进容器中 其中特定的注解会包括@Controller @Service @Repository @Component
> >
> > ```java
> > // 控制层
> > @Controller
> > public class UserController {
> > }
> > 
> > // 业务层
> > @Service
> > public class UserService {
> > }
> > 
> > // 持久层
> > @Repository
> > public class UserDao {
> > }
> > ```
> >
> > ```java
> > public class TestConfiguration {
> > @Test
> > public void Test() {
> >   AnnotationConfigApplicationContext applicationContext = new AnnotationConfigApplicationContext(AppConfig.class);
> >   String[] beanNames = applicationContext.getBeanDefinitionNames();
> >   for (String beanName:beanNames) {
> >       System.out.println("容器中对象名称："+beanName);
> >   }
> > 
> > }
> > }
> > @Configuration
> > @ComponentScan(value = "com.example.app.goodjobdemo.Test")
> > class AppConfig {
> > }
> > //容器中对象名称：appConfig
> > //容器中对象名称：userController
> > //容器中对象名称：userDao
> > //容器中对象名称：userService
> > ```
> >
> > 3.@Import注解导入 开发中很少使用 对spring扩展的时候才会经常用到 通常搭配自定义注解使用往容器导入配置类文件
> >
> > ```java
> > public class TestConfiguration {
> > @Test
> > public void Test() {
> >   AnnotationConfigApplicationContext applicationContext = new AnnotationConfigApplicationContext(AppConfig.class);
> >   String[] beanNames = applicationContext.getBeanDefinitionNames();
> >   for (String beanName:beanNames) {
> >       System.out.println("容器中对象名称："+beanName);
> >   }
> > 
> > }
> > }
> > @Configuration
> > @Import({UserController.class,UserDao.class,UserService.class})
> > class AppConfig {
> > }
> > //容器中对象名称：appConfig
> > //容器中对象名称：com.example.app.goodjobdemo.Test.UserController
> > //容器中对象名称：com.example.app.goodjobdemo.Test.UserDao
> > //容器中对象名称：com.example.app.goodjobdemo.Test.UserService
> > ```
> >
> > 4.实现BeanDefinitionRegistryPostProcessor进行后置处理
> >
> > ```java
> > //源码 BeanFactoryPostProcessor接口中只有一个方法 就是postProcessBeanDefinitionRegistry
> > public interface BeanDefinitionRegistryPostProcessor extends BeanFactoryPostProcessor {
> > 	void postProcessBeanDefinitionRegistry(BeanDefinitionRegistry registry) throws BeansException;
> > }
> > ```
> >
> > spring容器启动会执行postProcessBeanDefinitionRegistry方法 
> >
> > 即 等BeanDefinition加载完毕后进行后置处理 在此调整BeanDefinition就可以干扰到后面初始化bean操作
> >
> > 5.使用FactoryBean接口 
> >
> > 使用@Configuration+@Bean方式将AdminFactoryBean加入到容器中
> >
> > 代码如下 并没有向容器中直接注入Admin 而是注入AdminFactoryBean然后再从容器中拿到Admin这个类型的Bean
> >
> > ```java
> > @Configuration
> > public class TestConfiguration {
> > @Bean
> > public AdminFactoryBean adminFactoryBean(){
> >   return new AdminFactoryBean();
> > }
> > @Test
> > public void Test() {
> >   AnnotationConfigApplicationContext applicationContext = new AnnotationConfigApplicationContext(TestConfiguration.class);
> >   Admin bean = applicationContext.getBean(Admin.class);
> >   System.out.println(bean);
> > }
> > }
> > @Component
> > class AdminFactoryBean implements FactoryBean {
> > @Override
> > public Admin getObject() throws Exception {
> >   return new Admin();
> > }
> > @Override
> > public Class<?> getObjectType() {
> >   return Admin.class;
> > }
> > }
> > //Admin(id=null, name=null, password=null)
> > ```
> >
> > 还有很多实现注入Bean的方法
> >
> > `1.xml；2.扫描加注解；3.配置类@bean；4.实现factorybean；5.annotationapplicationcontext的register注册；6.import类；7.selectimport实现类；8.实现importbeandefinitionregister自定义bean；9.实现beandefinitionregisterpostprocessor后置注册修改bean`
>
> ---
>

### <u>**Spring bean 的生命周期？**</u>

> 1.调用Bean的构造方法创建Bean
>
> 2.通过反射调用setter方法进行属性依赖注入
>
> 2.1如果bean实现了BeanNameAware接口 spring将调用setBeanName()方法设置Bean的name(对应xml文件中bean的标签id)
>
> 2.2如果bean实现实现了BeanFacoryAware接口spring就将调用2.3setBeanFactory()把beanfactory设置给bean
>
> 2.4如果存在beanPostProcessor spring将会调用postProcessBeforeLinitialization预处理方法在bean初始化之前对其处理
>
> 2.5如果bean实现了InitialigBean接口spring将调用tafterPropertiesSet()方法 然后调用xml定义的init-method方法 两个方法作用类似 都是再初始化bean的时候执行
>
> 2.6如果存在beanPostProcessor spring将会调用postProcessAfterLinitialization初始化后方法在bean初始化之后对其处理
>
> 3.bean初始化完成 供应用使用 分为两种情况：
>
> 3.1如果bean为单例的话那么容器返回bean给用户并存入缓存池
>
> 如果实现了DisposableBean接口 spring将调用他的destory()然后调用xml中定义的destory-mothod方法 这两个方法作用类似都是在bean实例销毁前执行
>
> 3.2如说bean是多例的话 容器将bean返回给用户 剩下的生命周期将由用户控制
>
> ---

### <u>**Spring怎么解决循环依赖的？**</u>

> **Spring通过三级缓存来解决缓存依赖** 
>
> #example:两个对象互相形成依赖
> 创建Bean-A时 对Bean-A进行构造方法后就将Bean-A对象放入Spring的三级缓存**singletonFactories**
>
> 发现Bean-A依赖Bean-B，开始创建Bean-B并执行完Bean-B的构造方法后，放入三级缓存
>
> 处理Bean-B的依赖Bean-A时，发现三级缓存中有一个Bean-A，拿到这个BeanA完成B的注入，同时也完成A的注入

### **<u>Spring Bean如何保证并发安全？</u>**

> > ```yaml
> > example:
> > spring的bean默认都是单例的 singleton 某些情况下单例并发是不安全的
> > 假如我们在Controller控制层定义了成员变量 多个请求来临时进入的都是同一单例对象并且对成员变量进行修改会有并发安全风险
> > 如何解决？
> > ```
> >
> > 1.单例变原型
> >
> > 如果是web应用在controller类上加**@Scope("prototype")**或者**@Scope("request")**
> >
> > 如果不是web应用在Component类上加注解**@Scope("prototype")**
> >
> > 这种方式实现起虽然简单 但是会增加服务器资源中bean创建销毁实例的开销
> >
> > 2.尽量避免使用成员变量
> >
> > 在业务允许范围内 使用RequsetMapping方法中的局部变量替换控制层的成员 这种方式比较恰当
> >
> > 3.使用并发安全类
> >
> > 如果如果一定需要在单例bean使用成员变量 可以使用并发安全的容器
> >
> > 例如 ConcurrentHashMap  ConcurrentHashSet
> >
> > 4.分布式或者微服务 项目的并发安全解决方案
> >
> > 如果还需要考虑到微服务或者分布式服务的并发安全解决 第三种方法便不太合适
> >
> > 借助于可以共享某些信息的分布式缓存中间件 例如Redis等
> >
> > 这样既可以保证统一服务 不同服务实例 且都有同一共享信息
>
> ---
>

### **<u>Spring用到了那些设计模式？</u>**

> > **1.工厂模式** IOC容器可以使用BeanFactory 或 ApplicationContext创建 bean 对象 
> >
> > - BeanFactory 是bean合集工厂类 懒加载或者延时加载 (使用到某个 bean 的时候才会注入) 启动速度快占用内存少
> >
> > - ApplicationContext 是BeanFactory的扩展(接口提供额外功能)  即使加载(容器启动的时候 不管你用没用到 一次性创建所有 bean) 开发人员使用ApplicationContext会更多 
> >
> >   ```yaml
> >   #ApplicationContext的三个实现类
> >   -ClassPathXmlApplication：从类的根路径下加载配置文件（推荐使用这种）
> >   -FileSystemXmlApplication：它是从磁盘路径上加载配置文件，配置文件可以在磁盘的任意位置。
> >   -XmlWebApplicationContext：从Web系统中的XML文件载入上下文定义信息。
> >   -AnnotationConfigApplicationContext：当使用注解配置容器对象时，需要使用此类来创建 spring 容器。它用来读取注解
> >   ```
> >
> >   ```java
> >   //example
> >   ApplicationContext applicationContext = new ClassPathXmlApplicationContext("applicationContext.xml");
> >   UserService userService = (UserService) applicationContext.getBean("userService");
> >   userService.save();
> >   ```
> >
> > ---
> >
> > **2.单例模式** 一个类仅有一个实例 提供一个访问它的全局访问点
> >
> > **由于Spring中bean的默认作用域就是singleton(单例)的 优点如下：**
> >
> > - 对于频繁使用的对象，可以**省略创建对象所花费的时间**
> > - 由于new操作的次数减少，因而**对系统内存的使用频率也会降低 **减轻GC压力，缩短GC停顿时间
> >
> > **除了singleton作用域，Spring中bean还有下面几种作用域**
> >
> > - prototype : **每次**请求都会创建一个新的 bean 实例。
> > - request : 每一次HTTP请求都会产生一个新的bean，该bean仅在当前**HTTP request**内有效。
> > - session : 每一次HTTP请求都会产生一个新的 bean，该bean仅在当前**HTTP session**内有效。
> >
> > ---
> >
> > **3.代理模式**
> >
> > **1.Spring AOP**(Aspect-Oriented Programming:面向切面编程) **基于代理操作** 提供了两种动态代理实现 且都是**运行时增强** 
> >
> > - JDK Proxy 
> > - CGLIB Proxy
> >
> > **2.AspectJ AOP**  **是编译时增强**   基于**字节码操作(Bytecode Manipulation)**
> >
> > Spring AOP 已经集成了 AspectJ  相比于 Spring AOP 功能更加强大，但是 Spring AOP 相对来说更简单。如果我们的切面比较少，那么两者性能差异不大。但是，当切面太多的话，最好选择 AspectJ ，它比Spring AOP 快很多。
> >
> > ----
> >
> > **4.适配器模式 <Adapter Pattern>**
> >
> > **将一个接口转换成客户希望的另一个接口，适配器模式使接口不兼容的那些类可以一起工作，其别名为包装器(<u>Wrapper</u>)。**
> >
> > 比如 Spring MVC 中适配器HandlerAdatper，应用会有多个不同类型的Controller实现。如果需要调用方法会先判断是哪个Controller 再对应处理
> >
> > 如果增加一个 Controller就需要修改原来的判断逻辑 不利于维护 违反了模式设计开闭原则 <对扩展开放，对修改关闭>
> >
> > 为此Spring提供了该适配器接口 每个Controller对应一种HandlerAdatper实现类 对应请求时SpringMVC会通过getHandler()指定对应的Controller获取HandlerAdatper最后调用Handle()方法处理请求 实际是调用Controller的HandleRequest()方法
> >
> > 这种方法处理每次添加新的Controller时 只需增加一个适配器类即可 无需修改原有逻辑
> >
> > ---
> >
> > **5.观察者模式**      一种对象与对象之间具有依赖关系，当一个对象发生改变的时候，这个对象所依赖的对象也会做出反应
> >
> > - 事件角色 ：ApplicationEvent (org.springframework.context包下)抽象类
> >
> >    继承了java.util.EventObject并实现了 java.io.Serializable接口。
> >
> >   ```yaml
> >   #对ApplicationContextEvent的实现(继承自ApplicationContextEvent)
> >   - ContextStartedEvent：ApplicationContext 启动后触发的事件;
> >   - ContextStoppedEvent：ApplicationContext 停止后触发的事件;
> >   - ContextRefreshedEvent：ApplicationContext 初始化或刷新完成后触发的事件;
> >   - ContextClosedEvent：ApplicationContext 关闭后触发的事件。
> >   ```
> >
> > - 事件监听者角色  ApplicationListener接口 <java.util.EventListener>
> >
> >   里面只定义了一个 onApplicationEvent()方法来处理ApplicationEvent
> >
> >   我们只要实现 ApplicationListener 接口实现 onApplicationEvent() 方法即可完成监听事件
> >
> >   ```java
> >   package org.springframework.context;
> >   import java.util.EventListener;
> >   @FunctionalInterface
> >   public interface ApplicationListener<E extends ApplicationEvent> extends EventListener {
> >       void onApplicationEvent(E var1);
> >   }
> >   ```
> >
> > - 事件发布者角色 ApplicationEventPublisher  事件的发布者，它也是一个接口
> >
> >   ApplicationEventPublisher 接口的publishEvent()这个方法在AbstractApplicationContext类中被实现
> >
> >   实际是通过ApplicationEventMulticaster来广播出去的
> >
> >   ```java
> >   @FunctionalInterface
> >   public interface ApplicationEventPublisher {
> >       default void publishEvent(ApplicationEvent event) {
> >           this.publishEvent((Object)event);
> >       }
> >                                 
> >       void publishEvent(Object var1);
> >   }
> >   ```
> >
> > ---
> >
> > **6.模板模式 **
> >
> > 一个操作中的算法的骨架，而将一些步骤延迟到子类中。 
> >
> > 模板方法使得子类可以不改变一个算法的结构即可重定义该算法的某些特定步骤的实现方式。
> >
> > Spring 中 jdbcTemplate、hibernateTemplate 等以 Template 结尾的对数据库操作的类，它们就使用到了模板模式。一般情况下，我们都是使用继承的方式来实现模板模式，但是 Spring 并没有使用这种方式，而是使用Callback 模式与模板方法模式配合，既达到了代码复用的效果，同时增加了灵活性。
> >
> > ---
> >
> > ### 概括总结：
> >
> > 工厂设计模式 : Spring使用工厂模式通过 BeanFactory、ApplicationContext 创建 bean 对象。
> > 代理设计模式 : Spring AOP 功能的实现。
> > 单例设计模式 : Spring 中的 Bean 默认都是单例的。
> > 模板方法模式 : Spring 中 jdbcTemplate hibernateTemplate 等以 Template 结尾的对数据库操作的类，它们就使用到了模板模式。
> > 观察者模式: Spring 事件驱动模型就是观察者模式很经典的一个应用。
> > 适配器模式 :Spring AOP 的增强或通知(Advice)使用到了适配器模式、spring MVC 中也是用到了适配器模式适配Controller。
> > 装饰者(包装器)设计模式 : 我们的项目需要连接多个数据库，而且不同的客户在每次访问中根据需要会去访问不同的数据库。这种模式让我们可以根据客户的需求能够动态切换不同的数据源。
> >
> > ---
> >
> > 装饰者模式和适配器模式都是包装模式（Wrapper Pattern），装饰者模式是一种特殊的代理模式，二者对比如下：
> >
> > |      |          装饰者模式          |                          适配器模式                          |
> > | :--: | :--------------------------: | :----------------------------------------------------------: |
> > | 形式 |       非常特别的适配器       |              没有层级关系，装饰者模式有层级关系              |
> > | 定义 | 装饰者和被装饰着实现同一接口 | 适配器和被适配这没有必然的关系，通常采用继承或代理的形式进行包装 |
> > | 关系 |         满足is-a关系         |                        满足has-a关系                         |
> > | 功能 |        注重覆盖、扩展        |                        注重兼容、转换                        |
> > | 设计 |           前置考虑           |                           后置考虑                           |

## **2.面向切面AOP**  

**目的是业务逻辑与系统服务分开**

> 将一些公共逻辑(例如日志，事务管理等)封装成切面**@aspect** 跟业务代码进行分开 减少系统重复代码以及降低模板之间的耦合度
>
> **AOP：**
>
> 1. Aspect(切面): 是通知和切入点的结合,通知和切入点共同定义了关于切面的全部内容—它的功能、在何时和何地完成其功能
> 2. joinpoint(连接点):所谓连接点是指那些被拦截到的点。在spring中,这些点指的是方法,因为spring只支持方法类型的连接点.
> 3. Pointcut(切入点):所谓切入点是指我们要对哪些joinpoint进行拦截的定义.（何地）
>
> **Spring框架提供以下几种类型的通知：**
>
> 1. 前置通知：先执行方面功能再执行目标功能
> 2. 后置通知：先执行目标功能再执行方面功能（目标无异常才执行方面）
> 3. 最终通知：先执行目标功能再执行方面功能(目标功能有无异常都执行方面)
> 4. 异常通知：先执行目标，抛出后执行方面
> 5. 环绕通知：先执行方面强制部分，然后执行目标，最后再执行方面后置部分
>
> ```java
> /*可以按照下面的try...catch...finally结构来理解/*/        
> 		try {
> //            前置通知-执行部分
> //            环绕通知前置部分
> //            环绕目标组件方法
> //            环绕通知后置部分
> //            后置通知执行部分
>         }catch(){
> //            异常通知执行部分
>         }finally {
> //            最终通知执行部分
> 
>         }
> ```
>
> 实现方式有两种 **静态代理和动态代理**
>

### **静态代理**：

代理类编译阶段生成 编译时增强 AspectJ就是静态代理  简单实现如下：

> ```java
>public class ProxyTest implements TestInterface {
>     //也实现目标接口，但是还包含目标对象的引用。
>    TestInterface Interface;
>     ProxyTest(TestInterface testInterface){
>         this.Interface=testInterface;
>     }
>    @Override
>     public void s_out() {
>        System.out.println("切面方法a");
>         this.Interface.s_out();//目标类的目标方法 (横向业务流：对应示意图的方法5();
>         System.out.println("切面方法f");
>     }
> }
> class ProxyTestMain{
>    public static void main(String[] args) {
>         //横向业务流：方法1();
>         TestInterface face = new ProxyTest(new TestObject());
>         face.s_out();///代理对象来代理目标对象，执行目标方法。
>         //横向业务流：方法7();
>     }
> }
> class TestObject implements TestInterface {
>     @Override//实现目标接口
>     public void s_out() {
>         System.out.println("实现方法");
>     }
> }
> interface TestInterface {
>     void s_out();//定义目标方法
> }
>```
> 
>**实现步骤：**
> 
>![](https://img-blog.csdn.net/20161009162557378)
> 
> ```java
> //完整案例
> interface TestInterface {//接口定义抽象想做的事 比如说批发钟薛糕
>     float initPrice =2;//单件钟薛糕成本原料价
>     float Initial(int count);//定义批发的这件事
> }
> class TestObject implements TestInterface {//商家最先实现生产
>     //实现接口 已知厂家的单件成本价2
>     float Price = initPrice + 5;//加价五元做批发
>     @Override//实现目标接口批发方法
>     public float Initial(int count) {
>         System.out.println("商家：");
>         System.out.println("我这里批发单件钟薛糕"+Price+"元");
>         System.out.println("你在我这批发了"+count+"件");
>         System.out.println("收你"+Price *count+"元");
>         System.out.println("实际上我赚取了"+(Price-initPrice)*count+"件");
>         return Price *count;
>     }
> }
> public class ProxyTest extends TestObject implements TestInterface {//开超市
>     float Price = super.Price+ 5;//加价五元做零售
>     //也实现目标接口，但是还包含目标对象的引用。
>     TestInterface Interface;
>     ProxyTest(TestInterface testInterface){//找到联系厂家的方式
>         this.Interface=testInterface;
>     }
>     @Override//实现目标接口批发方法
>     public float Initial(int count) {
>         //切面方法a();
>         System.out.println("超市：");
>         System.out.println("我这里卖单件钟薛糕"+Price+"元");
>        System.out.println("你在我这买了"+count+"件");
>         System.out.println("收你"+Price *count+"元");
>        System.out.println("实际上我赚取了"+5*count+"元");
>         //切面方法f();
>        return Price *count;
>     }
> }
> class ProxyTestMain{
>     public static void main(String[] args) {
>         System.out.println("买多少根钟薛糕？？");
>         Scanner scanner = new Scanner(System.in);
>         int count = scanner.nextInt();
>         System.out.println("每卖"+count+"跟钟薛糕产生的数据：");
>         TestObject testObject = new TestObject();
>         testObject.Initial(count);
>         //横向业务流：方法1();
>         TestInterface face = new ProxyTest(testObject);//开了个超市做代理 参数是商家
>         face.Initial(count);///代理对象来代理目标对象，执行目标方法。
>         //横向业务流：方法7();
>     }
> }
> /**买多少根钟薛糕？？
> 10
> 每卖10跟钟薛糕
> 商家：
> 我这里批发单件钟薛糕7.0元
> 你在我这批发了10件
> 收你70.0元
> 实际上我赚取了50.0件
> 超市：
> 我这里卖单件钟薛糕12.0元
> 你在我这买了10件
> 收你120.0元
> 实际上我赚取了50元**/
> ```
> 

### **动态代理：**

> 代理类运行时创建 aop框架不会修改字节码 在内存中临时生成一个代理对象 在运行期间对业务进行增强 不会产生新的类
>
> 而Spring AOP是基于**动态代理**的，基于两种动态代理机制： **JDK动态代理**和**CGLIB动态代理**
>

####  **JDK动态代理**：

> **目标类如果实现了接口 SpringAOP会自动采用JDK动态代理方式代理目标类**
>
> - 动态代理类跟目标类实现的接口动态生成 无需编写 
>
> - 生成的目标类和动态代理类都实现同样的
> 
> - JDK动态代理的核心是java.lang.reflect(反射包)里面有三个类：InvocationHandler, Method, Proxy
>
> - 没有实现接口就无法使用JDK动态代理
>
>   ```java
>   //JDK动态代理实例
>   public class ServiceProxy {
>   /**
>    * 基于接口的动态代理
>   * 对于一些需要重复执行的验证功能或下一步操作,
>    * 在核心方法执行前后都会执行增强的功能
>    */
>       public static Object newProxyInstance(Object target){
>       return Proxy.newProxyInstance(target.getClass().getClassLoader(),target.getClass().getInterfaces(), (proxy, method, args) -> {
>           System.out.println("动态增强功能1:登录权限认证");
>           System.out.println("动态增强功能2:黑名单验证");
>           System.out.println("----------------------");
>           Object invoke = method.invoke(target, args);//执行被代理的核心业务功能
>           System.out.println("----------------------");
>           System.out.println("动态增强功能3:进入订单中心");
>           return invoke;
>       });}}
>   interface UserServiceTest {//User业务方法
>       void testUserService();
>   }
>    @Service
>   class UServiceImpl implements UserServiceTest {//User业务方法实现
>      @Override
>       public void testUserService() {
>          System.out.println("User核心功能业务Service");
>       }
>   }
>   interface OrderServiceTest {//Order业务方法
>       void testOrderService();
>   }
>   @Service
>   class OServiceImpl implements OrderServiceTest {//Order业务方法实现
>       @Override
>       public void testOrderService() {
>           System.out.println("Order核心功能业务Service");
>       }
>   }
>   class ServiceProxyTest{//Test类
>       public static void main(String[] args) {
>           UserServiceTest userService= new UServiceImpl();
>           userService = (UserServiceTest)ServiceProxy.newProxyInstance(userService);
>           userService.testUserService();
>           System.out.println("==========================");
>           OrderServiceTest orderService=new OServiceImpl();
>           orderService = (OrderServiceTest)ServiceProxy.newProxyInstance(orderService);
>           orderService.testOrderService();
>       }
>   }
>   /**动态增强功能1:登录权限认证
>   动态增强功能2:黑名单验证
>   ----------------------
>   User核心功能业务Service
>   ----------------------
>   动态增强功能3:进入订单中心
>   ==========================
>   动态增强功能1:登录权限认证
>   动态增强功能2:黑名单验证
> ----------------------
>   Order核心功能业务Service
>  ----------------------
>   动态增强功能3:进入订单中心**/
>  ```
> 

#### **CGLIB动态代理：**

> **如果目标类没有实现接口 SpringAOP会自动采用CGLIB动态代理方式代理目标类**
>
> - 通过继承实现
>
> - 运行时动态生成类的字节码 动态创建目标类子类对象 在子类对象中增强目标类
> 
> - 无需实现特定接口 更加灵活
>
>   ```java
>    //CGLIB动态代理实例
>   public class CGLIBProxy {//CGLIB动态代理类
>       public static Object newProxyInstance(Object target) {
>           //1.工具类
>           Enhancer enhancer = new Enhancer();
>           //2.设置父类,传递类对象
>          enhancer.setSuperclass(target.getClass());
>           //3.设置回调函数
>           enhancer.setCallback((MethodInterceptor) (o, method, objects, methodProxy) -> {
>               System.out.println("cglib增强功能1");
>               System.out.println("cglib增强功能2");
>               System.out.println("-------------");
>               return method.invoke(target, objects);
>           });
>           //4.功能增强后，返回代理对象
>           return enhancer.create();
>       }
>   }
>   class UserServiceCGLIB{
>       public void testUserService() {
>           System.out.println("User核心功能业务Service");
>       }
>    }
>   class OrderServiceCGLIB {
>      public void testOrderService() {
>           System.out.println("Order核心功能业务Service");
>      }
>   }
>   class CGLIBTest {
>       public static void main(String[] args) {
>           UserServiceCGLIB us_cglib = new UserServiceCGLIB();
>           us_cglib= (UserServiceCGLIB)CGLIBProxy.newProxyInstance(us_cglib);
>           us_cglib.testUserService();
>           System.out.println("======================");
>           OrderServiceCGLIB os_cglib=new OrderServiceCGLIB();
>           os_cglib=(OrderServiceCGLIB)CGLIBProxy.newProxyInstance(os_cglib);
>           os_cglib.testOrderService();
>       }
>   }
>   /**cglib增强功能1
>   cglib增强功能2
>   -------------
>   User核心功能业务Service
>   ======================
>   cglib增强功能1
>   cglib增强功能2
>   -------------
>   Order核心功能业务Service**/
>   ```

-----------------------

---

# SpringBoot

1. 简化配置，SpringBoot的核心思想就是**约定大于配置**，省去xml配置

2. 简化部署，内置Tomcat，可以快速启动应用，以jar包的形式

3. 简化依赖，开发web应用，我们只需要在pom文件中添加如下一个 starter-web 依赖即可

   ```java
   <dependency>
       <groupId>org.springframework.boot</groupId>
       <artifactId>spring-boot-starter-web</artifactId>
   </dependency>
   ```

---

## Springboot的核心注解

**@SpringBootApplication ** 包含如下组合注解

- **@SpringBootConfiguration**：声明当前类是SpringBoot应用的配置类 又包括：

  @Configuration **主类上使用的注解** 等同于spring的XML<beans></beans>配置文件 指出该类是 **Bean 配置的信息源**

  @Bean 在**方法上使用的注解** 等同于<bean></bean> **声明一个Bean并且交给Spring管理**

  @ComPonent 声明 泛指各种组件 类不属于各种归类时(Controller services Repository等) 就用该注解标记此类

- **@EnableAutoConfiguration**：开启自动配置 也可以通过exclude属性关闭某个自动配置的Class

  ```yaml
  如关闭数据源自动配置功能： @SpringBootApplication(exclude = { DataSourceAutoConfiguration.class })；
  ```

  @AutoConfiggurationPackage 保存标注相关注解的类的所在包路径 使用一个BasePackage类保存路径 使用@Import注解将其注入到ioc容器中 < @Import(AutoConfiguartionPackages.Registrar.Class) >

  @Import 用来**导入其他配置类 **<@Import (AutoConfiguartionImportSelector.Class)>

- **@ComponentScan**：扫描Spring组件 通过**basePackageClasses**或者**basePackages**属性来指定要扫描包的路径 不指定我就扫自己包以及子包

- @ImportResource 加载xml配置文件

- @Autowired 自动注入依赖的bean 通过类型bytype方式 自动装配属性方法

- @Resource 默认byName方式注入 

---

## Starters

stater作用就是加载项目启动所需要的的相关jar包，不用去一个个找jar包pom了，一键式 只需要添加对应依赖即可。

---

## SpringBoot容器功能

### 1.组件添加 

- @Configuration  配置类 == 配置文件 **默认单例Full模式** 配置类本身也是组件

  属性 proxyBeanMethods 

  **Full模式**：`@Configuration(proxyBeanMethods = true)` 保证@Bean组件多少次使用返回都是单实例
  **Lite模式**：`@Configuration(proxyBeanMethods = false)  `保证@Bean组件多少次使用返回都是新建的

- @Bean 给容器中添加组件。以方法名作为组件的id。返回类型就是组件类型。返回的值，就是组件在容器中的实例。

- @ComponentScan Spring 组件扫描
- @Import 导入其他配置类
- @Conditional 条件装配

### 2.原生配置文件引入

- @ImportResource 导入原生配置文件 `@ImportResource("classpath:beans.xml")`

### 3.配置绑定 

读取properties文件内容 并封装到 JavaBean 中 供随时使用

- @ConfigurationProperties + @EnableConfigurationProperties
- @Component + @Configurationproperties

---

## 异常处理

- 在Controller方法中使用 @ExceptionHandler 处理**局部异常 **controller外的异常无法处理
- 使用@ControllerAdvice + @ExceptionHandler 注解处理**全局异常**（开发中常用）
- 配置 **SimpleMappingExceptionResolver** 类处理异常
- 实现 **HandlerExceptionResolver** 接口处理异常

---

## 事务   <Transactional>

- **声明式事务**： 通过**<u>AOP面向切面</u>**在方法前开启事务 方法后**提交**或**回滚 **通常用用配置文件或注解**@Transactional**控制事务
- **编程式事务**：**手动** 开启、提交、回滚事务。

操作：事务提交 or 事务回滚

```yaml
#example小明给如花转账：
开启事务--- 1.从小明的账户扣除1000块 2.给如花的账户增加1000块
事务提交--- 以上两步骤任意一个步骤出现问题 都会导致事务回滚
通俗来讲 从搭讪到结婚就是事务提交，女方要求男方重新追求她一次，就是事务回滚。
```

### 事务的四大特性 

1. **原子性(Atomicity):**事务中所有操作是不可分割的原子单位。事务中所有操作要么全部执行成功，要么全部执行失败。
2. **一致性(Consistency):**事务执行后，数据库状态与其它业务规则保持一致。如转正业务，无论事务执行成功与否，参与转账的两个账号余额之和应该是不变的。
3. **隔离性(Isolation):**隔离性是指在并发操作中，不同事务之间应该隔离开来，使每个并发中的事务不会相互干扰。
4. **持久性(Durability):**一旦事务提交成功，事务中所有的数据操作都必须被持久化到数据库中，即使提交事务后，数据库马上崩溃，在数据库重启时，也必须你能保证通过某种机制恢复数据。

### 事务的传播特性

指的就是当一个事务方法被另一个事务方法调用时，这个事务方法应该**如何进行**。

spring总共给出了7种事务传播特性：

1.**死活不要事务的**

- propagation_never: 没有就非事务执行，有就抛出异常。
- propagation_not_supported: 没有就非事务执行，有就直接挂起，然后非事务执行。

2.**可有可无**

- propagation_supports: 有就用，没有就算了

3.**必须有事务的**

- propagation_requires_new: 有没有都新建事务，如果原来有，就将原来的挂起。**里面的事务，和外面事务是完全隔离的，互不影响的，外面事务不影响里面的事务，里面的事务也不影响外面的事务。**

- propagation_nested: 如果没有，就新建一个事务，如果有，就在当前事务中嵌套其他事务。**外面的事务回滚的时候会影响里面的事务，但是，里面的事务不影响外面的事务。**
- propagation_requered: 如果没有，就新建一个事务，如果有，就加入当前事务。
- propagation_mandatory: 如果没有，就抛出异常，如果有，就使用当前事务。

### 事务的隔离级别

数据库事务的隔离级别**由低到高**有4种，

1. Read uncommitted(**读未提交**)  一个事务可以读取另一个未提交事务的数据，会产生**脏读**。
2. Read committed(**读已提交**) 一个事务要等另一个事务提交后才能读取数据，会产生**不可重复读**。
3. Repeatable read(**可重复**）就是在开始读取数据(事务开启)时，不再允许修改操作。可能会产生**幻读**。
4. Serializable(**可串行化**)  **最高的事务隔离级别**  可以**避免脏读，不可重复读、与幻读**。效率低下 一般不使用。

```yaml
#数据库默认隔离等级知识
Sql Server Oracle ：读已提交 Read committed
Mysql ：可重复 Repeatable read
```

*在事务的**并发操作中**可能会出现**脏读**，**不可重复读**、**幻读**、**事务丢失**。*

**脏读**：读取了未提交的新事物，然后被回滚了

**不可重复读**：读取了提交的新事务，指更新操作

**幻读**：也是读取了提交的新事务，指增删操作

**事务丢失**：

- 回滚丢失

A和B同时在执行一个数据，然后B事务已经提交了，然后A事务回滚了，这样B事务的操作就因A事务回滚而丢失了。

- 提交覆盖丢失

A和B一起执行一个数据，两个同时取到一个数据，然后，B事务首先提交，但是，A事务接下来又提交，这样就覆盖了B事务。

### **事务总结**

- 读未提交：别人改数据的事务尚未提交，我在我的事务中也能读到。
- 读已提交：别人改数据的事务已经提交，我在我的事务中才能读到。
- 可重复读：别人改数据的事务已经提交，我在我的事务中也不去读。
- 串行：我的事务尚未提交，别人就别想改数据。
- 这4种隔离级别，并行性能依次降低，安全性依次提高。

---

## *Spring Boot自动配置原理？*

Spring Boot通过@EnableAutoConfiguration注解开启自动配置，对jar包下的META-INF/spring.factories文件进行扫描，这个文件中包含了可以进行自动配置的类，当满足@Condition注解指定的条件时，便在依赖的支持下进行实例化，注册到Spring容器中。

简单点说以上过程就是：getCandidateConfigurations()方法通过SpringFactoriesLoader加载器加载META-INF/spring.factories文件——>通过这个文件获取到每个配置类的url——>通过这些url将它们封装成Properties对象——>解析内容存于Map<String,List>中——>通过loadFactoryNames传递过来的class名称作为Key从Map中获得该类的配置列表——>getCandidateConfigurations（）方法获取到了配置类并存于List中——>通过selectImports（）方法返回一个自动配置类的全限定名数组。配置类需要在满足@Condition后才能真正的被注册到Spring容器之中。

**<u>如何在SpringBoot启动的时候运行一些特定的代码？</u>**

可以实现接口**ApplicationRunner**或者**CommandLineRunner**的run()方法

## *Spring  MVC 的处理流程？*

1. **DispatcherServlet** 前端处理器处理收到请求
2. 请求 **HandlerMapping** 找出容器中被 @Controler 注解修饰的 Bean 以及被 @RequestMapping 修饰的方法和类 生成 **Handler 和 HandlerInterceptor** 并返回一个**处理器执行链**。
3. 之后 DispatcherServlet **使用 Handler 找到对应的 HandlerApapter**，通过 HandlerApapter 调用 Handler的方法，**将请求参数绑定到方法的形参上**，执行方法处理请求并得到 ModelAndView。
4. 最后 DispatcherServlet 根据使用 ViewResolver 视图解析器对得到的 ModelAndView 逻辑视图进行解析得到 View 物理视图，然后对视图渲染，将数据填充到视图中并返回给客户端。

## *Spring事务失效问题?*

Spring事务：数据库对**事务 <u>@Transactional</u> **的支持

1. 获取连接 Connection con = DriverManager.getConnection()
2. 开启事务con.setAutoCommit(true/false);
3. 执行CRUD
4. 提交事务/回滚事务 con.commit() / con.rollback();
5. 关闭连接 conn.close();

失效原因:

- 数据库引擎不支持事务

Spring事务生效的前提是连接的数据库底层要支持事务 

例如 Mysql默认引擎MyISAM就不支持事务 InnoDB和BDB就支持事务

- 事务方法未被Spring管理

事务方法所在的类没有加载到Spring IOC容器中 没有被加载为Bean 即没有被Spring管理

```java
public class ProductService {
 @Autowired
 private ProductDao productDao;
 
 @Transactional(propagation = Propagation.REQUIRES_NEW)
 public void updateProductStockCountById(Integer stockCount, Long id){
  productDao.updateProductStockCountById(stockCount, id);
 }
}
//ProductService类上没有标注@Service注解，Product的实例没有加载到Spring IOC容器中
```

- 方法没有被public修饰

如果事务所在的方法没有被public修饰，此时Spring的事务会失效  Spring 官方文档规定

- 同一类中方法调用

自身调用问题 同一个类中的两个方法分别为A和B，方法A上没有添加事务注解，方法B上添加了 @Transactional事务注解，方法A调用方法B，则方法B的事务会失效

- 未配置事务管理器

如果在项目中没有配置Spring的事务管理器，即使使用了Spring的事务管理功能，Spring的事务也不会生效。

```java
//未在配置类配置如下代码
@Bean
public PlatformTransactionManager transactionManager(DataSource dataSource) {
 return new DataSourceTransactionManager(dataSource);
}
```

- 不正确的捕获异常

把异常吃了，然后又不抛出来，事务怎么回滚吧！ 

```java
@Service
public class OrderService {
 @Autowired
 private OrderDao orderDao;
 @Autowired
 private ProductDao productDao;
 @Transactional(propagation = Propagation.REQUIRED)
 public void submitOrder(){
  //生成订单
  Order order = new Order();
  long number = Math.abs(new Random().nextInt(500));
  order.setId(number);
  order.setOrderNo("order_" + number);
  orderDao.saveOrder(order);
  //减库存
  this.updateProductStockCountById(1, 1L);
 }
 
 @Transactional(propagation = Propagation.REQUIRED)
 public void updateProductStockCountById(Integer stockCount, Long id){
  try{
   productDao.updateProductStockCountById(stockCount, id);
   int i = 1 / 0;
  }catch(Exception e){
   logger.error("扣减库存异常:", e.getMesaage());
  }}}
```

updateProductStockCountById()方法中使用try-catch代码块捕获了异常，即使updateProductStockCountById()方法内部会抛出异常，但也会被catch代码块捕获到，此时updateProductStockCountById()方法的事务会提交而不会回滚，并且submitOrder()方法的事务会提交而不会回滚，这就造成了Spring事务的回滚失效问题。

- 错误的标注异常类型

```java
@Transactional(propagation = Propagation.REQUIRED)
public void updateProductStockCountById(Integer stockCount, Long id){
 try{
  productDao.updateProductStockCountById(stockCount, id);
 }catch(Exception e){
  logger.error("扣减库存异常:", e.getMesaage());
  throw new Exception("扣减库存异常");
 }
}
```

因为Spring中对于默认回滚的事务异常类型为RuntimeException，上述代码抛出的是Exception异常。即事务回滚会失效

解决方法：手动指定标注的事务异常类型

```java
@Transactional(propagation = Propagation.REQUIRED,rollbackFor = Exception.class)
//Spring事务注解@Transactional中的rollbackFor属性可以指定 Throwable 异常类及其子类。
```

---

---

# 容器集合

Java中集合框架被设计成要满足以下几个目标。

- 该框架必须是高性能的。基本集合（动态数组，链表，树，哈希表）的实现也必须是高效的。
- 该框架允许不同类型的集合，以类似的方式工作，具有高度的互操作性。
- 对一个集合的扩展和适应必须是简单的。

为此，整个集合框架就围绕一组标准接口而设计。你可以直接使用这些接口的标准实现，诸如： **LinkedList**, **HashSet**, 和 **TreeSet** 等,除此之外你也可以通过这些接口实现自己的集合。

![img](https://www.runoob.com/wp-content/uploads/2014/01/2243690-9cd9c896e0d512ed.gif)

从上面的集合框架图可以看到，Java 集合框架主要包括两种类型的容器，**一种是集合（Collection）**，存储一个元素集合，**另一种是图（Map）**，存储键/值对映射。**Collection 接口又有 3 种子类型，List、Set 和 Queue，**再下面是一些抽象类，最后是具体实现类，常用的有 <u>ArrayList、LinkedList、HashSet、LinkedHashSet、HashMap、LinkedHashMap</u> 等等。

集合框架是一个用来代表和操纵集合的统一架构。所有的集合框架都包含如下内容：

- **接口：**是代表集合的抽象数据类型。例如 Collection、List、Set、Map 等。之所以定义多个接口，是为了以不同的方式操作集合对象
- **实现（类）：**是集合接口的具体实现。从本质上讲，它们是可重复使用的数据结构，例如：ArrayList、LinkedList、HashSet、HashMap。
- **算法：**是实现集合接口的对象里的方法执行的一些有用的计算，例如：搜索和排序。这些算法被称为多态，那是因为相同的方法可以在相似的接口上有着不同的实现。

除了集合，该框架也定义了几个 Map 接口和类。Map 里存储的是键/值对。尽管 Map 不是集合，但是它们完全整合在集合中。

**集合框架体系如图所示**：

![img](https://www.runoob.com/wp-content/uploads/2014/01/java-coll-2020-11-16.png)

## 集合接口

集合框架定义了一些接口。本节提供了每个接口的概述：

| 序号 | 接口描述                                                     |
| :--- | :----------------------------------------------------------- |
| 1    | **Collection 接口** ：Collection 是最基本的集合接口，一个 Collection 代表一组 Object，即 Collection 的元素, Java不提供直接继承自Collection的类，只提供继承于的子接口(如List和set)。Collection 接口存储一组不唯一，无序的对象。 |
| 2    | **List 接口：** List接口是一个有序的 Collection，使用此接口能够精确的控制每个元素插入的位置，能够通过索引(元素在List中位置，类似于数组的下标)来访问List中的元素，第一个元素的索引为 0，而且允许有相同的元素。List 接口存储一组不唯一，有序（插入顺序）的对象。 |
| 3    | **Set：** Set 具有与 Collection 完全一样的接口，只是行为上不同，Set 不保存重复的元素。Set 接口存储一组唯一，无序的对象。 |
| 4    | **SortedSet：** 继承于Set保存有序的集合。                    |
| 5    | **Map：** Map 接口存储一组键值对象，提供key（键）到value（值）的映射。 |
| 6    | **Map.Entry：** 描述在一个Map中的一个元素（键/值对）。是一个 Map 的内部接口。 |
| 7    | **SortedMap：** 继承于 Map，使 Key 保持在升序排列。          |
| 8    | **Enumeration**： 这是一个传统的接口和定义的方法，通过它可以枚举（一次获得一个）对象集合中的元素。这个传统接口已被迭代器取代。 |

### Set和List的区别

1. Set 接口实例存储的是无序的，不重复的数据。List 接口实例存储的是有序的，可以重复的元素。
2. Set 检索效率低下，删除和插入效率高，插入和删除不会引起元素位置改变 **<实现类有HashSet,TreeSet>**。
3. List 和数组类似，可以动态增长，根据实际存储的数据的长度自动增长 List 的长度。查找元素效率高，插入删除效率低，因为会引起其他元素位置改变 **<实现类有ArrayList,LinkedList,Vector>** 。

## 集合实现类（集合类）

Java提供了一套实现了Collection接口的标准集合类。其中一些是具体类，这些类可以直接拿来使用，而另外一些是抽象类，提供了接口的部分实现。

标准集合类汇总于下表：

| 序号 | 类描述                                                       |
| :--- | :----------------------------------------------------------- |
| 1    | **AbstractCollection**  实现了大部分的集合接口。             |
| 2    | **AbstractList**  继承于AbstractCollection 并且实现了大部分List接口。 |
| 3    | **AbstractSequentialList**  继承于 AbstractList ，提供了对数据元素的链式访问而不是随机访问。 |
| 4    | [LinkedList](https://www.runoob.com/java/java-linkedlist.html) 该类实现了List接口，允许有null（空）元素。主要用于创建链表数据结构，该类没有同步方法，如果多个线程同时访问一个List，则必须自己实现访问同步，解决方法就是在创建List时候构造一个同步的List。例如：`List list=Collections.synchronizedList(newLinkedList(...));`LinkedList 查找效率低。 |
| 5    | [ArrayList](https://www.runoob.com/java/java-arraylist.html) 该类也是实现了List的接口，实现了可变大小的数组，随机访问和遍历元素时，提供更好的性能。该类也是非同步的,在多线程的情况下不要使用。ArrayList 增长当前长度的50%，插入删除效率低。 |
| 6    | **AbstractSet**  继承于AbstractCollection 并且实现了大部分Set接口。 |
| 7    | [HashSet](https://www.runoob.com/java/java-hashset.html) 该类实现了Set接口，不允许出现重复元素，不保证集合中元素的顺序，允许包含值为null的元素，但最多只能一个。 |
| 8    | LinkedHashSet 具有可预知迭代顺序的 `Set` 接口的哈希表和链接列表实现。 |
| 9    | TreeSet 该类实现了Set接口，可以实现排序等功能。              |
| 10   | **AbstractMap**  实现了大部分的Map接口。                     |
| 11   | [HashMap](https://www.runoob.com/java/java-hashmap.html) HashMap 是一个散列表，它存储的内容是键值对(key-value)映射。 该类实现了Map接口，根据键的HashCode值存储数据，具有很快的访问速度，最多允许一条记录的键为null，不支持线程同步。 |
| 12   | TreeMap 继承了AbstractMap，并且使用一颗树。                  |
| 13   | WeakHashMap 继承AbstractMap类，使用弱密钥的哈希表。          |
| 14   | LinkedHashMap 继承于HashMap，使用元素的自然顺序对元素进行排序. |
| 15   | IdentityHashMap 继承AbstractMap类，比较文档时使用引用相等。  |

在前面的教程中已经讨论通过java.util包中定义的类，如下所示：

| 序号 | 类描述                                                       |
| :--- | :----------------------------------------------------------- |
| 1    | Vector 该类和ArrayList非常相似，但是该类是同步的，可以用在多线程的情况，该类允许设置默认的增长长度，默认扩容方式为原来的2倍。 |
| 2    | Stack 栈是Vector的一个子类，它实现了一个标准的后进先出的栈。 |
| 3    | Dictionary Dictionary 类是一个抽象类，用来存储键/值对，作用和Map类相似。 |
| 4    | Hashtable Hashtable 是 Dictionary(字典) 类的子类，位于 java.util 包中。 |
| 5    | Properties Properties 继承于 Hashtable，表示一个持久的属性集，属性列表中每个键及其对应值都是一个字符串。 |
| 6    | BitSet 一个Bitset类创建一种特殊类型的数组来保存位值。BitSet中数组大小会随需要增加。 |

## 如何使用迭代器？

通常情况下，你会希望遍历一个集合中的元素。例如，显示集合中的每个元素。

一般遍历数组都是采用for循环或者增强for，这两个方法也可以用在集合框架，但是还有一种方法是采用迭代器遍历集合框架，它是一个对象，实现了[Iterator](https://www.runoob.com/java/java-iterator.html) 接口或 ListIterator接口。

迭代器，使你能够通过循环来得到或删除集合的元素。ListIterator 继承了 Iterator，以允许双向遍历列表和修改元素。

| 序号 | 迭代器方法描述                                               |
| :--- | :----------------------------------------------------------- |
| 1    | [使用 Java Iterator](https://www.runoob.com/java/java-iterator.html) 这里通过实例列出 Iterator 和 ListIterator 接口提供的所有方法。 |

### 遍历 ArrayList

```java
//实例
import java.util.*;
 
public class Test{
 public static void main(String[] args) {
     List<String> list=new ArrayList<String>();
     list.add("Hello");
     list.add("World");
     list.add("HAHAHAHA");
     //第一种遍历方法使用 For-Each 遍历 List
     for (String str : list) {            //也可以改写 for(int i=0;i<list.size();i++) 这种形式
        System.out.println(str);
     }
 
     //第二种遍历，把链表变为数组相关的内容进行遍历
     String[] strArray=new String[list.size()];
     list.toArray(strArray);
     for(int i=0;i<strArray.length;i++) //这里也可以改写为  for(String str:strArray) 这种形式
     {
        System.out.println(strArray[i]);
     }
     
    //第三种遍历 使用迭代器进行相关遍历
     
     Iterator<String> ite=list.iterator();
     while(ite.hasNext())//判断下一个元素之后有值
     {
         System.out.println(ite.next());
     }
 }
}
//解析：
//三种方法都是用来遍历ArrayList集合，第三种方法是采用迭代器的方法，该方法可以不用担心在遍历的过程中会超出集合的长度。
```

### 遍历 Map

```java
//实例
import java.util.*;
 
public class Test{
     public static void main(String[] args) {
      Map<String, String> map = new HashMap<String, String>();
      map.put("1", "value1");
      map.put("2", "value2");
      map.put("3", "value3");
      
      //第一种：普遍使用，二次取值
      System.out.println("通过Map.keySet遍历key和value：");
      for (String key : map.keySet()) {
       System.out.println("key= "+ key + " and value= " + map.get(key));
      }
      
      //第二种
      System.out.println("通过Map.entrySet使用iterator遍历key和value：");
      Iterator<Map.Entry<String, String>> it = map.entrySet().iterator();
      while (it.hasNext()) {
       Map.Entry<String, String> entry = it.next();
       System.out.println("key= " + entry.getKey() + " and value= " + entry.getValue());
      }
      
      //第三种：推荐，尤其是容量大时
      System.out.println("通过Map.entrySet遍历key和value");
      for (Map.Entry<String, String> entry : map.entrySet()) {
       System.out.println("key= " + entry.getKey() + " and value= " + entry.getValue());
      }
    
      //第四种
      System.out.println("通过Map.values()遍历所有的value，但不能遍历key");
      for (String v : map.values()) {
       System.out.println("value= " + v);
      }
     }
}
```

## 如何使用比较器？

TreeSet和TreeMap的按照排序顺序来存储元素. 然而，这是通过比较器来精确定义按照什么样的排序顺序。

这个接口可以让我们以不同的方式来排序一个集合。

| 序号 | 比较器方法描述                                               |
| :--- | :----------------------------------------------------------- |
| 1    | 使用 Java Comparator 这里通过实例列出Comparator接口提供的所有方法 |

## 总结

Java集合框架为程序员提供了预先包装的数据结构和算法来操纵他们。

集合是一个对象，可容纳其他对象的引用。集合接口声明对每一种类型的集合可以执行的操作。

集合框架的类和接口均在java.util包中。

任何对象加入集合类后，自动转变为Object类型，所以在取出的时候，需要进行强制类型转换。

## ArrayList

**ArrayList 继承了 AbstractList.class ，并实现了 List 接口。**<u>非线程安全 动态数组结构 随机访问get/set快 自动扩容1.5倍</u>

![img](https://www.runoob.com/wp-content/uploads/2020/06/ArrayList-1-768x406-1.png)

ArrayList 类是一个可以动态修改的数组，与普通数组的区别就是它是没有固定大小的限制，我们可以添加或删除元素。

```java
//E: 泛型数据类型，用于设置 objectName 的数据类型，只能为引用数据类型,例如一些基本数据类型的包装类和一些常用的引用类型对象。
import java.util.ArrayList; // 引入 ArrayList 类
ArrayList<E> objectName =new ArrayList<>();　 // 初始化
```

## LinkedList

链表（Linked list）是一种常见的基础数据结构，是一种线性表，但是并不会按线性的顺序存储数据，而是在每一个节点里存到下一个节点的地址。

```java
// 引入 LinkedList 类
import java.util.LinkedList; 
LinkedList<E> list = new LinkedList<E>();   // 普通创建方法
//或者
LinkedList<E> list = new LinkedList(Collection<? extends E> c); // 使用集合创建链表
```

<u>非线程安全 双向链表结构 由于移动指针操作 所以插入删除(add/remove)快</u>

与 ArrayList 相比，LinkedList 的增加和删除的操作效率更高，而查找和修改的操作效率较低。

![img](https://www.runoob.com/wp-content/uploads/2020/06/linkedlist-2020-11-16.png)

1. LinkedList 继承了 AbstractSequentialList 类。
2. LinkedList 实现了 Queue 接口，可作为队列使用。
3. LinkedList 实现了 List 接口，可进行列表的相关操作。
4. LinkedList 实现了 Deque 接口，可作为队列使用。
5. LinkedList 实现了 Cloneable 接口，可实现克隆。
6. LinkedList 实现了 java.io.Serializable 接口，即可支持序列化，能通过序列化去传输。

## HashSet

**Hash算法** Hashmap(数组+链表)实现

 **非线程安全** **非有序 ** **元素可以为NULL  但只能有一个** 

HashMap默认初始化容量：16 必须是2的次幂 数组容量达到了3/4(0.75)开始扩容2倍

HashSet 是无序的，即不会记录插入的顺序。

实现对象相等需要重写hashcode()和equals()方法 对象相等必须具有相同散列码

**存取 查找 删除 性能好**

![img](https://www.runoob.com/wp-content/uploads/2020/07/java-hashset-hierarchy.png)

## HashMap

HashMap 是一个散列(hash)表，它存储的内容是键值对(key-value)映射。

JDK1.8以后的HashMap 当链表长度大于阈值（默认为8）时 会将链表转化为红黑树

HashMap 实现了 Map 接口，根据键的 HashCode 值存储数据，具有很快的访问速度，**最多允许一条记录的键为 null**，非线程安全。

HashMap 是无序的，即不会记录插入的顺序。

HashMap 继承于AbstractMap，实现了 Map、Cloneable、java.io.Serializable 接口。![img](https://www.runoob.com/wp-content/uploads/2020/07/WV9wXLl.png)

```java
HashMap<Integer, String> Sites = new HashMap<Integer, String>();
```

## Iterator（迭代器）

Java Iterator（迭代器）不是一个集合，它是一种用于访问集合的方法接口，可用于迭代 [ArrayList](https://www.runoob.com/java/java-arraylist.html) 和 [HashSet](https://www.runoob.com/java/java-hashset.html) 等集合。

![img](https://www.runoob.com/wp-content/uploads/2020/07/ListIterator-Class-Diagram.jpg)

迭代器 it 的两个基本操作是 next 、hasNext 和 remove。

调用 it.next() 会返回迭代器的下一个元素，并且更新迭代器的状态。

调用 it.hasNext() 用于检测集合中是否还有元素。

调用 it.remove() 将迭代器返回的元素删除。

```java
// 引入 ArrayList 和 Iterator 类
import java.util.ArrayList;
import java.util.Iterator;

public class RunoobTest {
    public static void main(String[] args) {
        // 创建集合
        ArrayList<String> sites = new ArrayList<String>();
        sites.add("Google");
        sites.add("Runoob");
        sites.add("Taobao");
        sites.add("Zhihu");
        // 获取迭代器
        Iterator<String> it = sites.iterator();

        // 输出集合中的所有元素
        while(it.hasNext()) {
            System.out.println(it.next());
        }
    }
}
```

## Serializable序列化

Java 提供了一种对象序列化的机制，该机制中，一个对象可以被表示为一个字节序列，该字节序列包括该对象的数据、有关对象的类型的信息和存储在对象中数据的类型。

将序列化对象写入文件之后，可以从文件中读取出来，并且对它进行反序列化，也就是说，对象的类型信息、对象的数据，还有对象中的数据类型可以用来在内存中新建对象。

整个过程都是 Java 虚拟机（JVM）独立的，也就是说，在一个平台上序列化的对象可以在另一个完全不同的平台上反序列化该对象。

请注意，一个类的对象要想序列化成功，必须满足两个条件：

1. 该类必须实现 java.io.Serializable 接口。
2. 该类的所有属性必须是可序列化的。如果有一个属性不是可序列化的，则该属性必须注明是短暂的。

```java
public class Employee implements java.io.Serializable
{
   public String name;
   public String address;
   public transient int SSN;
   public int number;
   public void mailCheck()
   {
      System.out.println("Mailing a check to " + name
                           + " " + address);
   }
}
```

序列化对象:

```java
import java.io.*;
 
public class SerializeDemo
{
   public static void main(String [] args)
   {
      Employee e = new Employee();
      e.name = "Reyan Ali";
      e.address = "Phokka Kuan, Ambehta Peer";
      e.SSN = 11122333;
      e.number = 101;
      try
      {
         FileOutputStream fileOut =
         new FileOutputStream("/tmp/employee.ser");
         ObjectOutputStream out = new ObjectOutputStream(fileOut);
         out.writeObject(e);
         out.close();
         fileOut.close();
         System.out.printf("Serialized data is saved in /tmp/employee.ser");
      }catch(IOException i)
      {
          i.printStackTrace();
      }
   }
}
```

反序列化对象:

```java
import java.io.*;
 
public class DeserializeDemo
{
   public static void main(String [] args)
   {
      Employee e = null;
      try
      {
         FileInputStream fileIn = new FileInputStream("/tmp/employee.ser");
         ObjectInputStream in = new ObjectInputStream(fileIn);
         e = (Employee) in.readObject();
         in.close();
         fileIn.close();
      }catch(IOException i)
      {
         i.printStackTrace();
         return;
      }catch(ClassNotFoundException c)
      {
         System.out.println("Employee class not found");
         c.printStackTrace();
         return;
      }
      System.out.println("Deserialized Employee...");
      System.out.println("Name: " + e.name);
      System.out.println("Address: " + e.address);
      System.out.println("SSN: " + e.SSN);
      System.out.println("Number: " + e.number);
    }
}
Deserialized Employee...
Name: Reyan Ali
Address:Phokka Kuan, Ambehta Peer
SSN: 0
Number:101
```

这里要注意以下要点：

readObject() 方法中的 try/catch代码块尝试捕获 ClassNotFoundException 异常。对于 JVM 可以反序列化对象，它必须是能够找到字节码的类。如果JVM在反序列化对象的过程中找不到该类，则抛出一个 ClassNotFoundException 异常。

注意，readObject() 方法的返回值被转化成 Employee 引用。

当对象被序列化时，属性 SSN 的值为 111222333，但是因为该属性是短暂的，该值没有被发送到输出流。所以反序列化后 Employee 对象的 SSN 属性为 0。



























































## Collection interface <extends Iterable>

- **单列**数据容器

- 实现了**collections**工具类以及**iterator**迭代器
- **Comparable**和**Comparator**对象排序接口

### List<E><interface extends Collection>

**<u>对付顺序的好帮手</u>**

- 拥有专属**Listiterator**迭代器
- 顺序存储 存放时顺序保持一致 可重复

1. **Vector** 线程安全 效率低  底层结构动态数组同Arraylist但是扩容是2倍
2. **ArrayList<典型实现>** 非线程安全 动态数组结构 随机访问get/set快 自动扩容1.5倍
3. **LinkedList** 非线程安全 双向链表结构 由于移动指针操作 所以插入删除(add/remove)快

---

### Set<E><interface extends Collection>

**<u>注重独一无二的性质</u>**

- 无顺序 不可重复元素 否则插入失败
- 判断对象相等使用`equals()`方法不使用 `==`

1.**HashSet<典型实现>**  <Class implements Set>

HashMap默认初始化容量：16 必须是2的次幂 数组容量达到了3/4(0.75)开始扩容2倍

**Hash算法** Hashmap(数组+链表)实现  **非线程安全** **非有序** **元素可以为NULL但只能有一个** 

实现对象相等需要重写hashcode()和equals()方法 对象相等必须具有相同散列码

存取 查找 删除 性能好

- LinkedHashSet   <class implements Set>

<u>**HashSet的子类**</u> 双向链表数据结构和哈希表 插入性能略低于父类 插入时遍历顺序保持一致

2.SortedSet 接口<interface extends Set>  

- 唯一实现类**TreeSet**<extends AbstractSet> 红黑树数据存储结构 默认自然排序(元素大小排序)或者定制排序 遍历保持由小到大 无重复 不允许放入NULL值

---

### Queue

**<u>实现排队功能的叫号机</u>**

按特定的排队规则来确定先后顺序 存储的元素是**有序**的 **可重复的** 

- queue 单向队列 
- deque 双向队列 ArrayDeque顺序表实现   LinkedList链表实现
- PriorityQueue 非线程安全 非NULL 实现了 `Serializable`

### HashSet插入时步骤？

1.先得到对象的hashcode值

2.判断hashcode值是否相等？

3.再比较对象实现的equals()方法

equals和hashcode分两种情况

- equals：false hashcode：ture 保存元素 数组已有位置通过链表链接
- equals：ture hashcode：false 添加元素成功 存储不同位置

### 如何将ArrayList变成线程安全的？

调用Collections工具类中的 static synchronizedList(List list)方法

### ArrayList如何去重？

- 使用HashSet去重 但是会影响元素原有位置 也可以使用LinkedHashSet保持元素原来的顺序

  ```java
  HashSet<String> objects = new HashSet<>(arr1);
  //或LinkedHashSet<Integer> hashSet = new LinkedHashSet<>(arr1);
  ```

- stream()的distinct()方法返回一个由不同数据组成的流 通过对象的equals()方法进行比较 

  ```java
  List<Integer> listWithoutDuplicates = numbersList.stream().distinct().collect(Collectors.toList());
  ```

- List的contains()循环遍历,重新排序,只添加一次数据,避免重复

  ```java
  for (String str : list) {
      if (!result.contains(str)) {
          result.add(str);
      }}
  ```

- 双重for循环去重

  ```java
  for (int i = 0; i < list.size(); i++) { 
      for (int j = 0; j < list.size(); j++) { 
          if(i!=j&&list.get(i)==list.get(j)) { 
              list.remove(list.get(j)); 
       } } }
  ```


---

## Map <interface>

**用 key 来搜索的专家**

- **双列**数据
- 保存具有映射关系的**K-V集合** key和value皆可以是任何类型
- 不允许重复 同一map对象对应对象必须重写hashcode和equlas方法
- JDK1.8以后的HashMap 当链表长度大于阈值（默认为8）时 会将链表转化为红黑树

1.**HashMap<典型实现>** hash散列算法实现 非线程安全 访问快 无序 以存储NULL的k和v 

2.LinkedHashMap 有序按添加顺序  访问慢 双向指针操作 非线程安全

3.TreeMap 按照添加k-v对进行排序 实现排序遍历 自然排序or定制排序 底层红黑树

4.Hashtable 线程安全的  效率低 不能存储null的key和value

5.Properties 常用来处理配置文件 key和value都是String类型 

---

## 枚举<extends ENUM>

特征：

- 无法继承 构造方法为私有 其他与常规类相同
- 不允许使用`=`复制给枚举常量
- enum可以有任意普通 静态 抽象 构造方法
- enum可以实现接口 

 继承自`java.lang.Enum`提供的常用方法  Enum 实现了**Serializable**和**Comparable**接口

- `values()` 数组顺序返回获取枚举类型的成员
- `ordinal()`方法可以找到每个枚举常量的索引，就像数组索引一样。
- `valueOf()`方法返回指定字符串值的枚举常量。

- `name()` 返回实例名
- `getDeclaringClass()` 返回实例所属的enum类型
- `equals()` 判断是否同一对象也可以使用`==`

工具类：

**Enumset**:枚举类型Set高效实现 要求放入它的枚举常量必须属于同一枚举类型

**EnumMap**:枚举类型Map高效实现 只接受同一枚举类型的实例作为键值 使用数组来存放与枚举类型对应的值

---

## 泛型 <E T K V N ?>

泛型是 JDK 5 中引入的一个新特性, 泛型提供了编译时类型安全检测机制，该机制允许程序员在编译时检测到非法的类型。

泛型的本质是参数化类型，也就是说所操作的数据类型被指定为一个参数。

```xml
假定我们有这样一个需求：写一个排序方法，能够对整型数组、字符串数组甚至其他任何类型的数组进行排序，该如何实现？
答案是可以使用 Java 泛型。
使用 Java 泛型的概念，我们可以写一个泛型方法来对一个对象数组排序。然后，调用该泛型方法来对整型数组、浮点数数组、字符串数组等进行排序。
```

**泛型类型在逻辑上看以看成是多个不同的类型，实际上都是相同的基本类型。**

- **E** - Element (在集合中使用，因为集合中存放的是元素)
- **T** - Type（Java 类）
- **K** - Key（键）
- **V** - Value（值）
- **N** - Number（数值类型）
- **？** - 表示不确定的 java 类型

---

## 线程安全的容器有哪些？

**同步容器类：<synchronized>**

- vector 线程安全的list 几乎不用

- HashTable 线程安全的Map 几乎不用

**并发容器**：

- ConcurrentHashMap: 使用较多 效率高(分段/CAS)再加synchronized保证同步操作 手动实现并发安全 用于并发几率低场景 
- CopyOnWriteArrayList：写时复制 常用于读多写少的并发环境
- CopyOnWriteArraySet：写时复制 常用于读多写少的并发环境

**Queue队列：**

- ConcurrentLinkedQueue **非阻塞**的方式实现的**基于链接节点**的**无界**的线程安全队列，性能非常好。
- ArrayBlockingQueue：基于**数组**的**有界阻塞队列**
- LinkedBlockingQueue：基于**链表**的**有界阻塞队列**
- PriorityBlockingQueue：**支持优先级**的**无界阻塞队列** 默认情况下元素自然升序排序

- DelayQueue： 延时获取元素的无界阻塞队列
- SynchronousQueue ：不存储元素的阻塞队列。每个put操作必须等待一个take操作，否则不能继续添加元素。内部其实没有任何一个元素，容量是0

**Deque：双向对列 允许在队列头和尾部进行入队出队操作**

- ArrayDeque:基于数组的双向非阻塞队列。
- LinkedBlockingDeque:基于链表的双向阻塞队列。

**Sorted容器：**

- ConcurrentSkipListMap：是TreeMap的线程安全版本
- ConcurrentSkipListSet：是TreeSet的线程安全版本

# 多线程与并发

## 多线程编程

多线程能满足程序员编写高效率的程序来达到充分利用 CPU 的目的。

Java 给多线程编程提供了内置的支持。 一条线程指的是进程中一个单一顺序的控制流，一个进程中可以并发多个线程，每条线程并行执行不同的任务。

多线程是多任务的一种特别的形式，但多线程使用了更小的资源开销。

## 进程

**执行程序的一次执行过程 也指正在运行的程序实体**

包括这个运行的程序中占据的所有系统资源，比如说CPU（寄存器），IO,内存，网络资源等。

同样一个程序，同一时刻被两次运行了，那么他们就是两个独立的进程。

一个操作系统中可以有多个进程，一个进程可以开启多个线程，其中有一个主线程来调用本进程中的其他线程。

## [线程](https://blog.csdn.net/qq_35598736/article/details/108431422?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522165984936416781432921249%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=165984936416781432921249&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~top_positive~default-2-108431422-null-null.142^v39^pc_rank_v36,185^v2^control&utm_term=%E5%A4%9A%E7%BA%BF%E7%A8%8B&spm=1018.2226.3001.4187)

JVM 执行任务的**运算调度的最小单位** ，它被**包含在进程之中**，一条线程指的是**进程中一个单一顺序的控制流**。

**多线程**可以让同一个进程同时**并发**处理多个任务

JVM中进程的六种状态 这些状态对应 **Thread.State** 枚举类中的状态 `<java.lang.Thread.State>`

1. **`NEW`**  **创建状态**

2. **`RUNNABLE`** **可运行状态**  运行 Thread 的 start 方法后 线程进入可运行状态

   可运行状态线程并不能马上运行   而是先进入**READY就绪状态**等待线程调度 在获取 CPU 后才能进入**RUNNING运行状态**  运行状态可以随着不同条件转换成除 NEW 以外的其他状态

3. **`BLOCKED`**  **阻塞状态** 运行进程进入 synchronized 同步块或同步方法时 获取锁失败 会进入BLOCKED状态 获取到锁后 会从BLOCKED状态恢复到就绪RUNNABLE状态 

4. **`WAITING` ** **等待状态**  wait()操作之后会释放锁 等待其他线程唤醒 获取到锁才能进入可运行状态

5. **`TIMED_WAITING`**  **有时间的等待 **sleep()或者join()操作先进入阻塞状态不会释放锁 时间结束或者等其他线程结束之前一直是属于等待状态

6. **`TERMINATED` ** **线程运行完成结束状态** 或者有异常发生 线程会进入死亡Dead状态

![多线程状态图](https://img-blog.csdnimg.cn/db36e894a0a843c6a36ca5a76cb3af2d.png)

![](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9wNi1qdWVqaW4uYnl0ZWltZy5jb20vdG9zLWNuLWktazN1MWZicGZjcC9lNGI3YTY3YTE2NDQ0NWYzYWE3ZjA1ZWVkNDAyM2I3OH50cGx2LWszdTFmYnBmY3Atem9vbS0xLmltYWdl?x-oss-process=image/format,png)

![对应枚举类状态](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9wNi1qdWVqaW4uYnl0ZWltZy5jb20vdG9zLWNuLWktazN1MWZicGZjcC8zOTlhNzYzODU5MzM0ZDYwOGYzZGMzMDA0NTgzODVlZX50cGx2LWszdTFmYnBmY3Atem9vbS0xLmltYWdl?x-oss-process=image/format,png)

## 并发与并行

**并发（Concurrent）**：一个时间段中有几个程序都处于已启动运行到运行完毕之间，且这几个程序都是在同一个处理机上运行。
同一时刻只能有一条指令执行，但多个进程指令被**快速的轮换执行**，使得在宏观上具有多个进程同时执行的效果，但在微观上并不是同时执行的，只是把**时间分成若干段，使多个进程快速交替的执行**。

**并行（Parallel）：**当系统有一个以上CPU时，当一个CPU执行一个进程时，另一个CPU可以执行另一个进程，两个进程互不抢占CPU资源，可以同时进行**真正的在同一时刻运行**，这种方式我们称之为并行 。

其实决定并行的因素不是CPU的数量，而是**CPU的核心数量**，比如一个CPU多个核也可以并行。

## 进程与线程的关系

- 进程是操作系统资源分配的基本单位，而线程是CPU的基本调度单位
- 一个进程由一个或多个线程(多线程)组成
- 进程之间相互独立，而线程共享所在进程的地址空间和其它资源(自己的栈和栈指针，程序计数器等寄存器)。
- 一个进程中可以并发多个线程，每条线程并行执行不同的任务
- 线程上下文切换比进程上下文切换要快得多

## 多线程的多种创建方式

### 1.继承Thread类 

- 自定义线程类继承 Thread类

- 重写 run() 方法 编写线程执行体
-  创建线程对象 调用 start() 方法启动线程

```java
public class Demo extends Thread {
    @Override
    public void run() {
        for (int i = 0; i < 20; i++) {
            System.out.println("111111111111111");
        }}
    public static void main(String[] args) {
        for (int i = 0; i < 100; i++) {
            Demo demo = new Demo();
            demo.start();  //一般都是调用start方法
            System.out.println("22222222222222222");
     }}}
```

### 2.实现Runnable接口 

- 定义MyRunnable类实现 Runnable 接口
- 实现 run() 方法,编写线程执行体
- 创建线程对象，调用 start() 方法启动线程

```java
//推荐使用 避免单继承的局限性，灵活方便，方便同一个对象被多个线程使用
public class MyRunnable implements Runnable {
    @Override
    public void run() {
        for (int i = 0; i < 20; i++) {
            System.out.println("111111111111111");
        }}
    public static void main(String[] args) {
        for (int i = 0; i < 100; i++) {
            MyRunnable myRunnable = new MyRunnable();
            new Thread(myRunnable).start();
            System.out.println("22222222222222222");
        }}}
```

```java
//龟兔赛跑实例
public class Race implements Runnable {
    private static String winner;
    @Override
    public void run() {
        for (int i = 0; i <= 100; i++) {
            if (Thread.currentThread().getName().equals("兔子")) {
                try {
                    Thread.sleep(10);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
            boolean gameOver = gameOver(i);
            if (gameOver) {
                break;
            }            System.out.println(Thread.currentThread().getName() + "--->跑了" + i);
        }}
    private boolean gameOver(int i) {
        if (winner != null) {
            return true;
        } else {
            if (i >= 100) {
                winner = Thread.currentThread().getName();
                System.out.println(winner + "赢得了比赛");
                return true;
            }
        }
        return false;
    }
    public static void main(String[] args) {
        Race race = new Race();
        new Thread(race, "兔子").start();
        new Thread(race, "乌龟").start();
    }}
```

### 3.实现Callable接口

- 实现Callable接口，需要返回值类型
- 重写call方法，需要抛出异常
- 创建目标对象
- 创建执行服务：`ExecutorService executorService=Executors.newFixedThreadPool();`
- 提交执行：`Future submit = executorService.submit(t1);`
- 获取结果：`boolean r1 = result.get()`
- 关闭服务: `ser.shutdownNow();`

```java
//实例Callable接口了解即可
public class MTImplementsCallable implements Callable {
    @Override
    public Object call() throws Exception {
        //执行线程业务的方法
        for (int i = 0; i < 10; i++) {
            //返回正在执行的线程实例
            Thread thread = Thread.currentThread();
            //getName（）获取当前线程实例的名称
            System.out.println(thread.getName()+"执行打印"+i);
        }
        //获取随机数
        UUID uuid = UUID.randomUUID();
        System.out.println("随机数字符串为："+uuid);
        System.out.println(1/0);
        return uuid;
    }}
```

### 4.使用线程池

```java
public class MTPool implements Runnable {
    @Override
    public void run() {
        //执行线程业务的方法
        for (int i = 0; i < 10; i++) {
            //返回正在执行的线程实例
            Thread thread = Thread.currentThread();
            //getName（）获取当前线程实例的名称
            System.out.println(thread.getName()+"执行打印"+i);
        }}}
//实例化线程类
MTPool mtPool =new MTPool();
//使用Executors创建固定长度为4的线程池
ExecutorService executorService = Executors.newFixedThreadPool(4);
//调用execute启动线程
executorService.execute(mtPool);
```

### 区别

runnable和callable都是执行多线程 方法名分别为run() 和call()

runnable没有返回值 无法获取线程业务方法执行方法 callable正好相反

Runnable方法没有抛出异常 而Callable有异常处理，并且获取异常

继承thread存在局限性 因为一个类只能继承一个父类 故不能用一个实例建立多个线程 只能共享Thread类的static变量

而一个类可以实现多个接口 例如runnable接口使用同一实例创建的多线程变量也是共享的 故实现接口更适合与资源共享

```java
public class SellTicketExtendsThread extends Thread {
    //定义总票数
    private int ticketNum = 20;
    //卖票人姓名
    private String  name;
    /**
     * 构造方法
     * @param name
     */
public SellTicketExtendsThread(String name) {
        this.name = name;
    }
    @Override
public void run() {
         while(ticketNum>0){
             System.out.println(name+"正在卖票，剩余"+(--ticketNum)+"张");
         }}}
public class SellTicketImplementsRunnable  implements Runnable{
    //定义总票数
    private int ticketNum = 20;
    @Override
    public void run() {
        while(ticketNum>0){
            System.out.println(Thread.currentThread().getName()+"正在卖票，剩余"+(--ticketNum)+"张");
        }}}
class Test {
    public static void main(String[] args) {
      /*  SellTicketExtendsThread sellTicketExtendsThread =new SellTicketExtendsThread("马云");
        sellTicketExtendsThread.start();
       *//* sellTicketExtendsThread.start();
        sellTicketExtendsThread.start();*//*
        SellTicketExtendsThread sellTicketExtendsThread1 =new SellTicketExtendsThread("马化腾");
        sellTicketExtendsThread1.start();
        SellTicketExtendsThread sellTicketExtendsThread2 =new SellTicketExtendsThread("刘强东");
        sellTicketExtendsThread2.start();*/
        SellTicketImplementsRunnable sellTicketImplementsRunnable =new SellTicketImplementsRunnable();
        new Thread(sellTicketImplementsRunnable,"马云").start();
        new Thread(sellTicketImplementsRunnable,"马化腾").start();
        new Thread(sellTicketImplementsRunnable,"刘强东").start();
    }}
```

```java 
//多线程匿名(Anonymous)内部类用法
public class Test8_7 {
        public static void main(String[] args) {
            //继承Thread启动线程
            new Thread(){
                @Override
                public void run() {
                    for (int i = 0; i < 10; i++) {
                        //返回正在执行的线程实例
                        Thread thread = Thread.currentThread();
                        //getName（）获取当前线程实例的名称
                        System.out.println(thread.getName()+"执行打印"+i);
                    }}}.start();
            System.out.println("-------------------------------------");
            //实现Runnable
            new Thread(new Runnable() {
                @Override
                public void run() {
                    for (int i = 0; i < 10; i++) {
                        //返回正在执行的线程实例
                        Thread thread = Thread.currentThread();
                        //getName（）获取当前线程实例的名称
                        System.out.println(thread.getName()+"执行打印"+i);
                    }}}).start();
            System.out.println("-------------------------------------");
            //实现Callable
            new Thread(new FutureTask<String>(
                    new Callable<String>() {
                        @Override
                        public String call() throws Exception {
                            for (int i = 0; i < 10; i++) {
                                //返回正在执行的线程实例
                                Thread thread = Thread.currentThread();
                                //getName（）获取当前线程实例的名称
                                System.out.println(thread.getName()+"执行打印"+i);}
                            return null;
                        }})).start();}}
```

## 多线程有哪些方法？

- start()：启动当前线程并调用线程的run()方法
- run() ：线程执行业务的方法
- currentThread():静态方法 返回当前代码执行的线程象的引用
- getName():获取当前线程的名字
- setName():设置当前线程的名字
- getPriority()：获取线程优先级 默认是5如果不手动指定 那么线程优先级具有继承性
- setpriority()：设置线程优先级 cpu会尽量执行优先级高的线程

继承性：相互启动的两个线程具有同样优先级

`MAX_PRIORITY:10`
`MIN_PRIORITY:1`
`NORM_PRIORITY:5`

- interrupt()： 通知线程中断 具体是否中断情况由被通知的线程自己处理

1.如果此时线程被阻塞状态(sleep wait join等) 立刻退出被阻塞状态并且抛出InterruptedException异常

2.如果线程处于正常活动状态 那么线程中断标志设置为ture 仅此而已 被设置中断标志线程继续正常运行 不受影响

即 ：interrupt()并不能真正中断线程 需要被通知的线程同意配合才行

- join() 等待其他线程终止 

在当前线程调用其他线程的join方法时 当前线程进入阻塞状态 直到其他线程运行结束 当前线程才由阻塞状态转换为就绪状态

- yieId() 暂停当前正执行线程 把执行机会给相同或者优先级级别更高的线程
- sleep() 使线程转入到阻塞状态

millis参数设置睡眠时间 默认以毫秒为单位 当睡眠结束线程自动进入Runnable可运行状态

- ~~stop() 强制停止线程 被废弃方法已过时~~
- isAlive():判断当前线程是否还存活

## 锁

### 同步锁

多个取款机 对应**多个锁**里面的现金互不影响 在多个取款机同时取钱也没有影响 每个来取钱的人对应的都是**线程 **在大厅等待取钱对应**线程状态**  轮到取钱者进入取款机锁上门对应**线程获得锁** 完成对应业务取钱后出门对应**线程释放** 下一个取钱者继续竞争锁 银行工作人员对应一个线程发现取款机里面现金不足通知上级 就会对取款机加钱**调用notifyAll方法<唤醒waitSet中所有的线程>** 取钱服务暂停 取钱大厅所有(**调用wait方法**)线程进入堵塞状态

而需要银行工作人员对取款机完成加钱操作也就是需要**工作人员线程获取到取款机锁**后加钱操作完成后通知大厅所以人来取钱对应的也就是上述的**调用notifyAll方法** 

如果取款机里面的人是取款人对应当前获取到锁的不是工作人员线程 因为取款机没钱了则需要释放锁 进入大厅堵塞状态(**调用wait方法**)

大堂里等待的人都来竞争锁，谁获取到谁进入继续取钱

### ReentrantLock

 ReentrantLock是可重入锁： 一个线程获取到对象的锁后，执行方法内部在需要获取锁的时候是可以获取到的。synchronized 也是可重入锁。

优点：

1. 支持获取锁的超时时间
2. 获取锁时可被打断
3. 可设为公平锁
4. 可以有不同的条件变量，即有多个waitSet，可以指定唤醒

### 死锁

是指多个进程在运行过程中因争夺资源而造成的一种僵局，当进程处于这种僵持状态时，若无外力作用，它们都将无法再向前推进。

例如老王 小李两个进程在运行到某一时刻时 都想获取酒和故事两种资源而两人分别持有酒和故事中一个资源 都想要对方手里的

```java
//example
static Beer beer = new Beer();
static Story story = new Story();
public static void main(String[] args) {
    new Thread(() ->{
        synchronized (beer){
            log.info("我有酒，给我故事");
            try {
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            synchronized (story){
                log.info("小王开始喝酒讲故事");
            }
        }
    },"小王").start();
    new Thread(() ->{
        synchronized (story){
            log.info("我有故事，给我酒");
            try {
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            synchronized (beer){
                log.info("老王开始喝酒讲故事");
            }
        }
    },"老王").start();
}
class Beer {
}
class Story{
}
```

如何避免死锁：

1. 避免一个线程同时获取多个锁
2. 避免一个线程在锁内同时占用多个资源，尽量保证每个锁只占用一个资源
3. 尝试使用超时解锁，从而规避无限期等待

### 内存模型<JMM>

1. 原子性 保证指令不会受到上下文切换的影响

   同步锁的synchronized代码块就是保证了原子性，就是**一段代码是一个整体**，原子性保证了线程安全，不会受到上下文切换的影响。

2. 可见性 保证指令不会受到cpu缓存的影响

   ```java
   static boolean run = true;
   public static void main(String[] args) throws InterruptedException {
       Thread t = new Thread(() -> {
           while (run) {
               // ....
           }});
       t.start();
       Thread.sleep(1000);
      // 线程t不会如预想的停下来
       run = false; }
   //线程有自己的工作缓存，当主线程修改了变量并同步到主内存时，t线程没有读取到，所以程序停不下来
   ```

   ![线程有自己的工作缓存，当主线程修改了变量并同步到主内存时，t线程没有读取到，所以程序停不下来](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9wMS1qdWVqaW4uYnl0ZWltZy5jb20vdG9zLWNuLWktazN1MWZicGZjcC9kODg4MDA0ZTBjMmM0N2JhYjExYjhhNjdiZjc4Zjg4ZH50cGx2LWszdTFmYnBmY3Atem9vbS0xLmltYWdl?x-oss-process=image/format,png)

3. 有序性 保证指令不会受并行优化的影响

   JVM在不影响程序正确性的情况下可能会调整语句的执行顺序，该情况也称为 **指令重排序** 。

### **Volatile**

volatile关键字解决了可见性和有序性，不能解决原子性，volatile通过**内存屏障<读/写屏障>**来实现的。

应用场景：一个线程读取变量，另外的线程操作变量，加了该关键字后保证写变量后，读变量的线程可以及时感知。

### **CAS**<compare and swap>

**轻量级 乐观锁的一种实现方式**

线程读数据时不加锁，在写回数据前，比较原值是否修改，未被其他线程修改则写回，若已被修改，则重新执行读取流程。

这是一种**乐观**策略，认为**并发操作**并不总会发生。

比较并写回的操作是通过操作系统原语实现的，保证执行过程中不会被中断，即不使用同步锁也可以保证操作的原子性。

```java
private AtomicInteger balance;
// 模拟cas的具体操作
@Override
public void withdraw(Integer amount) {
    while (true) {
        // 获取当前值
        int pre = balance.get();
        // 进行操作后得到新值
        int next = pre - amount;
        // 比较并设置成功 则中断 否则自旋重试
        if (balance.compareAndSet(pre, next)) {
            break;
        }}}
```

无锁的效率是要高于之前的锁的，由于无锁不会涉及线程的上下文切换

**cas是乐观锁的思想        sychronized是悲观锁的思想**

### 悲观锁与乐观锁？

悲观锁：在对数据进行修改前，先对数据进行加锁。之所以叫悲观锁，就是因为悲观的认为数据被并发修改的概率大，所需需要先加锁再操作

乐观锁：相对于悲观锁而言，乐观锁乐观的认为被修改数据不会发生并发修改问题，**所以乐观锁不会使用锁机制去主动的对数据进行上锁**，而是在数据修改之后，才正式对数据是否冲突进行校验（使用版本号的方式），如果发现了冲突，则提示错误，由用户决定下一步操作（撤销修改或者覆盖等）

### CAS 导致 的 **<u>ABA 问题</u>**

线程O1读取值之后 发生两次写入 由其他线程修改两次后 值没有发生变化 无法判断是否修改 这种操作不一定会影响结果 但是还是需要**增加额外的标志位或者时间戳**的方法来解决这类问题 <u>JUC并发工具包</u>中提供了这样的类 

1. AtomicInteger/AtomicBoolean/AtomicLong
2. AtomicIntegerArray/AtomicLongArray/AtomicReferenceArray
3. AtomicReference/AtomicStampedReference/AtomicMarkableReference

---

## 线程池

**一种管理线程的工具**

### 作用

1. 降低资源消耗，通过池化思想，减少创建线程和销毁线程的消耗，控制资源
2. 提高响应速度，任务到达时，无需创建线程即可运行
3. 提供更多更强大的功能，可扩展性高

```java
//线程池的构造方法
public ThreadPoolExecutor(int corePoolSize,
                          int maximumPoolSize,
                          long keepAliveTime,
                          TimeUnit unit,
                          BlockingQueue<Runnable> workQueue,
                          ThreadFactory threadFactory,
                          RejectedExecutionHandler handler) {}
```

![关系图](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9wOS1qdWVqaW4uYnl0ZWltZy5jb20vdG9zLWNuLWktazN1MWZicGZjcC85ZGFhMDM2NmY4Y2E0YmU4YWY3NWY3MDg2MTliNmQ2Y350cGx2LWszdTFmYnBmY3Atem9vbS0xLmltYWdl?x-oss-process=image/format,png)

| 参数名          | 参数意义                       |
| --------------- | ------------------------------ |
| corePoolSize    | 核心线程数                     |
| maximumPoolSize | 最大线程数                     |
| keepAliveTime   | 救急线程的空闲时间             |
| unit            | 救急线程的空闲时间单位         |
| workQueue       | 阻塞队列                       |
| threadFactory   | 创建线程的工厂，主要定义线程名 |
| handler         | 拒绝策略                       |

### **线程池案例**

1. 客户到银行时，开启柜台进行办理，柜台相当于线程，客户相当于任务，有两个是常开的柜台，三个是临时柜台。2就是核心线程数，5是最大线程数。即有两个核心线程
2. 当柜台开到第二个后，都还在处理业务。客户再来就到排队大厅排队。排队大厅只有三个座位。
3. 排队大厅坐满时，再来客户就继续开柜台处理，目前最大有三个临时柜台，也就是三个救急线程
4. 此时再来客户，就无法正常为其 提供业务，采用拒绝策略来处理它们
5. 当柜台处理完业务，就会从排队大厅取任务，当柜台隔一段空闲时间都取不到任务时，如果当前线程数大于核心线程数时，就会回收线程。即撤销该柜台。

![银行办理业务](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9wMy1qdWVqaW4uYnl0ZWltZy5jb20vdG9zLWNuLWktazN1MWZicGZjcC82YjUxNjM1OGIwNzk0ZTc0ODIyOTQyYjJlMjUyMWIzOH50cGx2LWszdTFmYnBmY3Atem9vbS0xLmltYWdl?x-oss-process=image/format,png)

### 线程池的主要流程

线程池创建、接收任务、执行任务、回收线程的步骤

1. 创建线程池后，线程池的状态是Running，该状态下才能有下面的步骤
2. 提交任务时，线程池会创建线程去处理任务
3. 当线程池的工作线程数达到corePoolSize时，继续提交任务会进入阻塞队列
4. 当阻塞队列装满时，继续提交任务，会创建救急线程来处理
5. 当线程池中的工作线程数达到maximumPoolSize时，会执行拒绝策略
6. 当线程取任务的时间达到keepAliveTime还没有取到任务，工作线程数大于corePoolSize时，会回收该线程

 注意： 不是刚创建的线程是核心线程，后面创建的线程是非核心线程，线程是没有核心非核心的概念的，这是我长期以来的误解。

拒绝策略：

1. 调用者抛出RejectedExecutionException (默认策略)
2. 让调用者运行任务
3. 丢弃此次任务
4. 丢弃阻塞队列中最早的任务，加入该任务

### 线程池的关闭

- shutdown()

会让线程池状态为shutdown，不能接收任务，但是会将工作线程和阻塞队列里的任务执行完 相当于优雅关闭。

```java
public void shutdown() {
    final ReentrantLock mainLock = this.mainLock;
    mainLock.lock();
    try {
        checkShutdownAccess();
        advanceRunState(SHUTDOWN);
        interruptIdleWorkers();
        onShutdown(); // hook for ScheduledThreadPoolExecutor
    } finally {
        mainLock.unlock();
    }
    tryTerminate();
}
```

- shutdownNow()

会让线程池状态为stop， 不能接收任务，会立即中断执行中的工作线程，并且不会执行阻塞队列里的任务， 会返回阻塞队列的任务列表

```java
public List<Runnable> shutdownNow() {
    List<Runnable> tasks;
    final ReentrantLock mainLock = this.mainLock;
    mainLock.lock();
    try {
        checkShutdownAccess();
        advanceRunState(STOP);
        interruptWorkers();
        tasks = drainQueue();
    } finally {
        mainLock.unlock();
    }
    tryTerminate();
    return tasks;
}
```

---

---

# Redis <redis io>

**开源**的、使用**C语言编写**的、支持**网络交互**的、可基于**内存也可持久化的Key-Value数据库**。

redi是一种高级的**key  :  value**存储数据结构 

其中**value支持以下五种数据**：

1.字符串（Strings）
2.字符串列表（Lists）
3.字符串集合（Sets）
4.有序字符串集合（Sorted Sets）
5.哈希（Hashes）

**key的规范使用**：

1.key不能太长 key也不要太短 尽量不要超过1024字节 太长：消耗内存 降低查找效率 太短： key可读性降低

2.key最好使用统一的命名模式，例如user:10000:passwd

**Strings** ：能存储字符串 并且有持久化操作功能 而遇到数值操作指令时 redis会将字符串类型转换成数值并且计算这个特性来实现业务上计数便利。

```yaml
set mystr "hello world!" //设置字符串类型
get mystr //读取字符串类型
set mynum "2"
OK
get mynum 
"2"
incr mynum 
(integer) 3
get mynum 
"3"
```

**Lists**：底层实现上并不是数组，而是**双端链表**









# REST_ful 风格

---

## REST <Resource Representational State Transfer> 

**对资源的访问状态通过url路径的体现出来 一种交互形式或者说模式风格**

**Resource** ：资源 REST架构核心 整个网络处理核心

**Representational** ：资源表达形式 例如 JSON  XML  JPRG

**State Transfer** ：状态变化 通过HTTP Methods实现

**通俗来讲：就是通过URL就知道要什么资源 通过HTTP Methods就知道要干什么实现什么 通过HTTP State Code就知道结果如何**

```yaml
example: 
GET/tasks			// 获取所有任务
POST/tasks 			// 创建新任务
GET/tasks/{id} 		// 通过任务id获取任务
PUT/tasks/{id}		// 通过任务id更新任务
DELETE/tasks/{id} 	// 通过任务id删除任务
- GET       //一次获取资源
- POST      //一次添加资源
- PUT       //一次修改资源
- DELETE  	//一次删除资源
#常见的HTTP State Code 
1xx：指示信息--表示请求已接收，继续处理
2xx：成功--表示请求已被成功接收
3xx：重定向--要完成请求必须进行更进一步的操作
4xx：客户端错误--请求有语法错误或请求无法实现
5xx：服务器端错误--服务器未能实现合法的请求
```

REST_ful 优点：

- 风格统一 易读
- 面向资源 具有解释性
- 充分利用HTTP协议语义





# Web传输核心协议

## HTTP 



## HTTPS















- 

# 算法


