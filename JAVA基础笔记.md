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
