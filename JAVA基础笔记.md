# 【一】Java基础语法数据类型
### 一、数据类型所占字节
		byte 一字节；
		short 、char 两字节；
		int 、float  四字节； float类型结尾加上f
		double、long 八字节；long类型结尾加上L；
### 二、var关键字
```java
StringBuilder sb = new StringBuilder()；
//以上语句可以使用var关键字进行定义
var sb = new StringBuilder();
//编译器自动根据赋值语句退出sb的变量类型为StringBuilder
```
### 三、移位运算
以下为>>或<<移位符，<<右移符最高位符号位不改变
```java
int n = 7; // 00000000 00000000 00000000 00000111 = 7`
int a = n << 1; // 00000000 00000000 00000000 00001110 = 14`
int b = n << 2; // 00000000 00000000 00000000 00011100 = 28`
int c = n << 28; // 01110000 00000000 00000000 00000000 = 1879048192`
int d = n << 29; // 11100000 00000000 00000000 00000000 = -536870912`
int n = 7; // 00000000 00000000 00000000 00000111 = 7`
int a = n >> 1; // 00000000 00000000 00000000 00000011 = 3`
int b = n >> 2; // 00000000 00000000 00000000 00000001 = 1`
int c = n >> 3; // 00000000 00000000 00000000 00000000 = 0`
```
还有一种不带符号的右移运算，使用`>>>`，它的特点是符号位跟着动，因此，对一个负数进行`>>>`右移，它会变成正数，原因是最高位的`1`变成了`0`
```java
int n = -536870912;`
int a = n >>> 1; // 01110000 00000000 00000000 00000000 = 1879048192`
int b = n >>> 2; // 00111000 00000000 00000000 00000000 = 939524096`
int c = n >>> 29; // 00000000 00000000 00000000 00000111 = 7`
int d = n >>> 31; // 00000000 00000000 00000000 00000001 = 1`
```
### 四、多行字符串
```java
String s = """  
            select * from            users   
            where id > 100  
            order by name desc        """;
```
输出如下：
```
    select * from
    users
    where id > 100
    order by name desc
```

将int型值视为Unicode编码，进行拼接成字符串
```java
int b =  72;  
int c = 105;  
int d = 65281;  
String e = ""+(char)b+(char)c+(char)d;  
System.out.println(e);//结果为Hi!
```
### 五、数组定义
```java
int[] ns = new int[5];
int[] ns = new int[]{68，31,23，15};
int[] ns = {13,23,251,315};
```
### 六、逻辑判断
##### （一）Switch语句

```java
//Switch 在Java12版本后的简洁表达式语法，保证了只有一条路劲会被执行，可不使用break语句
String fruit = "apple";  
switch (fruit){  
    case "apple" -> System.out.println("Select apple");  
    case "banana" -> System.out.println("Select banana");  
    case "mango" -> {  
        System.out.println("select mango");  
        System.out.println("Good choice!");  
    }  
    default -> System.out.println("No fruit selected");


//Switch返回值old  
int opt;  
switch (fruit){  
    case "apple":  
        opt = 1;  
        break;  
    case "pear":  
    case "mango":  
        opt = 2;  
        break;  
    default:  
        opt  = 0;  
        break;  
}  
  
//Switch新用法可以不使用break，并且可以直接返回值  
String fruit1 = "apple";  
int opt1 = switch (fruit1){  
    case "apple" -> 1;  
    case "pear","mango"->2;  
    default -> 0;  
}; //此处赋值语句需要以；结束  
System.out.println("opt1 = " + opt1);

//Switch中yield的使用大多数时候，在`switch`表达式内部，我们会返回简单的值。但是，如果需要复杂的语句，我们也可以写很多语句，放到`{…}`里，然后，用`yield`返回一个值作为`switch`语句的返回值：

int opt2 = switch (fruit1){  
    case "apple" -> 1;  
    case "pear","mango" ->2;  
    default -> {  
        int code = fruit.hashCode();  
        yield code;//yield 表示Switch语句返回值  
    }  
};  
System.out.println("opt2 = " + opt2);
```
##### （二）for each语句
```java
//for……each  
int[] ns = {1,4,9,16,25};  
int sumNum = 0;  
for(int x:ns){  
    sumNum += x;  
}  
System.out.println(sumNum);
```
#### （三）break与continue语句
break语句跳出他当前本身在的循环
```java
for(int i = 1;i<=10;i++){  
    System.out.println("i = " + i);  
    for(int j = 1; j<=10; j++){  
        System.out.println("j = " + j);  
        if (j >= i){  
            break;  
        }  
    }  
    //break 跳出他自己的当前循环，到这里  
    System.out.println("breaked");  
}
```
continue语句只是结束本次循环，并开始下一次循环
```java
//continue循环 ,实现求1-10之间奇数和  
int sum = 0;  
for(int i = 1; i<=10;i++){  
    System.out.println("begin i = " + i);  
    if( i % 2 == 0){  
        continue;  
    }  
    sum = sum + i;  
    System.out.println("end i = " +i);  
}  
System.out.println(sum);
```
### 七、数组
#### 数组排序：对数组排序实际上修改了数组本身
```java
//数组降序排序  [冒泡排序]
int[] ns = {28,12,89,73,65,18,96,50,8,36};  
System.out.println("排序前："+ Arrays.toString(ns));  
for(int i = 0 ; i < ns.length - 1; i++){  
    for (int j = 1; j < ns.length-i;j++){  
        if(ns[j-1]<ns[j]){  
            int temp = ns[j];  
            ns[j] = ns[j-1];  
            ns[j-1] = temp;  
        }  
    }  
}  
System.out.println("排序后："+Arrays.toString(ns));
```

```java
//定义二维数组  
int[][] arr = {{1,2,3,4},{5,6},{7,8,9}};  
  
//打印二维数组  使用两个for each语句
for (int[] ar:arr) {  
    for(int n: ar){  
        System.out.print(n);  
        System.out.print(',');  
    }  
    System.out.println();  
}

//使用Java标准库中的Arrays.deepToString()语句进行打印
System.out.println(Arrays.deepToString(arr));
```

```java
//用二维数组表示的学生成绩如下  
int[][] scores = {  
        {82,90,91},  
        {68,72,64},  
        {95,91,89},  
        {67,52,60},  
        {79,81,85},  
};  
//计算学生的全部平均成绩  
int sum = 0;  
int count = 0;  
for (int[] ns:scores) {  
    for(int n : ns){  
        sum += n;  
        count++;  
    }  
}  
  
double average = sum/count;  
System.out.println(average);
```
# 【二】Java面向对象编程
### 一、面向对象基础
Java是一种面向对象的编程语言。面向对象编程【object-oriented programming】；与之不同的是面向过程编程。
**面向对象编程，是一种通过对象的方式，把现实世界映射到计算机模型的一种编程方法。**
**（一）、class和instance**
class：是一种对象模版，它定义了如何创建实例，因此，class本身就是一种数据类型；
instance是对象实例，instance是根据class创建的实例，可以创建多个instance，每个instance类型相同，但各自属性可能不相同；
##### 定义class

在Java中，创建一个类，例如，给这个类命名为`Person`，就是定义一个class：
```java
class Person {
	public String name;
	public int age;
}

```
##### 创建实例
定义了class，只是定义了对象模版，而要根据对象模版创建出真正的对象实例，必须用new操作符。
new操作符可以创建一个实例，然后，我们需要定义一个引用类型的变量来指向这个实例：
```java
Person ming = new Person();
```

上述代码创建了一个Person类型的实例，并通过变量`ming`指向它。

注意区分`Person ming`是定义`Person`类型的变量`ming`，而`new Person()`是创建`Person`实例
```java
public class test2_oop {  
    public static void main(String[] args) { 
	    //实例化对象 
        City bj = new City();
        //为对象赋值  
        bj.name = "Beijing";  
        bj.latitude = 39.903;  
        bj.longitude = 116.401;  
        System.out.println(bj.name);  
        System.out.println("location: "+bj.latitude+","+bj.longitude);  
    }  
}  
//创建一个城市类
class City{  
    public String name;  
    public double latitude;  //纬度  
    public double longitude;   //经度  
}
```

以上`City`类中赋予的权限为public，在真正的开发中，容易引起逻辑混乱，因此在定义类中对于此类属性，多使用private进行封装，提供相应的方法实现间接修改，对类进行规范。

```java
public class test2_oop {  
    public static void main(String[] args) {  
        City bj = new City();  
        bj.setName("Beijing");   
        bj.setLatitude(39.903);  
        bj.setLongitude(116.401);  
        System.out.println(bj.getName());  
        System.out.println("location: "+bj.getLatitude()+","+bj.getLongitude());  
    }  
}  
  
class City{  
    private String name;  
    private double latitude;  //纬度  
    private double longitude;   //经度  
  
    public String getName(){  
        return this.name;  
    }  
    public void setName(String name){  
        this.name = name;  
    }  
  
    public double getLatitude(){  
        return this.latitude;  
    }  
    public void setLatitude(double latitude){  
        this.latitude = latitude;  
    }  
  
    public double getLongitude(){  
        return  this.longitude;  
    }  
    public void setLongitude(double longitude){  
        this.longitude = longitude;  
    }  
  
}
```
如以上：虽然外部代码不能直接修改`private`字段，但是，外部代码可以调用方法`setName()`和`setLatitude()`来间接修改`private`字段。在方法内部，我们就有机会检查参数对不对。比如，`setAge()`就会检查传入的参数，参数超出了范围，直接报错。这样，外部代码就没有任何机会把`age`设置成不合理的值。
##### 一、封装
##### 方法参数中的可变参数
```  java
//可变参数用类型...定义，可变参数相当于数组类型
class group{  
    private String[] name;  
    public void setName(String...names){  
        this.name = names;  
    }  
}


//创建实例对象，并对其进行传参，可传n个变量
Group g = new Group();  
g.setName("xiao hu");  
g.setName("xiao ming");  
g.setName("xiao lian","xiao zhang");


//可将以上可变参数定义为数组String[]类型
class group{  
    private String[] name;  
    public void setName(String[] names){  
        this.name = names;  
    }  
}
//对于以上定义用户在使用时需自己构造String[],进行传参，如下：
Group g = new Group();  
g.setName(new String[]{"xiao ming","xiao hong","xiao jun"});

以上两种方式的区别主要是：
	可变参数可以保证无法传入null，当传入0个参数时，会接收到一个空数组

```
##### 参数绑定
基本类型参数的传递，是调用方值的复制。双方各自的后续修改，互不影响
```java
public class test2_oop {  
    public static void main(String[] args) {  
        Person p = new Person();  
		int n = 15;  
		p.setAge(n);  
		System.out.println(p.getAge());  
		//此处修改了变量的值，但变量修改前传递的值已与参数位置进行了绑定，因此不影响对象的值  
		n = 20;  
		System.out.println(p.getAge());
    }  
}  


class Person{  
    private int age;  
    public int getAge(){  
        return this.age;  
    }  
    public void setAge(int age){  
        this.age = age;  
    }  
}
```

引用类型参数的传递，调用方的变量，和接收方的参数变量，指向的是同一个对象。双方任意一方对这个对象的修改，都会影响对方（因为指向同一个对象嘛）。

```java
//例1
public class test2_oop {  
    public static void main(String[] args) {  
	    Person p = new Person();  
		String[] fullname = new String[]{"Homer","Simpson"};  
		p.setName(fullname);  
		System.out.println(p.getName()); //输出为Homer Simpson  
		fullname[0] = "Bart";   //修改引用指向地址的值  
		System.out.println(p.getName());  //输出为Bart Simpson
    }  
}  


class Person{  
	private String[] name;  
	
	public String getName(){  
	    return this.name[0] + " " + this.name[1];  
	}  
	public void setName(String[] name){  
	    this.name = name;  
	}
}
```

```java
//例2
public class test2_oop {  
    public static void main(String[] args) {  
	    Person p = new Person();  
		String bob = "Bob";  
		p.setName(bob);  
		System.out.println(p.getName());  //输出值Bob  
		bob = "Alice";  //修改字符串类型指向  
		System.out.println(p.getName());  //输出依旧为Bob
    }  
}  

class Person{  
    private int age;  
    private String name;  
  
    public String getName(){  
        return this.name;  
    }  
  
    public void setName(String name){  
        this.name = name;  
    }  
}

```



注：当改变引用指向后，原对象指向的地址不会改变，其对象中指向的值也应当不变。当引用指向并未改变，引用指向中指向的值发生改变，对象与引用所共享一个值，则对象所引用的值也发生改变。故以上例1对象的值发生了改变，而例2的值并未发生改变。

##### 构造方法
```java
class Person{  
    private int age;  
    private String name;  

	//构造方法如下，以类名命名的方法，再不自己定义前，编译器自动为我们生成一个默认构造方法
    public Person(String name,int age){  
        this.name = name;  
        this.age = age;  
    }  

	//默认构造方法，编译器在对象创建时默认生成，当我们定义后编译器将不在自动生成，一个类中可包含多个构造方法，即可保存带参数的构造以及不带参数的构造等等
	/*
	public Person(){
	}
	*/
      
}
```

注：当其类在定义时，设置了默认初始化，又设置了带有参数的构造方法，当用户使用构造方法，传入值时，当前创建的对象的属性根据构造方法参入值改变。如：
```java

public class test2_oop {  
    public static void main(String[] args) {  
	    Person p = new Person("lisi",12);  
		System.out.println(p.getName());   //输出为lisi
		System.out.println(p.getAge());    //输出为12
    }  
}  



class Person{  
    private int age = 10;    //对字段直接进行初始化
    private String name = "faWaiKuangTuZhangSan";     //对字段直接进行初始化
  

    public String getName(){  
        return this.name;  
    }  
    public int getAge(){  
        return this.age;  
    }  

    public Person(String name,int age){  
        this.name = name;  
        this.age = age;  
    }  
  
}
```

在一个类中可定义多个构造方法，在通过new操作调用时，编译器会自动通过构造方法的参数数量、参数类型、参数位置进行区分。
```java
class Person{  
    private int age = 10;  
    private String name = "faWaiKuangTuZhangSan";  

  
    public String getName(){  
        return this.name;  
    }  
    public int getAge(){  
        return this.age;  
    }  
	//当需要默认构造方法时，需定义
	public Person(){
	}

	//第一个构造方法
    public Person(String name,int age){  
        this.name = name;  
        this.age = age;  
    }  
	//第二个构造方法
	public Person(String name){
		this.name = name;
	}
	
}
```

**一个构造方法可以调用其他构造方法，实现代码的复用，其语法为`this(...)`**
```java
class Person{  
    private int age = 10;  
    private String name = "faWaiKuangTuZhangSan";  

  
    public String getName(){  
        return this.name;  
    }  
    public int getAge(){  
        return this.age;  
    }  
	//当需要默认构造方法时，需定义
	public Person(){
		this("Unamed");//此处调用另一个构造方法Person(String)
	}

	//第一个构造方法
    public Person(String name,int age){  
        this.name = name;  
        this.age = age;  
    }  
	//第二个构造方法
	public Person(String name){
		this.name = name;
	}
	
}
```
##### 方法重载
在一个类中，我们可以定义多个方法。如果有一系列方法，它们的功能都是类似的，只有参数有所不同，那么，可以把这一组方法名做成*同名*方法。在一般情况下，方法的返回值类型相同。例如，在`Hello`类中，定义多个`hello()`方法：
```java
public class test2_oop {  
    public static void main(String[] args) {  
	    Hello he = new Hello();  
		he.hello();  
		he.hello("zhangsan");  
		he.hello("lisi",3);
    }  
}  


class Hello{  
    public void hello(){  
        System.out.println("Hello,world!");  
    }  
    public void hello(String name){  
        System.out.println("Hello, " + name + "!");  
    }  
    public void hello(String name,int age){  
        if(age < 18){  
            System.out.println("Hi, " + name + "!");  
        }else{  
            System.out.println("Hello, " + name + "!");  
        }  
    }  
}
```
输出如下：
![[Pasted image 20231015081535.png]]

##### 二、继承
继承的实现使得代码的重复得以简化，即在子类中不必重复写相同的代码，继承是面向对象编程中非常强大的一种机制，它首先可以复用代码。当我们让`Student`从`Person`继承时，`Student`就获得了`Person`的所有功能，我们只需要为`Student`编写新增的功能。
```java
//父类、基类、超类
class Person{  

	//注：在继承中，若需让子类成功调用父类中的字段及方法，需避免使用private关键字，private表示只能当前类调用，其子类及子类的子类不可访问，因此在继承的父类中，需将子类所需的字段及方法设置为protect或public
	//protect表示当前类及子类以及子类的子类可访问
    protected int age = 10;  
    protected String name = "faWaiKuangTuZhangSan";  

  
    public String getName(){  
        return this.name;  
    }  
  
    public void setName(String name){  
        this.name = name;  
    }  
    public int getAge(){  
        return this.age;  
    }  
    public void setAge(int age){  
        this.age = age;  
    }  
  
    //构造方法，父类的默认构造方法，当父类中没有默认构造方法时，子类需使用编译器提供的super()方法，自动调用父类的构造方法
    public Person(){  
  
    }  
  
    public Person(String name,int age){  
        this.name = name;  
        this.age = age;  
    }  
  
}

//子类、扩展类；当我们的子类中需要使用到父类相同的属性及方法时，使用继承
class Student extends Person{  
	//不需重复name和age字段及方法
	//补充子类中特需的字段及方法即可
    protected int score;  
  
    public int getScore(){  
        return score;  
    }  
    public void setScore(int score){  
        this.score = score;  
    }  
  
}
```

**super()关键字**
`super`关键字表示父类（超类）。子类引用父类的字段时，可以用`super.fieldName`。例如：
```java
class Student extends Person{
	public String hello(){
		return "Hello, " + super.name;
	}
}
```
**当创建父类构造时，必须使用super()关键字，当子类构造时，编译器默认调用父类构造super();例如：**
```java
class Student extends Person{  
    protected int score;  
  
    public int getScore(){  
        return score;  
    }  
    public void setScore(int score){  
        this.score = score;  
    }  
  
    //构造方法  
    public Student(String name,int age,int score){  
	    super();//在调用时编译器自动调用父类的构造方法，在父类构造中有默认构造方法，可省略。当父类中没有默认的构造方法时，需设置父类带参相应的构造方法  
        this.score = score;  
    }  
  
}
```
**当父类中，没有默认的构造方法时，需在子类中调用super()传入相应的参数，实现父类构造：**
```java
class Person{  
    protected int age = 10;  
    protected String name = "faWaiKuangTuZhangSan";  
  
  
    public String getName(){  
        return this.name;  
    }  
  
    public void setName(String name){  
        this.name = name;  
    }  
  
    public int getAge(){  
        return this.age;  
    }  
    public void setAge(int age){  
        this.age = age;  
    }  
  
    //带参构造方法  
    public Person(String name,int age){  
        this.name = name;  
        this.age = age;  
    }  
}

  //继承父类
class Student extends Person{  
    protected int score;  
  
    public int getScore(){  
        return score;  
    }  
    public void setScore(int score){  
        this.score = score;  
    }  
  
    //构造方法  
    public Student(String name,int age,int score){  
        super(name,age);  //父类中，只有带参的构造，因此需传入所需的参数 
        this.score = score;  
    }  
  
}
```
**向上转型：把子类类型安全地变成父类类型的赋值**
指将父类的引用类型指向子类的示例，即子类向父类转型，向上转型，例如：
```java
public class Extends {  
    public static void main(String[] args) {  
		//Person的引用p指向的其子类的实例，以下操作是可行的
        Person p = new Student("zhangsan",15,89);  
    }  
}
```
这是因为`Student`继承自`Person`，因此，它拥有`Person`的全部功能。`Person`类型的变量，如果指向`Student`类型的实例，对它进行操作，是没有问题的！
**向下转型：把一个父类类型强制转型为子类类型，可能是不安全的，例如：**
```java
public class Extends {  
    public static void main(String[] args) {  
		//向下转型，强制将父类转成子类，会发生不安全访问
        Student s = (Student) new Person("lisi",19);  
        //此处产生报错
        s.getScore();  
    }  
}
```
![[Pasted image 20231015093235.png]]

Java编译器为了防止程序员在转型中遇到以上此种问题，提供了`instanceof`操作符便于判断一个变量所指向的实例是否是指定类型，或者这个类型的子类。如果一个引用变量为`null`，那么对任何`instanceof`的判断都为`false`。
```java
Person p = new Person("zhangsan",18);  
System.out.println(p instanceof Person);//true  
System.out.println(p instanceof Student); //false  
  
Student s = new Student("lisi",18,90);  
System.out.println(s instanceof Person);//true  
System.out.println(s instanceof Student); //true  
  
Student n = null;  
System.out.println(n instanceof Student); //false
```
利用`instanceof`可在向下转型时进行判断：
```java
Person p = new Student("zhangsan",15,89);  

if(p instanceof Student){  
    Student s = (Student) p; 
}
```
##### 三、多态(Polymorphic)
在继承关系中，子类如果定义了一个与父类方法签名完全相同(方法名称、方法返回值类型、方法参数)的方法，被称为覆写（Override）。
**需要注意的是，当发生向下转型时，方法调用使用的是引用类型的方法还是实际调用的方法，在Java的实例方法中调用是基于运行时的实际类型的动态调用，而非变量的声明类型。即实际调用的方法。
```java
public class Extends {  
    public static void main(String[] args) {  
  
        Person p = new Student("zhangsan",15,89);  
  
        p.run();//发生向下转型，返回Student.run  
          
    }  
}
class Person{  
    protected int age = 10;  
    protected String name = "faWaiKuangTuZhangSan";  
    
    public Person(String name,int age){  
        this.name = name;  
        this.age = age;  
    }  
    //父类中的方法  
    public void run(){  
        System.out.println("Person.run");  
    }  
}

class Student extends Person{  
    protected int score;  
  
    //构造方法  
    public Student(String name,int age,int score){  
        super(name,age); 
        this.score = score;  
    }  
  
    @Override   //检查与父类中的方法是否构成重写  
    public void run() {  
        System.out.println("Student.run");  //重写父类中的方法  
    }  
}
```
多态的特性就是，运行期才能动态决定调用的子类方法。对某个类型调用某个方法，执行的实际方法可能是某个子类的覆写方法。
```java
  
public class Polymorphic {  
    public static void main(String[] args) {  
        Income[] incomes = new Income[]{  
                new Income(3000),  
                new Salary(7500),  
                new stateCouncilSpecialAllowance(1999999)  
        };  
        System.out.println(totalTax(incomes));  
    }  
  
    public static double totalTax(Income...incomes){  
        double total = 0;  
        for (Income income:incomes) {  
            total = total + income.getTax();  
        }  
        return total;  
    }  
  
}  
  
class Income{  
    protected double income;  
    public Income(double income){  
        this.income = income;  
    }  
    public double getTax(){  
        System.out.println("IncomeTax:" + income*0.1);  
        return income*0.1;  
    }  
}  
  
class Salary extends Income{  
  
    public Salary(double income){  
        super(income);  
    }  
  
    @Override  
    public double getTax(){  
        if(income <= 5000){  
            return 0;  
        }  
        System.out.println("SalaryTax:"+(income - 5000) * 0.2);  
        return (income - 5000) * 0.2;  
    }  
  
}  
  
class stateCouncilSpecialAllowance extends Income{  
    public stateCouncilSpecialAllowance(double income){  
        super(income);  
    }  
  
    @Override  
    public double getTax() {  
        System.out.println("0");  
        return 0;  
    }  
}
```
![[Pasted image 20231015102608.png]]

**final关键字**
继承可以允许子类覆写父类的方法。如果一个父类不允许子类对它的某个方法进行覆写，可以把该方法标记为`final`。用`final`修饰的方法不能被`Override`；
```java
class Person {
	protected String name;
	public final String hello() {
		return "Hello, " + name;
	}
}

Student extends Person {
	// compile error: 不允许覆写`
	@Override
	public String hello() {
	}
}
```
如果一个类不希望任何其他类继承自它，那么可以把这个类本身标记为`final`。用`final`修饰的类不能被继承
```java
final class Person {
	protected String name;
}

// compile error: 不允许继承自Person`
Student extends Person {
}
```
可以在构造方法中初始化final字段：
```java
class Person {
	public final String name;
	public Person(String name) {
		this.name = name;
	}
}
```
这种方法更为常用，因为可以保证实例一旦创建，其`final`字段就不可修改。

**抽象类**
如果父类的方法本身不需要实现任何功能，仅仅是为了定义方法签名，目的是让子类去覆写它，那么，可以把父类的方法声明为抽象方法：
```java
abstract class Person{
	public abstract void run();
}
```
具有抽象方法的类，必须定义成抽象类，即在class前加上abstract，否则编译报错。抽象类无法进行实例化，只能用于子类继承，继承了抽象类的子类必须重写抽象类的抽象方法。
**接口**
在抽象类中，抽象方法本质上是定义接口规范：即规定高层类的接口，从而保证所有子类都有相同的接口实现，这样，多态就能发挥出威力。
如果一个抽象类没有字段，所有方法全部都是抽象方法：
```java
abstract class Person{
	public abstract void run();
	public abstract String getName();
}
```
可将以上类改写成接口：`interface。`可使用`interface`声明接口
```java
interface Person{
	void run();
	String getName();
}
```
所谓`interface`，就是比抽象类还要抽象的纯抽象接口，因为它连字段都不能有。因为接口定义的所有方法默认都是`public abstract`的，所以这两个修饰符不需要写出来（写不写效果都一样）。
当一个具体的`class`去实现一个`interface`时，需要使用`implements`关键字。
```java
class Student implements Person{
	private String name;
	public Student(String name){
		this.name = name;
	}

	@Override
	public void run(){
		System.out.println(this.name + " run");
	}

	@Override
	public String getName(){
		return this.name;
	}
}
```
我们知道，在Java中，一个类只能继承自另一个类，不能从多个类继承。但是，一个类可以实现多个`interface`，例如：
```java
class Student implements Person,Hello{

}
```
**default方法**
在接口中，可以定义`default`方法，实现类可以不必覆写`default`方法。`default`方法的目的是，当我们需要给接口新增一个方法时，会涉及到修改全部子类。如果新增的是`default`方法，那么子类就不必全部修改，只需要在需要覆写的地方去覆写新增方法。
`default`方法和抽象类的普通方法是有所不同的。因为`interface`没有字段，`default`方法无法访问字段，而抽象类的普通方法可以访问实例字段。

**静态字段和静态方法**
用`static`修饰的字段，称为静态字段：`static field`
实例字段在每个实例中都有自己的一个独立“空间”，但是静态字段只有一个共享“空间”，所有实例都会共享该字段。
```java
public class test2_oop {  
    public static void main(String[] args) {  
        //实现静态字段与静态方法  
        Person ming = new Person("xiao ming",12);  
        Person hong = new Person("xion hong",15);  
        ming.number = 88;  
        System.out.println(ming.number);    //不建议如此使用，建议使用类名Person进行调用 Person.number
        hong.number = 99;  
        System.out.println(ming.number);  
  
    }  
}

class Person{  
    protected int age;  
    protected String name;  
    public static int number;  //定义静态字段
  
    public Person(String name,int age){  
        this.name = name;  
        this.age = age;  
    }  
  
}
```
![[Pasted image 20231015133552.png]]
结果如上：因为静态字段共享一片空间，因此修改后都会产生变化，建议使用类对静态字段进行调用，对象虽可访问静态字段，但静态字段属于类，并非属于实例对象。在实际调用中，编译器会自动转换为`类名.静态字段`。
静态方法与静态字段类似，也使用`static`修饰。需要注意的是，调用实例方法必须通过一个实例对象，而调用静态方法则不需要实例对象，可使用类名直接调用。
```java
public class test2_oop {  
    public static void main(String[] args) {  
		//使用类直接调用静态方法  
		Person.setNumber(99);  
		System.out.println(Person.number);
    }  
}

class Person{  
    protected int age;  
    protected String name;  
    public static int number;  //定义静态字段
	//定义静态方法  
	public static void setNumber(int value){  
	    number = value;  
	}

    public Person(String name,int age){  
        this.name = name;  
        this.age = age;  
    }  
  
}
```
因为静态方法属于`class`而不属于实例，因此，静态方法内部，无法访问`this`变量，也无法访问实例字段，它只能访问静态字段。
通过实例变量也可以调用静态方法，但这只是编译器自动帮我们把实例改写成类名而已。
通常情况下，通过实例变量访问静态字段和静态方法，会得到一个编译警告。![[Pasted image 20231015134519.png]]

**包**
要特别注意：包没有父子关系。java.util和java.util.zip是不同的包，两者没有任何继承关系。
位于同一个包的类，可以访问包作用域的字段和方法。不用`public`、`protected`、`private`修饰的字段和方法就是包作用域。
*import*：导入其他包中的类
(一)、写类所在包的完整名称
```java
public class Person{
	public void run(){
		mr.jun.Arrays array = new mr.jun.Arrays();
	}
}
```
(二)、使用import语句导入包
```java
package ming;  //当前类所在包
import mr.jun.Arrays;  //导入所需使用的包
//import mr.jun.*; //此处可以用*省略代表导入所有的class

public class Person{
	public void run(){
		Arrays array = new Arrays();
	}
}
```
(三)、使用`import static`的语法，可以导入一个类的静态字段和静态方法
```java
package ming;  //当前类所在包
import static java.lang.System.*;  //导入System类的所有静态字段和静态方法

public class Main{
	public static void main(String[] args){
		//相当于调用System.out.println(...)
		out.println("Hello,world!");
	}
}
```

注：
编写class的时候，编译器会自动帮我们做两个import动作：
- 默认自动`import`当前`package`的其他`class`；
如果有两个`class`名称相同，例如，`mr.jun.Arrays`和`java.util.Arrays`，那么只能`import`其中一个，另一个必须写完整类名。

**作用域**
`public`、`protected`、`private`用于限制访问作用域。
- public：定义为`public`的`class`、`interface`等可以被其他任何类访问
- protected：`protected`作用于继承关系。定义为`protected`的字段和方法可以被子类访问，以及子类的子类：
- private：定义为`private`的`class`、`method`等不可以被其他任何类访问，但Java支持嵌套类，如果一个类内部还定义了嵌套类，那么，嵌套类拥有访问`private`的权限；
*包的作用域*
	包作用域是指一个类允许访问同一个`package`的没有`public`、`private`修饰的`class`，以及没有`public`、`protected`、`private`修饰的字段和方法。
```java
package abc;
//package权限的类：
class Hello{
	//package权限的方法：
	void hi(){
	}
}
```
只要在同一个包，就可以访问`package`权限的`class`、`field`和`method`：
```java
package abc;  //注意，要在同一个包，则包名完全一致

class Main(){
	void foo(){
		//可以访问package权限的类：
		Hello h = new Hello();
		//可以调用package权限的方法：
		h.hi()
	}
}

```
*final修饰符*
- 用`final`修饰`class`可以阻止被继承；
- 用`final`修饰`method`可以阻止被子类覆写；
- 用`final`修饰`field`可以阻止被重新赋值；
- 用`final`修饰局部变量可以阻止被重新赋值；

**classpath和jar**
`classpath`是JVM用到的一个环境变量，它用来指示JVM如何搜索`class`。
因为Java是编译型语言，源码文件是`.java`，而编译后的`.class`文件才是真正可以被JVM执行的字节码。因此，JVM需要知道，如果要加载一个`abc.xyz.Hello`的类，应该去哪搜索对应的`Hello.class`文件。
所以，`classpath`就是一组目录的集合，它设置的搜索路径与操作系统相关。例如，在Windows系统上，用`;`分隔，带空格的目录用`""`括起来，可能长这样：
 `C:\work\project1\bin;C:\shared;"D:\My Documents\project1\bin"`
在Linux系统上，用`:`分隔，可能长这样：
 `/usr/shared:/usr/local/bin:/home/liaoxuefeng/bin`

JAR包
如果有很多`.class`文件，散落在各层目录中，肯定不便于管理。如果能把目录打一个包，变成一个文件，就方便多了。
jar包就是用来干这个事的，它可以把`package`组织的目录层级，以及各个目录下的所有文件（包括`.class`文件和其他文件）都打成一个jar文件，这样一来，无论是备份，还是发给客户，就简单多了。
jar包实际上就是一个zip格式的压缩文件，而jar包相当于目录。如果我们要执行一个jar包的`class`，就可以把jar包放到`classpath`中：
`java -cp ./hello.jar abc.xyz.Hello`
这样JVM会自动在`hello.jar`文件里去搜索某个类。
**模块**
后面回头学
### 二、Java核心类
**String的基本特性**
在Java中，`String`是一个引用类型，它本身也是一个`class`。但是，Java编译器对`String`有特殊处理，即可以直接用`"…"`来表示一个字符串：
	`String s1 = "Hello!";`
实际上字符串在`String`内部是通过一个`char[]`数组表示的，因此，按下面的写法也是可以的：
`String s2 = new String(new char[] {'H', 'e', 'l', 'l', 'o', '!'});`
因为`String`太常用了，所以Java提供了`"…"`这种字符串字面量表示方法。
Java字符串的一个重要特点就是字符串*不可变*。这种不可变性是通过内部的`private final char[]`字段，以及没有任何修改`char[]`的方法实现的。
**! 字符串在比较时，需要使用`equals()`方法，而非`==`进行比较**
**String 类型的一些基本方法**
```java
  
import java.util.Arrays;  
  
  
public class StringUse {  
    public static void main(String[] args) {  
  
        String s1 = "hello";  
        String s2 = "Hello";  
        //使用equals进行字符串比较，equalsIgnoreCase()表示忽略大小写的比较  
        System.out.println(s1.equalsIgnoreCase(s2));  //true  
  
        //contain()方法的参数是CharSequence而不是String，CharSequence是String的父类  
        System.out.println(s1.contains("he"));  //true  
  
        //indexOf(“”)返回指定的字符串所在当前字符串中的位置，下标从0开始  
        System.out.println(s1.indexOf("l"));  //2  
        System.out.println(s1.lastIndexOf("l"));  //3  
        System.out.println(s1.startsWith("he")); //true  判断是否以“”开头  
        System.out.println(s1.endsWith("lo"));  //true  判断是否以“”结尾  
  
        System.out.println("Hello".substring(2));  //"llo" 从第2个位置开始截取  
        System.out.println("Hello".substring(2,4));  //“ll"  从第2个位置截取到第4个位置  
  
        //String还提供许多自带的方法，例如：trim()、strip()去除前后端的空格  
        String s3 = "   \u3000\tHello\r\n ";  //\u3000为中文空格  
        System.out.println(s3.trim()); //“    Hello"  注：并未改变字符串的内容，而是返回一个新的字符串  
        System.out.println(s3.strip());//"Hello"  与trim()的区别在与会将类似中文字符的空格也去除  
  
        //isEmpty()和isBlank()判断字符串是否为空，是否只包含空格  
        System.out.println("".isEmpty()); // true  
        System.out.println("  ".isEmpty()); //false  
        System.out.println(" \n".isBlank());  //true  
        System.out.println("\nhello".isBlank()); //false  
  
        //替换字符replace()方法  
        String s = "hello";  
        System.out.println(s.replace('l', 'n')); //henno 所有的l都将被替换  
  
        //分割字符串  
        String s4 = "A,B,C,D";  
        String[] ss = s.split("\\,"); //{"A","B","C","D"}  
  
        //join()        String[] arr = {"A","B","C"};  
        String s5 = String.join("***",arr);  //"A***B***C"  
  
        //类型转换  
        System.out.println(String.valueOf(123)); //"123"  
        System.out.println(String.valueOf(45.6)); //"45.67"  
  
        //将字符串转换成其他类型  
        int n1 = Integer.parseInt("134");  //123  
        System.out.println("n1 = " + n1);  
        int n2 = Integer.parseInt("ff",16);  //按十六进制转换  
  
        boolean b1 = Boolean.parseBoolean("true"); //true  
        boolean b2 = Boolean.parseBoolean("false");  
  
        //要特别注意，Integer有个getInteger(String)方法，它不是将字符串转换为int，而是把该字符串对应的系统变量转换为Integer：  
        System.out.println(Integer.getInteger("java.version")); //版本号，11  
  
        //实现string和char[]类型的转换  
        char[] cs = "Hello".toCharArray();  //String -> char[]  
        String s6 = new String(cs);     //char[] -> String，复制的一份  
        System.out.println(s6);  
        cs[0] = 'X';  //  改变其值不会影响拷贝的String字符  
        System.out.println(s6);// Hello  此处不会更改，  
        System.out.println(Arrays.toString(cs));  //[X,e,l,l,o]  
    }  
}
```
**StringBuilder**
Java提供了的`StringBuilder`是用于处理字符拼接的一个方法，在Java中一般不使用`+`直接拼接，会参数大量的临时数据，造成内存的浪费。`StringBuilder`它是一个可变对象，可以预分配缓冲区，这样，往`StringBuilder`中新增字符时，不会创建新的临时对象：
```java
//StringBuilder的使用  
StringBuilder sb = new StringBuilder(1024);  
for (int i = 0; i < 1000; i++) {  
    sb.append(i);  
    sb.append(',');  
}  
String s = sb.toString();  
System.out.println(s);

//StringBuilder也可以使用链式操作，之所以可实现链式存储，其原因为StringBuilder的源码返回的为this即其自身，由此可接着调用
StringBuilder sb1 = new StringBuilder(1024);  
sb1.append("Mr ").append("Bob ").append("!").insert(0,"Hello, ");  
String ss = sb1.toString();  
System.out.println(ss);

```

**StringJoiner的使用**
```java
//使用StringJoiner方法  
String[] names = {"Bob","Alice","Grace"};  
var sj = new StringJoiner(", ","Hello ","!");  
for (String name:names) {  
    sj.add(name);  
}  
System.out.println(sj);
```

`String`还提供了一个静态方法`join()`,这个方法在内部使用了`StringJoiner`来拼接字符串，在不需要指定“开头”和“结尾”的时候，用`String.join()`更方便：
```java
String[] arr = {"bob","alice","grace"};  
String sss = String.join(",",arr);  
System.out.println(sss);
```

**包装类型**
- 基本类型：`byte`、`short`、`int`、`long`、`boolean`、`float`、`double`、`char`
- 引用类型：所有`class`和`interface`类型
注：引用类型可以赋值为`null`，表示空，但基本类型不能赋值为`null`。
对两个`Integer`实例进行比较要特别注意：绝对不能用`==`比较，因为`Integer`是引用类型，必须使用`equals()`比较。

**enum枚举**
为了让编译器能自动检查某个值在枚举的集合内，并且，不同用途的枚举需要不同的类型来标记，不能混用，我们可以使用`enum`来定义枚举类：
```java

Weekday day = Weekday.SUN;  
if(day == Weekday.SAT || day == Weekday.SUN){  
    System.out.println("Work at home!");  
}else{  
    System.out.println("Work at office!");  
}

enum Weekday{  
    SUN,MON,TUE,WED,THU,FRI,SAT;  
}
```

使用`enum`定义的枚举类是一种引用类型。前面我们讲到，引用类型比较，要使用`equals()`方法，如果使用`==`比较，它比较的是两个引用类型的变量是否是同一个对象。因此，引用类型比较，要始终使用`equals()`方法，但`enum`类型可以例外。
这是因为`enum`类型的每个常量在JVM中只有一个唯一实例，所以可以直接用`==`比较：
```java
if(day == Weekday.FRI){}  //可以
if(day.equals(Weekday.SUN)){} //也可以
```
*enum类型的特点*
通过`enum`定义的枚举类，和其他的`class`有什么区别？
答案是没有任何区别。`enum`定义的类型就是`class`，只不过它有以下几个特点：
- 定义的`enum`类型总是继承自`java.lang.Enum`，且无法被继承；
- 只能定义出`enum`的实例，而无法通过`new`操作符创建`enum`的实例；
- 定义的每个实例都是引用类型的唯一实例；
- 可以将`enum`类型用于`switch`语句。

**Random**
`Random`用来创建伪随机数。所谓伪随机数，是指只要给定一个初始的种子，产生的随机数序列是完全一样的。
```java
Random r = new Random();
r.nextInt(); // 2071575453,每次都不一样`
r.nextInt(10); // 5,生成一个[0,10)之间的int`
r.nextLong(); // 8811649292570369305,每次都不一样`
r.nextFloat(); // 0.54335...生成一个[0,1)之间的float`
r.nextDouble(); // 0.3716...生成一个[0,1)之间的double`
```