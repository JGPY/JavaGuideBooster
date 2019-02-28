# Java语言相关

### 目录

---
<a href="#1">1. 标识符的命名规则。</a> <br>
<a href="#2">2. instanceof 关键字的作用。</a> <br>
<a href="#3">3. strictfp 关键字的作用。</a> <br>
<a href="#4">4. 什么是不可变类?</a> <br>
<a href="#5">5. Java 中的基本数据类型占据几个字节?</a> <br>
<a href="#6">6. 运算符的优先级。</a> <br>
<a href="#7">7. 强制类型转换时的规则有哪些。</a> <br>
<a href="#8">8. 数组初始化时需要注意的问题。</a> <br>
<a href="#9">9. 如何在 main()方法执行前输出“Hello world”?</a> <br>
<a href="#10">10. Java 程序初始化的顺序(对象实例化的过程)。</a> <br>
<a href="#11">11. 构造函数的特点。</a> <br>
<a href="#12">12. 序列化与反序列化。</a> <br>
<a href="#13">13. Switch 能否用 string 做参数?</a> <br>
<a href="#14">14. equals 与==的区别。</a> <br>
<a href="#15">15. Hashcode 的作用。</a> <br>
<a href="#16">16. hashCode() 与 equals() 生成算法、方法怎么重写。</a> <br>
<a href="#17">17. Object 有哪些公用方法?</a> <br>
<a href="#18">18. String、StringBuffer 与 StringBuilder 的区别。</a> <br>
<a href="#19">19. try catch finally,try 里有 return,finally 还执行么?如果会的话,什么时候执行,在 return 之前还是 return 之后?</a> <br>
<a href="#20">20. 说下异常的原理。</a> <br>
<a href="#21">21. Java 面向对象的三个特征与含义。</a> <br>
<a href="#22">22. java 多态的实现原理(实现机制)。</a> <br>
<a href="#23">23. Override(覆盖、重写)和 Overload(重载)的区别。</a> <br>
<a href="#24">24. 接口与抽象类的区别。</a> <br>
<a href="#25">25. 静态内部类和非静态内部类的区别。</a> <br>
<a href="#26">26. static 的使用方式。</a> <br>
<a href="#27">27. 反射的作用与原理。如何提高反射效率?</a> <br>
<a href="#28">28. Java 和 C++/C 的区别,JAVA 的优点。</a> <br>
<a href="#29">29. 同一个.java 文件中是否可以有多个 main()方法?</a> <br>
<a href="#30">30. JAVA 中的类和成员的访问控制。</a> <br>
<a href="#31">31. System.out.println()方法使用时需要注意的问题。</a> <br>
<a href="#32">32. 继承和组合区别。</a> <br>
<a href="#33">33. final finally finalize 的区别。</a> <br>
<a href="#34">34. JDK1.7 和 1.8 的区别。</a> <br>
<a href="#35">35. List<String>能否转为List<Object>?能否List<Object>list=newArrayList<String>()?List<String>list=new ArrayList<Object>()?原因?</a> <br>
<a href="#36">36. 泛型的好处?</a> <br>

### <a name="1">1. 标识符的命名规则。</a>
&ensp;&ensp;&ensp;&ensp;
    标识符只能由数字、字母(a-z、A-Z)、下划线(_)和$组成,并且第一
个字符不能为数字。

### <a name="2">2. instanceof 关键字的作用。</a>
&ensp;&ensp;&ensp;&ensp;
    用法:对象 A instanceof 类 B。 <br>
&ensp;&ensp;&ensp;&ensp;
    instanceof 通过返回一个布尔值来指出,这个对象是否是这个特定类或者是
它的子类的一个实例。注意:如果对象 A 为 null,则返回 false。 <br>

### <a name="3">3. strictfp 关键字的作用。</a>
&ensp;&ensp;&ensp;&ensp;
    strictfp 可以用来修饰一个类、接口或者方法,在所声明的范围内,所有浮
点数的计算都是精确的。当一个类被 strictfp 修饰时,所有方法默认也被 strictfp
修饰。 <br>

### <a name="4">4. 什么是不可变类?</a>
&ensp;&ensp;&ensp;&ensp;
    不可变类:当创建了一个类的实例后,就不允许修改它的值了。特别注意:
String 和包装类(Integer,Float......)都是不可变类。String 采用了享元设计模
式(flyweight)。 <br>

**扩展问题 1**:new String("abc");创建了几个对象? <br>
&ensp;&ensp;&ensp;&ensp;
    1 个或者 2 个对象。如果常量池中原来有”abc”,那么只创建一个对象;如
果常量池中原来没有字符串”abc”,那么就会创建 2 个对象。 <br>

**扩展问题 2**: <br>


    String s = "abc";
    String ss = "ab" + "c";
    System.out.println(s == ss);
输出为:true <br>
解析: "ab" + "c"在编译时就被转换为”abc”。 <br>

**扩展问题 3**: <br>
    
    
    String s = "abc";
    char[] ch={'a','b','c'};
    System.out.println(s.equals(ch));
输出为:false <br>
解析:S 和 ch 分别为字符串类型和数组类型,所以输出为 false。 <br>

    public static void changeStringBuffer(StringBuffer ss1,
        StringBuffer ss2) {
            ss1.append(" world");
            ss2 = ss1;
        }
        ublic static void main(String[] args) {
        Integer a = 1;//包装类是不可变类
        Integer b = a;
        b++;
        System.out.println(a);
        System.out.println(b);
        StringBuffer s1 = new StringBuffer("Hello");
        StringBuffer s2 = new StringBuffer("Hello");
        changeStringBuffer(s1, s2);
        System.out.println(s1);
        System.out.println(s2);
    }
输出结果: <br>
1 <br>
2 <br>
Hello world <br>
Hello <br>

### <a name="5">5. Java 中的基本数据类型占据几个字节?</a>
在 java 中, <br>
&ensp;&ensp;&ensp;&ensp;
    **占 1 个字节**:byte,boolean <br>
&ensp;&ensp;&ensp;&ensp;
    **占 2 个字节**:char,short <br>
&ensp;&ensp;&ensp;&ensp;
    **占 4 个字节**:int,float <br>
&ensp;&ensp;&ensp;&ensp;
    **占 8 个字节**:long,double <br>
&ensp;&ensp;&ensp;&ensp;
    他们对应的封装类型是:**Integer** ,Double ,Long ,Float,
Short,Byte,**Character**,Boolean。 <br>

基本数据类型和对应的包装类的区别: <br>
&ensp;&ensp;&ensp;&ensp;
    **初始值的不同**。当基本数据类型变量和包装类的对象作为**类的实例变量**时,
默认初始值是不同的。包装类的对象默认初始值是 null,基本数据类型变量
的默认初始值根据变量类型不同而不同,如 Int 的默认初始值是 0。如下。
另外,**包装类是不可变类**。 <br>

    public class Test {
        Integer i;
        int j;
        public static void main(String[] args) {
            System.out.println(new Test().i);
            System.out.println(new Test().j);
        }
    }
结果输出为: <br>
null <br>
0 <br>

其他需要注意的问题: <br>
1.默认声明的小数是 double 类型的,比如 1.2 默认就是 double 类型的,因此,
在对 float 类型的变量进行赋值的时候需要进行类型转换。如 float i=1.2f; <br>
2.null **不是一个合法的 object 实例,所以并没有为其分配内存**。null 仅仅用于
表明该引用目前没有指向任何对象。 <br>

3.Integer 的缓存策略。 <br>
&ensp;&ensp;&ensp;&ensp;
    在类加载时就将-128 到 127 的 Integer 对象创建了,并保存在 cache 数
组中(**Integer cache[]**),一旦程序调用 **Integer.valueOf( i )** 方法,如果 i 的
值是在 **-128** 到 **127** 之间就直接在 cache 缓存数组中**去取 Integer 对象,不
在的话,就创建新的包装类对象**。 <br>
Short(-128 — 127 缓存) <br>
Long(-128 — 127 缓存) <br>
Float(没有缓存) <br>
Doulbe(没有缓存) <br>

    public static Integer valueOf(int i) {
    if(i >= -128 && i <= IntegerCache.high)
    return IntegerCache.cache[i + 128];
    else
    return new Integer(i);
    }
    
**例子:** <br>
&ensp;&ensp;&ensp;&ensp;
    装箱是将一个原始数据类型赋值给相应封装类的变量,而拆箱则是将一个
封装类的变量赋值给相应原始数据类型的变量。 <br>

    //装箱。装箱就是 jdk 自己帮你完成了调用 Integer.valueOf(100)。
    Integer integer1 = 3;
    Integer integer2 = 3;
    System.out.println(integer1 == integer2);
    Integer integer3 = 300;
    Integer integer4 = 300;
    System.out.println(integer3 == integer4);
    Integer a3 = new Integer(100);
    Integer a4 = new Integer(100);
    System.out.println(a3 == a4);
    int a = 1000, b = 1000;
    System.out.println(a == b);
    Integer c = 1000, d = 1000;
    System.out.println(c == d);
    Integer e = 100, f = 100;
    System.out.println(e == f);
输出: <br>
true <br>
false <br>
false <br>
true <br>
false <br>
true <br>

    int i = 128;
    Integer i2 = 128;
    Integer i3 = new Integer(128);
    // 当 Integer 和 int 类型数值进行比较的时候, Integer 会自动拆箱
    为 int 再比较,所以为 true
    System.out.println(i == i2);
    System.out.println(i == i3);
    System.out.println("**************");
    Integer i5 = 127;// java 在编译的时候,被翻译成-> Integer i5
    = Integer.valueOf(127);
    Integer i6 = 127;
    System.out.println(i5 == i6);// true
    Integer ii5 = new Integer(127);
    System.out.println(i5 == ii5); // false
    
4.包装类作为参数传递时,仍是按值传递。 <br>

    public static void fun(Integer i){
    i=i+2;
    }
    public static void main(String[] args) {
    Integer p=new Integer(5);
    fun(p);
    System.out.println(p);
    }
输出的结果仍然是 5。 <br>

### <a name="6">6. 运算符的优先级。</a>

**(++,--)> (\*,/,%) > (+,-) > (<<,>>) > (&) > ( | ) >&& > ||**

**例子:**

    public static void main(String[] args) {
    byte a = 5;
    int b = 5;
    int c = a >> 2 + b >> 2;
    System.out.println(c);
    }
输出是 0.

    public static void main(String[] args) {
    int a = 10, b = 4, c = 5, d = 9;
    System.out.println(++a * b + c * --d);
    }
输出是 84.

### <a name="7">7. 强制类型转换时的规则有哪些。</a>
&ensp;&ensp;&ensp;&ensp;
    1.当对小于 int 的数据类型(byte,char,short)进行运算时,首先会把这些
类型的**变量值**强制转为 int 类型,对 int 类型的值进行运算,最后得到的值也是
int 类型的。因此,如果把 2 个 short 类型的值相加,最后得到的结果是 int 类型,
如果需要得到 short 类型的结果,就必须显示地运算结果转为 short 类型。
**例子:** short s1=1; s1=s1+1;
编译出错。正确的写法是 short s1 = 1; s1 = (short) (s1 + 1);
**例子:** short s1 = 1;s1 += 1;
编译通过。
&ensp;&ensp;&ensp;&ensp;
    2.基本数据类型和 boolean 类型是不能相互转换的。
&ensp;&ensp;&ensp;&ensp;
    3.char 类型的数据转为高级类型时,会转换为对应的 ASCII 码。

**例题 1:**

    int i=1;
    if(i)
    System.out.println(i);
编译出错。基本数据类型和 boolean 类型是不能相互转换的。

**例题 2:**

    short i = 128;
    System.out.println((byte) i);
&ensp;&ensp;&ensp;&ensp;
    i 对应的二进制为 00000000 10000000,由于 byte 只占一个字节,在强制
转换的时候,从前面开始截掉,因此截掉后的值为二进制的 10000000,也就是
十进制的-128。 <br>

扩展: 数据类型自动转换 <br>
&ensp;&ensp;&ensp;&ensp;
    自动转换按从低到高的顺序转换。不同类型数据间的优先关系如下: <br>
&ensp;&ensp;&ensp;&ensp;
    低 ---------------------------------------------> 高 <br>
&ensp;&ensp;&ensp;&ensp;
    byte,short,char-> int -> long -> float -> double <br>
    
### <a name="8">8. 数组初始化时需要注意的问题。</a>
&ensp;&ensp;&ensp;&ensp;
    1.数组被创建后会根据数组存放的数据类型默认初始化为对应的初始值,
例如,int 类型会初始化为 0,对象类型会初始化为 null。 <br>
&ensp;&ensp;&ensp;&ensp;
    2.2 维数组中,每行元素个数可以不同。 <br>
    
### <a name="9">9. 如何在 main()方法执行前输出“Hello world”?</a>
&ensp;&ensp;&ensp;&ensp;
    用静态代码块。静态代码块在类加载的初始化阶段就会被调用。
    
### <a name="10">10. Java 程序初始化的顺序(对象实例化的过程)。</a>
&ensp;&ensp;&ensp;&ensp;
    1.父类的静态变量、父类的静态代码块 (谁在前,谁先初始化) <br>
&ensp;&ensp;&ensp;&ensp;
    2.子类的静态变量、子类的静态代码块(谁在前,谁先初始化) <br>
&ensp;&ensp;&ensp;&ensp;
    3.父类的非静态变量、父类的非静态代码块(谁在前,谁先初始化)
    、父类的构造函数 <br>
&ensp;&ensp;&ensp;&ensp;
    4.子类的非静态变量、子类的非静态代码块(谁在前,谁先初始化)
    、子类的构造函数 <br>
![04_10](/data/images/Java应届生面试突击/Java基础/04_10.png) <br>
    
### <a name="11">11. 构造函数的特点。</a>
&ensp;&ensp;&ensp;&ensp;
    1.构造函数必须和类名一样(**但和类名一样的不一定是构造方法,普通方
法也可以和类名同名**),并且不能有返回值,返回值也不能为 void。 <br>
&ensp;&ensp;&ensp;&ensp;
    2.构造函数总是伴随着 new 操作一起调用,并且不能由程序的编写者调用,
**只能由系统调用**。 <br>
&ensp;&ensp;&ensp;&ensp;
    3.**构造函数不能被继承**。 <br>
&ensp;&ensp;&ensp;&ensp;
    4.子类可以通过 super()来显示调用父类的构造函数。 <br>

    public class Test {
    public Test() {
    System.out.println("constructor...");
    }
    public void Test() {
    System.out.println("call test14....");
    }
    public static void main(String[] args) {
    new Test().Test();
    }
    }
输出结果为: <br>
constructor... <br>
call test14.... <br>
解析:**和类同名的方法,除了构造方法以外,也可以是普通方法。构造方法不
带返回值,而普通方法是必须有返回值的,这就是区别他们的方法。** <br>

### <a name="12">12. 序列化与反序列化。</a>
* 1.定义 <br>
&ensp;&ensp;&ensp;&ensp;
    把 **Java 对象**转换为**字节序列**的过程称为对象的序列化。
把**字节序列**恢复为 **Java 对象**的过程称为对象的反序列化。 <br>
* 2.实现方式 <br>
&ensp;&ensp;&ensp;&ensp;
    所有实现序列化的类都必须实现 Serializable 接口,它是一种标记接口,里面没有任
何方法。当序列化的时候,需要用到 **ObjectOutputStream** 里面的 **writeObject()**;当反序
列化的时候,需要用到 **ObjectInputStream** 里面的 **readObject()**方法。 <br>
* 3.特点 <br>
&ensp;&ensp;&ensp;&ensp;
    3.1 序列化时,**只对对象的状态进行保存**,而不管对象的方法。 <br>
&ensp;&ensp;&ensp;&ensp;
    3.2 当一个**父类实现序列化**时,子类自动实现序列化,不需要显示实现 Serializable 接口。 <br>
&ensp;&ensp;&ensp;&ensp;
    3.3 当一个对象的实例变量引用了其他对象时,序列化该对象时,也把引用对象进行序列
化。 <br>
&ensp;&ensp;&ensp;&ensp;
    3.4 对象中**被 static 或者 transient 修饰的变量**,在序列化时其变量值是不被保存的。 <br>
* 4.好处 <br>
&ensp;&ensp;&ensp;&ensp;
    一是,实现了**数据的持久化**,通过序列化可以把数据永久地保存到硬盘上(通常存放在
文件里);二是,利用序列化实现**远程通信**,即在网络上传送对象的字节序列。
下面说下版本号。 <br>
&ensp;&ensp;&ensp;&ensp;
    我们在写程序的时候,最好在被序列化的类中显示声明 serialVersionUID.这么做的好
处: <br>
&ensp;&ensp;&ensp;&ensp;
    1.提高程序的运行效率。如果在类中没有显示声明 serialVersionUID,那么在序列化的
时候会通过计算得到该值。如果显示声明该值的话,会省去计算的过程。 <br>
&ensp;&ensp;&ensp;&ensp;
    2. 如 果 你 的 类 没 有 提 供 serialVersionUID , 那 么 编 译 器 会 自 动 生 成 , 而 这 个
serialVersionUID 就是对象的 hashcode 值。那么如果加入新的成员变量,重新生成的
serialVersionUID 将 和 之 前 的 不 同 , 那 么 在 进 行 反 序 列 化 的 时 候 就 会 产 生
java.io.InvalidClassException 的异常。 <br>

&ensp;&ensp;&ensp;&ensp;
    **扩展:ArrayList 和 LinkedList 能否序列化?** <br>
&ensp;&ensp;&ensp;&ensp;
    都可以序列化。 ArrayList 里面的数组 elementData 是声明为 transient 的,表示 ArrayList
在序列化的时候,默认不会序列化这些数组元素。因为 ArrayList 实际上是动态数组,每次
在放满以后会扩容,如果数组扩容后,实际上只放了一个元素,那就会序列化很多 null 元
素,浪费空间,所以 ArrayList **把元素数组设置为 transient,仅仅序列化已经保存的数据**。 <br>
&ensp;&ensp;&ensp;&ensp;
    对象实现 java.io.Serializable 接口以后,序列化的动作不仅取决于对象本身,还取决
于执行序列化的对象。 <br>
&ensp;&ensp;&ensp;&ensp;
    以 ObjectOutputStream 为例,如果 ArrayList 或自定义对象实现了 writeObject(),
readObject(),那么在序列化和反序列化的时候,就按照自己定义的方法来执行动作,所以
**ArrayList 就自定义了 writeObject 和 readObject 方法**,然后在 writeObject 方法内完成
数组元素的自定义序列化动作,在 readObject 方法内完成数组元素的自定义反序列化动作。 <br>

### <a name="13">13. Switch 能否用 string 做参数?</a>
&ensp;&ensp;&ensp;&ensp;
    在 Java 7 之前,switch 只能支持 byte、short、char、int 或者其对
应的包装类以及 Enum 类型。在 Java 7 中,String 支持被加上了。 <br>
&ensp;&ensp;&ensp;&ensp;
    在使用 switch 时,需要注意另外一个问题,如果和匹配的 case 情况中
省略了 break,那么匹配的 case 值后的所有情况都会执行,而不管 case 是
否匹配,一直遇到 break 结束。 <br>

    int x = 2;
    switch (x) {
    case 2:
    System.out.println(x);
    case 3:
    System.out.println(x);
    case 4:
    System.out.println(x);
    break;
    default:
    System.out.println("dddddd");
    }
输出结果为: <br>
2 <br>
2 <br>
2 <br>

### <a name="14">14. equals 与==的区别。</a>
&ensp;&ensp;&ensp;&ensp;
    “==”可用于比较基本数据类型(比较的是他们的值是否相等),也
可以用于比较对象在内存中的存放地址是否相等。 <br>
&ensp;&ensp;&ensp;&ensp;
    JAVA 当中所有的类都是继承于 Object 这个基类的,在 Object 中的基
类中定义了一个 equals 的方法,**这个方法的初始行为是比较对象的内存地
址,但在一些类库当中这个方法被覆盖掉了,如 String,包装类**在这些类
当中 equals 有其自身的实现,而不再是比较类在堆内存中的存放地址了(**对
于 String 的 equals()方法比较二个对象的内容是否相等**)。 <br>
&ensp;&ensp;&ensp;&ensp;
    因此,对于复合数据类型之间进行 equals 比较,**在没有覆写 equals
方法的情况下,他们之间的比较还是基于他们在内存中的存放位置的地址
值的**,因为 Object 的 equals 方法也是用双等号(==)进行比较的,所以比
较后的结果跟双等号(==)的结果相同。 <br>

    public class Example4
    {
        public static void main(String[] args)
        {
            Example4 e=new Example4();
            Example4 e4=new Example4();
            System.out.println(“用 equals(Object) 比较结果”);
            System.out.println(e.equals(e4));
            //结果为 false
            System.out.println(“用 == 比较结果”);
            System.out.println(e==e4);
            //结果为 false
        }
    }
**扩展**: 当调用 **intern 方法**时, 如果池已经包含一个等于此 String 对象
的字符串(该对象由 equals(Object) 方法确定),则返回池中的字符串。否则,
将此 String 对象添加到池中,并且返回此 String 对象的引用。 <br>

### <a name="15">15. Hashcode 的作用。</a>
&ensp;&ensp;&ensp;&ensp;
    hashCode()方法是从 Object 类继承过来的, Object 类中的 hashCode()
方法返回的是对象在内存中的地址转换成的 int 值,如果对象没有重写
hashCode()方法,任何对象的 hashCode()方法的返回值都是不相等的。 <br>
&ensp;&ensp;&ensp;&ensp;
    重写方法:Java 中的 hashCode 方法就是根据一定的规则将与对象相
关的信息(比如对象的存储地址,对象的字段等)映射成一个数值,这个数
值称作为散列值。 <br>
&ensp;&ensp;&ensp;&ensp;
    主要作用是用于查找的,为了配合基于散列的集合一起正常运行,这样
的散列集合包括 HashSet、 HashMap 以及 HashTable, hashCode 是用来
在散列存储结构中确定对象的存储地址的。 <br>
&ensp;&ensp;&ensp;&ensp;
    考虑一种情况,当向集合中插入对象时,如何判别在集合中是否已经存
在该对象了?(注意:集合中不允许重复的元素存在)。 <br>
&ensp;&ensp;&ensp;&ensp;
    当集合要添加新的对象时,先调用这个对象的 hashCode 方法,得到对
应的 hashcode 值;如果在该位置有值,就调用它的 equals 方法与新元素
进行比较,相同的话就不存了,不相同就散列其它的地址。 <br>

&ensp;&ensp;&ensp;&ensp;
    扩展:为什么在重写 equals 方法的同时,必须重写 hashCode 方法? <br>
&ensp;&ensp;&ensp;&ensp;
    回答:比如在使用 set 集合时,往其中放入内容相同的对象,如果没有
重写 hashCode()方法,那么 set 中将会放入内容相同的对象(因为 2 个对
象的地址不同),这和 set 集合的性质不同。因此需要在重写 equals 方法
的同时,必须重写 hashCode 方法。 <br>

    public class HashTest {
        private int i;
        public int getI() {
            return i;
        }
        public void setI(int i) {
            this.i = i;
        }
        
        public boolean equals(Object object) {
            if (object == null) {
                return false;
            }
            if (object == this) {
                return true;
            }
            if (!(object instanceof HashTest)) {
                return false;
            } 
            HashTest other = (HashTest) object;
            if (other.getI() == this.getI()) {
                return true;
            }
            return false;
        }
        
        public int hashCode() {
            return i % 10;
        }
        
        public static void main(String[] args) {
            HashTest a = new HashTest();
            HashTest b = new HashTest();
            a.setI(1);
            b.setI(1);
            Set<HashTest> set = new HashSet<HashTest>();
            set.add(a);
            set.add(b);
            System.out.println(a.hashCode() == b.hashCode());
            System.out.println(a.equals(b));
            System.out.println(set);
        }
    }
此时得到的结果就会如下: <br>
true <br>
true <br>
[com.ubs.sae.test.HashTest@1] <br>

&ensp;&ensp;&ensp;&ensp;
    Java 对于 equals()方法和 hashCode()方法是这样规定的: <br>
&ensp;&ensp;&ensp;&ensp;
    1.如果 2 个对象的 equals()方法返回 true,则 hashCode()返回的值也
相同。 <br>
&ensp;&ensp;&ensp;&ensp;
    2.如果 2 个对象的 equals()方法返回 false,则 hashCode()返回的值可
能相同,也可能不相同。 <br>
&ensp;&ensp;&ensp;&ensp;
    3.如果 2 个对象的 hashCode()方法返回值相同,则 equals()返回的值
可能为 true,也可能为 false。 <br>
&ensp;&ensp;&ensp;&ensp;
    4.如果 2 个对象的 hashCode()方法返回值不同,则 equals()返回的值
为 false。 <br>

### <a name="16">16. hashCode() 与 equals() 生成算法、方法怎么重写。</a>
&ensp;&ensp;&ensp;&ensp;
    1.尽量保证使用对象的同一个属性来生成 hashCode()和 equals()两个
方法。 <br>
&ensp;&ensp;&ensp;&ensp;
    2.在重写 equals 方法的同时,必须重写 hashCode 方法(二者必须同时
重写)。 <br>

    //age 是 int 类型的,id 是 Integer 类型的
    public boolean equals(Object obj) {
        if (this == obj)
        return true;
        if (obj == null)
        return false;
        if (getClass() != obj.getClass())
        return false;
        Employee other = (Employee) obj;
        if (age != other.age)
        return false;
        if (id == null) {
            if (other.id != null)
            return false;
        } else if (!id.equals(other.id))
        return false;
        return true;
    }
    
    public int hashCode() {
        final int prime = 31;
        int result = 1;
        result = prime * result + age;
        result = prime * result + ((id == null) ? 0 : id.hashCode());
        return result;
    }
    
### <a name="17">17. Object 有哪些公用方法?</a>
&ensp;&ensp;&ensp;&ensp;
    1.clone() :创建并返回此对象的一个副本。 <br>

&ensp;&ensp;&ensp;&ensp;
    2.equals(Object obj):指示其他某个对象是否与此对象的地址“相等”。
    hashCode():返回该对象的哈希码值。 <br>

&ensp;&ensp;&ensp;&ensp;    
    3.wait() :
    notify() :唤醒在此对象监视器上等待的单个线程。
    notifyAll():唤醒在此对象监视器上等待的所有线程。
 
&ensp;&ensp;&ensp;&ensp;   
    4.toString():返回该对象的字符串表示。 <br>

&ensp;&ensp;&ensp;&ensp;   
    5.finalize():当垃圾回收器确定不存在对该对象的更多引用时,由对象的
    垃圾回收器调用此方法。 <br>

&ensp;&ensp;&ensp;&ensp;    
    6.getClass():返回此 Object 的运行时类。 <br>
    
### <a name="18">18. String、StringBuffer 与 StringBuilder 的区别。</a>
1.可变与不可变 <br>
&ensp;&ensp;&ensp;&ensp;
    string 对象是不可变的;StringBuilder 与 StringBuffer 对象是可变的。
因此在每次对 String 类型进行改变的时候,都会生成一个新的 String 对象,然后
将指针指向新的 String 对象,所以经常改变内容的字符串最好不要用 String ,因为每次
生成对象都会对系统性能产生影响,特别当内存中无引用对象多了以后, JVM 的 GC 就
会开始工作,性能就会降低。 <br>
&ensp;&ensp;&ensp;&ensp;
    修改 String 对象的原理:首先创建一个 StringBuffer 对象,然后调用 append()方
法,最后调用 toString()方法。 <br>
&ensp;&ensp;&ensp;&ensp;
    
    String s=”Hello”;
    S+=”World”;
    等价于: 
    StringBuffer
    sb=new StringBuffer(s); 
    sb.append(“World”); 
    sb.toString(); 
&ensp;&ensp;&ensp;&ensp;
    使用 StringBuffer 类时,每次都会对 StringBuffer 对象本身进行操作,而不是生
成新的对象并改变对象引用。所以多数情况下推荐使用 StringBuffer ,特别是字符串对
象经常改变的情况下。 <br>

2.是否多线程安全 <br>
&ensp;&ensp;&ensp;&ensp;
    String 和 StringBuffer 是线程安全的。 StringBuilder 并没有对方法进行加同步锁,
所以是非线程安全的。 <br>

3.初始化方式的不同 <br>
&ensp;&ensp;&ensp;&ensp;
    StringBuffer 和 StringBuilder 只能用构造函数的形式来初始化。 String 除了用构
造函数进行初始化外,还可以直接赋值。 <br>
### <a name="19">19. try catch finally,try 里有 return,finally 还执行么?如果会的话,什么时候执行,在 return 之前还是 return 之后?</a>
1.finally 块里的代码在 return 之前执行。 <br>
2.如果 finally 块中有 return 语句的话,它将覆盖掉函数中其他 return 语
句。 <br>

1.如果 finally 块中,改变了 try 块中返回变量的值,该变量为基本数据类
型的话,则 finally 块中改变变量值的语句将不起作用;如果该变量为引用
变量的话,则起作用。 <br>
2.Finally 块中的代码不一定执行。
比如,try 块执行之前,出现了异常,则程序终止。
比如,在 try 块中执行了
System.exit(0)。 <br>

### <a name="20">20. 说下异常的原理。</a>
异常是指程序运行时所发生的错误。 <br>
Throwable 是所有异常的父类,它有 2 个子类:Error 和 Exception。 <br>

1.Error 表示程序在运行期间发生了非常严重的错误,并且该错误是不可恢
复的。Error 不需要捕捉。如 OutOfMemoryError。 <br>

2.Exception 是可恢复的异常。它包含 2 种类型:检查异常和运行时异常。 <br>
&ensp;&ensp;&ensp;&ensp;
    2.1 检查异常(Checked Exception) <br>
比如 IOException、SQLException 和 FileNotFoundException 都是检查
异常。它发生在编译阶段,编译器会强制程序去捕获此类异常,需要在编码时
用 try-catch 捕捉。 <br>
&ensp;&ensp;&ensp;&ensp;
    2.2 运行时异常(RuntimeException) <br>
它发生在运行阶段,编译器不会检查运行时异常。比如空指针异常,算
数运算异常,数组越界异常等。如果代码会产生 RuntimeException 异常,则需
要通过修改代码进行避免。例如,若会发生除数为零的情况,则需要通过代码
避免该情况的发生! <br>
&ensp;&ensp;&ensp;&ensp;
    在处理异常的时候,需要注意:捕获异常的时候,先捕获子类异常,再捕
获父类异常。 <br>
### <a name="21">21. Java 面向对象的三个特征与含义。</a>
&ensp;&ensp;&ensp;&ensp;
    封装:属性的封装和方法的封装。把属性定义为私有的,get(),set()方法。
好处是信息隐藏和模块化,提高安全性。封装的主要作用在于对外隐藏内
部实现细节,增强程序的安全性。 <br>

&ensp;&ensp;&ensp;&ensp;
    继承:子类可以继承父类的成员变量和成员方法。继承可以提高代码的复
用性。 <br>

继承的特性: <br>
1.单一继承。 <br>
2.子类只能继承父类的非私有成员变量和方法。 <br>
3.成员变量的隐藏和方法的覆盖。 <br>

&ensp;&ensp;&ensp;&ensp;
    多态:当同一个操作作用在不同对象时,会产生不同的结果。实现原理见
下面。 <br>

### <a name="22">22. java 多态的实现原理(实现机制)。</a>
&ensp;&ensp;&ensp;&ensp;
    有 2 种方式来实现多态,一种是编译时多态,另外一种是运行时多态;编
译时多态是通过方法的重载来实现的,运行时多态是通过方法的重写来实现的。 <br>
&ensp;&ensp;&ensp;&ensp;
    方法的重载,指的是同一个类中有多个同名的方法,但这些方法有着不同
的参数。在编译时就可以确定到底调用哪个方法。 <br>
&ensp;&ensp;&ensp;&ensp;
    方法的重写,子类重写父类中的方法。父类的引用变量不仅可以指向父类
的实例对象,还可以指向子类的实例对象。当父类的引用指向子类的对象时,
只有在运行时才能确定调用哪个方法。 <br>
&ensp;&ensp;&ensp;&ensp;
    特别注意:只有类中的方法才有多态的概念,类中成员变量没有多态的概
念。 <br>
&ensp;&ensp;&ensp;&ensp;
    其余部分见“重载和覆盖的区别”。 <br>

### <a name="23">23. Override(覆盖、重写)和 Overload(重载)的区别。</a>
&ensp;&ensp;&ensp;&ensp;
    重载和覆盖是 java 多态性的不同表现方式。 <br>
&ensp;&ensp;&ensp;&ensp;
    重载是在一个类中多态性的一种表现,是指在一个类中定义了多个同名的
方法,但是他们有不同的参数个数或有不同的参数类型。 <br>

在使用重载时要注意以下几点: <br>
&ensp;&ensp;&ensp;&ensp;
    1.重载只能通过不同的方法参数来区分。例如不同的参数类型,不同的
参数个数,不同的参数顺序。 <br>
&ensp;&ensp;&ensp;&ensp;
    2.不能通过访问权限、返回类型、抛出的异常进行重载。
覆盖是指子类函数覆盖父类中的函数。 <br>

在覆盖时要注意以下几点(重点!!): <br>
&ensp;&ensp;&ensp;&ensp;
    1.覆盖的方法的函数名和参数必须要和被覆盖的方法的函数名和参数完全
匹配,才能达到覆盖的效果; <br>
&ensp;&ensp;&ensp;&ensp;
    2.覆盖的方法的返回值必须和被覆盖的方法的返回值类型一致; <br>
&ensp;&ensp;&ensp;&ensp;
    3.覆盖的方法所抛出的异常必须和被覆盖方法的所抛出的异常一致,或者
是其子类; <br>
&ensp;&ensp;&ensp;&ensp;
    4.被覆盖的方法不能为 private,否则在其子类中只是新定义了一个方法,
并没有对其进行覆盖。 <br>
&ensp;&ensp;&ensp;&ensp;
    5.子类函数的访问修饰权限要大于等于父类的
(public>protected>default>private) 。(重要!!!) <br>
特别注意:Java 中,子类无法覆盖父类的 static 方法或 private 方法。 <br>

    class Parent {
        public static void p() {
            System.out.println("parent....");
        }
    }
    
    public class Test19 extends Parent {
        public static void p() {
            System.out.println("child...");
        }
        
        public static void main(String[] args) {
            Parent parent = new Test19();
            parent.p();
        }
    }
输出: <br>
parent.... <br>
原因:Java 中,子类无法覆盖父类的 static 方法。 <br>

### <a name="24">24. 接口与抽象类的区别。</a>
* 1.语法层面上的区别 <br>
&ensp;&ensp;&ensp;&ensp;
    1)抽象类可以提供成员方法的实现细节(注:可以只包含非抽象方法),
而接口中只能存在 public abstract 方法,方法默认是 public abstract 的,
但是,java8 中接口可以有 default 方法; <br>
&ensp;&ensp;&ensp;&ensp;
    2)抽象类中的成员变量可以是各种类型的,而接口中的成员变量只能是
public static final 类型的; <br>
&ensp;&ensp;&ensp;&ensp;
    3)抽象类可以有静态代码块和静态方法和构造方法;接口中不能含有静态
代码块以及静态方法以及构造方法。但是,java8 中接口可以有静态方法; <br>
&ensp;&ensp;&ensp;&ensp;
    4)一个类只能继承一个抽象类,而一个类却可以实现多个接口。 <br>
    
* 2.设计层面上的区别 <br>
&ensp;&ensp;&ensp;&ensp;
    1) 抽象层次不同。抽象类是对类的整体抽象,包括属性和行为的抽象。
而接口只是对行为的抽象。 <br>
&ensp;&ensp;&ensp;&ensp;
    2)跨域不同。抽象类所体现的是一种继承关系,父类和派生类之间必须
存在"is-a" 关系,即父类和派生类在概念本质上应该是相同的。对于接口
则不然,并不要求接口的实现者和接口定义在概念本质上是一致的, 仅仅
是实现了接口定义的契约而已,其设计理念是“has-a”的关系(有没有、
具备不具备的关系),实现它的子类可以不存在任何关系,共同之处。例如
猫、狗可以抽象成一个动物类抽象类,具备叫的方法。鸟、飞机可以实现飞
Fly 接口,具备飞的行为,这里我们总不能将鸟、飞机共用一个父类吧! <br>
&ensp;&ensp;&ensp;&ensp;
    3) 设计层次不同。对于抽象类而言,它是自下而上来设计的,我们要先
知道子类才能抽象出父类,而接口则不同,它根本就不需要知道子类的存在,
只需要定义一个规则即可,至于什么子类、什么时候怎么实现它一概不知。
比如我们只有一个猫类在这里,如果你这时就抽象成一个动物类,是不是设
计有点儿过度?我们起码要有两个动物类,猫、狗在这里,我们再抽象他们
的共同点形成动物抽象类吧!所以说抽象类往往都是通过重构而来的!但是
接口就不同,比如说飞,我们根本就不知道会有什么东西来实现这个飞接口,
怎么实现也不得而知,我们要做的就是事前定义好飞的行为接口。所以说抽
象类是自底向上抽象而来的,接口是自顶向下设计出来的。 <br>
### <a name="25">25. 静态内部类和非静态内部类的区别。</a>
    /* 下面程序演示如何在 java 中创建静态内部类和非静态内部类 */
    class OuterClass {
        private static String msg = "GeeksForGeeks";
        // 静态内部类
        public static class NestedStaticClass {
        // 静态内部类只能访问外部类的静态成员和静态方法
            public void printMessage() {
                // 试着将 msg 改成非静态的,这将导致编译错误
                System.out.println("Message from nested static class:
                " + msg);
            }
        }
        // 非静态内部类
        public class InnerClass {
            // 不管是静态方法还是非静态方法都可以在非静态内部类中访问
            public void display() {
                System.out.println("Message from non-static nested
                class: " + msg);
            }
        }
    }
    
    public class Main {
        // 怎么创建静态内部类和非静态内部类的实例
        public static void main(String args[]) {
            
            // 创建静态内部类的实例(注意前面还是要加外部类的名字的!!!)
            OuterClass.NestedStaticClass printer = new
            OuterClass.NestedStaticClass();
            
            // 调用静态内部类的非静态方法
            printer.printMessage();
            
            // 为了创建非静态内部类,我们需要外部类的实例
            OuterClass outer = new OuterClass();
            OuterClass.InnerClass inner = outer.new InnerClass();
            
            // 调用非静态内部类的非静态方法
            inner.display();
            
            // 我们也可以结合以上步骤,一步创建的内部类实例
            OuterClass.InnerClass innerObject = new OuterClass().new InnerClass();         
            
            // 同样我们现在可以调用内部类方法
            innerObject.display();
        }
    }

静态内部类和非静态内部类主要的不同: <br>
&ensp;&ensp;&ensp;&ensp;
    (1)静态内部类不依赖于外部类实例而被实例化,而非静态内部类需要在
外部类实例化后才可以被实例化。 <br>
&ensp;&ensp;&ensp;&ensp;
    (2)静态内部类不需要持有外部类的引用。但非静态内部类需要持有对外
部类的引用。 <br>
&ensp;&ensp;&ensp;&ensp;
    (3)静态内部类不能访问外部类的非静态成员和非静态方法。它只能访问
外部类的静态成员和静态方法。非静态内部类能够访问外部类的静态和非静态
成员和方法。 <br>

扩展:内部类都有哪些? <br>
&ensp;&ensp;&ensp;&ensp;
    有四种:静态内部类,非静态内部类,局部内部类,匿名内部类。 <br>
&ensp;&ensp;&ensp;&ensp;
    1.静态内部类和 2.非静态内部类的讲解见上面的部分。 <br>
&ensp;&ensp;&ensp;&ensp;
    3.局部内部类:在外部类的方法中定义的类。其作用的范围是所在的方法 <br>
内。它不能被 public,private,protected 来修饰。它只能访问方法中定义为 final
类型的局部变量。 <br>

    class outerClass{
        public void f(){
            class innerClass{//局部内部类
            }
        }
    }
4.匿名内部类 <br>

    interface Person {
        public abstract void eat();
    }
    public class Test4 {
        public static void main(String[] args) {
            Person p = new Person() {
                public void eat() {
                    System.out.println("eat something");
                }
            };
            p.eat();
        }
    }
是一种没有类名的内部类。 <br>

需要注意的是: <br>
&ensp;&ensp;&ensp;&ensp;
    4.1 匿名内部类一定是在 new 的后面,这个匿名内部类必须继承一个父类
或者实现一个接口。 <br>
&ensp;&ensp;&ensp;&ensp;
    4.2 匿名内部类不能有构造函数。 <br>
&ensp;&ensp;&ensp;&ensp;
    4.3 只能创建匿名内部类的一个实例。 <br>
&ensp;&ensp;&ensp;&ensp;
    4.4 在 Java 8 之前,如果匿名内部类需要访问外部类的局部变量,则必须
使用 final 来修饰外部类的局部变量。在现在的 Java 8 已经去取消了这个限制。 <br>

### <a name="26">26. static 的使用方式。</a>
&ensp;&ensp;&ensp;&ensp;
    static 有 4 种使用方式:修饰类(静态内部类),修饰成员变量(静态变
量),修饰成员方法(静态成员方法),静态代码块。。 <br>
&ensp;&ensp;&ensp;&ensp;
    1.修饰类(静态内部类)。 <br>
参考上面的介绍。
&ensp;&ensp;&ensp;&ensp;
    2.修饰成员变量(静态变量)。 <br>
    静态变量属于类,只要静态变量所在的类被加载,这个静态变量就会被分
配空间,在内存中只有一份,所有对象共享这个静态变量。使用有二种方式,
一个是类名.静态变量,还有一种是对象.静态变量。**特别注意:不能在方法体中
定义静态变量(无论该方法是静态的或是非静态的)。VS **实例变量属于类,只
有对象创建后,实例变量才会分配空间。。 <br>
&ensp;&ensp;&ensp;&ensp;
    3.修饰成员方法(静态成员方法)
    静态成员方法属于类,不需要创建对象就可以使用。而非静态方法属于对
象,只有在对象创建出来以后才可以被使用。静态方法里面只能访问所属类的
静态成员变量和静态成员方法。。 <br>
&ensp;&ensp;&ensp;&ensp;
    4.静态代码块。 <br>
    静态代码块经常被用来初始化静态变量,在类加载的初始化阶段会执行为
静态变量赋值的语句和静态代码块的内容,静态代码块只会被执行一次。


### <a name="27">27. 反射的作用与原理。如何提高反射效率?</a>
&ensp;&ensp;&ensp;&ensp;
    1.定义:反射机制是在运行时,对于任意一个类,都能够知道这个类的所
有属性和方法;对于任意一个对象,都能够调用它的任意一个方法。在 java 中,
只要给定类的名字,那么就可以通过反射机制来获得类的所有信息。 <br>
&ensp;&ensp;&ensp;&ensp;
    2.反射机制主要提供了以下功能:在运行时判定任意一个对象所属的类;
在运行时创建对象;在运行时判定任意一个类所具有的成员变量和方法;在运
行时调用任意一个对象的方法;生成动态代理。 <br>
&ensp;&ensp;&ensp;&ensp;
    3.哪里用到反射机制? <br>
jdbc 中有一行代码: <br>
Class.forName('com.mysql.jdbc.Driver.class'); //加载 MySql 的驱动类。 这就
是反射,现在很多框架都用到反射机制,hibernate,struts 都是用反射机制实
现的。 <br>
&ensp;&ensp;&ensp;&ensp;
    4.反射的实现方式 <br>
在 Java 中实现反射最重要的一步,也是第一步就是获取 Class 对象,得到
Class 对象后可以通过该对象调用相应的方法来获取该类中的属性、方法以及调
用该类中的方法。 <br>
&ensp;&ensp;&ensp;&ensp;
    有 4 种方法可以得到 Class 对象: <br>
&ensp;&ensp;&ensp;&ensp;
    1.Class.forName(“类的路径”); <br>
&ensp;&ensp;&ensp;&ensp;
    2.类名.class。 <br>
&ensp;&ensp;&ensp;&ensp;
    3.对象名.getClass()。 <br>
&ensp;&ensp;&ensp;&ensp;
    4.如果是基本类型的包装类,则可以通过调用包装类的 Type 属性来获得
该包装类的 Class 对象。 <br>
&ensp;&ensp;&ensp;&ensp;
    例如:Class<?> clazz = Integer.TYPE; <br>

5.实现 Java 反射的类 <br>
1)Class:它表示正在运行的 Java 应用程序中的类和接口。 <br>
2)Field:提供有关类或接口的属性信息,以及对它的动态访问权限。 <br>
3)Constructor:提供关于类的单个构造方法的信息以及对它的访问权限 <br>
4)Method:提供关于类或接口中某个方法信息。 <br>
注意:Class 类是 Java 反射中最重要的一个功能类,所有获取对象的信息(包
括:方法/属性/构造方法/访问权限)都需要它来实现。 <br>

6.反射机制的优缺点? <br>

优点: <br>
(1)能够运行时动态获取类的实例,大大提高程序的灵活性。 <br>
(2)与 Java 动态编译相结合,可以实现无比强大的功能。 <br>

缺点: <br>
(1)使用反射的性能较低。 java 反射是要解析字节码,将内存中的对象进
行解析。 <br>
&ensp;&ensp;&ensp;&ensp;
    解决方案: <br>
&ensp;&ensp;&ensp;&ensp;
    1.由于 JDK 的安全检查耗时较多,所以通过 setAccessible(true)的方式关闭安全检查
来(取消对访问控制修饰符的检查)提升反射速度。 <br>
&ensp;&ensp;&ensp;&ensp;
    2.需要多次动态创建一个类的实例的时候,有缓存的写法会比没有缓存要快很多: <br>
&ensp;&ensp;&ensp;&ensp;
    3.ReflectASM 工具类 ,通过字节码生成的方式加快反射速度。 <br>
(2)使用反射相对来说不安全,破坏了类的封装性,可以通过反射获取这个
类的私有方法和属性。 <br>

### <a name="28">28. Java 和 C++/C 的区别,JAVA 的优点。</a>
&ensp;&ensp;&ensp;&ensp;
    1.运行过程的不同。JAVA 源程序经过编译器编译成字节码文件,然后由 JVM
解释执行。而 C++/C 经过编译、链接后生成可执行的二进制代码。因此 C/C++
的执行速度比 JAVA 快。 <br>
&ensp;&ensp;&ensp;&ensp;
    2.跨平台性。JAVA 可以跨平台,而 C++/C 不可以跨平台。 <br>
&ensp;&ensp;&ensp;&ensp;
    3.JAVA 没有指针,C++/C 有指针。 <br>
&ensp;&ensp;&ensp;&ensp;
    4. JAVA 不支持多重继承,但是可以同时实现多个接口来达到类似的目的。
C++支持多重继承。 <br>
&ensp;&ensp;&ensp;&ensp;
    5.JAVA 不需要对内存进行管理,有垃圾回收机制。C/C++需要对内存进行显
示的管理。 <br>
&ensp;&ensp;&ensp;&ensp;
    6.JAVA 不支持运算符重载。C/C++支持运算符重载。 <br>
&ensp;&ensp;&ensp;&ensp;
    7.JAVA 中每个数据类型在不同的平台上所占字节数固定的,而 C/C++则不
然。 <br>

JAVA 的优点:
&ensp;&ensp;&ensp;&ensp;
    1.跨平台。JAVA 语言可以“一次编译,到处运行”。跨平台的含义:无论是
在 windows 平台还是在 Linux 平台对 Java 程序进行编译,编译后的程序都可以
在其他平台上运行。编译器会把 JAVA 代码编译成字节码文件,然后在 JVM 上解
释执行,由于字节码与平台无关,因此,JAVA 可以很好地跨平台执行。 <br>
&ensp;&ensp;&ensp;&ensp;
    2.垃圾回收机制。 <br>
&ensp;&ensp;&ensp;&ensp;
    3.去掉了 C++中难以理解的东西,比如指针和运算符重载。 <br>
&ensp;&ensp;&ensp;&ensp;
    4.具有较好的安全性。比如 JAVA 有数组边界检测,但是 C/C++里面没有。 <br>

### <a name="29">29. 同一个.java 文件中是否可以有多个 main()方法?</a>
&ensp;&ensp;&ensp;&ensp;
    每个类中都可以定义 main()方法,但只有用 public 修饰的类且与文件名相
同的类中的 main()方法才可以作为整个程序的入口方法。 <br>
例子: <br>
创建了一个名为 Test17.java 的文件。 <br>

    class T {
        public static void main(String[] args) {
            System.out.println("T main");
        }
    }
    
    public class Test17 {
        public static void main(String[] args) {
            System.out.println("Test main");
        }
    }
输出: <br>
Test main <br>

### <a name="30">30. JAVA 中的类和成员的访问控制。</a>
&ensp;&ensp;&ensp;&ensp;
    类的访问控制。可以用 public 和不含 public 的来修饰。 <br>
&ensp;&ensp;&ensp;&ensp;
    成员的访问控制。 <br>
&ensp;&ensp;&ensp;&ensp;
    如果一个类是用 public 来修饰的,它的成员用第一列的访问修饰符时,在
不同范围的类和对象是否有权访问它们。 <br>
[04_30](/data/images/Java应届生面试突击/Java基础/04_30.png) <br>

### <a name="31">31. System.out.println()方法使用时需要注意的问题。</a>
    
    public class Test18 {
        public static void main(String[] args) {
            System.out.println(1 + 2 + "");
            System.out.println("" + 1 + 2);
        }
    }
输出: <br>
3 <br>
12 <br>

### <a name="32">32. 继承和组合区别。</a>
组合和继承是代码复用的 2 种方式。 <br>
&ensp;&ensp;&ensp;&ensp;
    1.组合是在新类里面创建原有类的对象,重复利用已有类的功能。 <br>
&ensp;&ensp;&ensp;&ensp;
    2.组合关系在运行期决定,而继承关系在编译期就已经决定了。 <br>
&ensp;&ensp;&ensp;&ensp;
    3.使用继承关系时,可以实现类型的回溯,即用父类变量引用子类对象,这样
便可以实现多态,而组合没有这个特性。 <br>
&ensp;&ensp;&ensp;&ensp;
    4.从逻辑上看,组合最主要地体现的是一种整体和部分的思想,例如在电脑类
是由内存类,CPU 类,硬盘类等等组成的,而继承则体现的是一种可以回溯的父子
关系,子类也是父类的一个对象。 <br>

### <a name="33">33. final finally finalize 的区别。</a>
final 可以用来修饰类,变量和方法。
&ensp;&ensp;&ensp;&ensp;
    1.当一个类被 final 修饰的时候,表示该类不能被继承。类中方法默认被
final 修饰。 <br>
&ensp;&ensp;&ensp;&ensp;
    2.当 final 修饰基本数据类型的变量时,表示该值在被初始化后不能更改;
当 final 修饰引用类型的变量时,表示该引用在初始化之后不能再指向
其他的对象。 <br>
注意:final 修饰的变量必须被初始化。可以在定义的时候初始化,也可
以在构造函数中进行初始化。 <br>
&ensp;&ensp;&ensp;&ensp;
    3.当 final 修饰方法时,表示这个方法不能被子类重写。 <br>
使用 final 方法的原因有 2 个: <br>
第一、把方法锁定,防止任何继承类修改它的实现。 <br>
第二、高效。当要使用一个被声明为 final 的方法时,直接将方法主体插
入到调用处,而不进行方法调用,可以提高程序的执行效率(ps.如果过多的话,
这样会造成代码膨胀)。 <br>
扩展:String 类为什么要设计成 final 类型的? <br>
java 中不仅 String 是 final 的。 Long, Double, Integer 之类的全都是
final 的。 <br>
&ensp;&ensp;&ensp;&ensp;
    1. Requirement of String Pool <br>
&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;
        If a string is not immutable, changing the string with one reference will
    lead to the wrong value for the other references. <br>
&ensp;&ensp;&ensp;&ensp;
    2. Caching Hashcode <br>
&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;
        因为字符串是不可变的,所以在它创建的时候 hashcode 就被缓存了,不需要重新计
    算。 <br>
&ensp;&ensp;&ensp;&ensp;
    3.线程安全 <br>
&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;
        Because immutable objects can not be changed, they can be shared <br>
&ensp;&ensp;&ensp;&ensp;
    among multiple threads freely. This eliminates the requirements of doing <br>
&ensp;&ensp;&ensp;&ensp;
    synchronization(不用同步了)。. <br>
&ensp;&ensp;&ensp;&ensp;
    4.为了防止扩展类无意间破坏原来方法的实现。 <br>
&ensp;&ensp;&ensp;&ensp;
    finally 的用法: <br>
&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;
        finally 是异常处理的一部分,只能用在 try-catch 语句中,表示这段代码
    一般情况下,一定会执行。经常用在需要释放资源的情况下。 <br>
&ensp;&ensp;&ensp;&ensp;
    finalize 的用法: <br>
&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;
        它是 Object 类的一个方法,在垃圾回收器执行时会调用被回收对象的
    finalize()方法。

### <a name="34">34. JDK1.7 和 1.8 的区别。</a>
接口的默认方法。
Java 8 允许我们给接口添加一个非抽象的方法实现,只需要使用 default
关键字即可,这个特征又叫做扩展方法,Default 方法带来的好处是,往接口新
增一个 Default 方法,在接口添加新功能特性,而不破坏现有的实现架构。示
例如下:

    interface Formula {
        double calculate(int a);
        default double sqrt(int a) {
            return Math.sqrt(a);
        }
    }
Formula 接口在拥有 calculate 方法之外同时还定义了 sqrt 方法,实
现了 Formula 接口的子类只需要实现一个 calculate 方法,默认方法 sqrt 将
在子类上可以直接使用。
    
    Formula formula = new Formula() {
        public double calculate(int a) {
            return sqrt(a * 100);
        }
    };
    formula.calculate(100);// 100.0
    formula.sqrt(16);// 4.0

### <a name="35">35. List<String>能否转为List<Object>?能否List<Object>list=newArrayList<String>()?List<String>list=new ArrayList<Object>()?原因? </a>
&ensp;&ensp;&ensp;&ensp;    
    都不可以,会出现编译错误。List<Object>可以存储任何类型的对象,
包括 String,Integer 等,而 ArrayList<String>只能用来存储字符串。

### <a name="36">36. 泛型的好处?</a>
&ensp;&ensp;&ensp;&ensp;
    在编译的时候检查类型安全,确保只能把正确类型的对象放入集合中;消
除强制类型转换。
