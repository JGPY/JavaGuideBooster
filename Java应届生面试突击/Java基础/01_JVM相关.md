# JVM相关

### 目录

---
<a href="#1">1. 说一下 Java 的垃圾回收机制</a> <br>
<a href="#2">2. JVM 的内存布局/内存模型。(需要详细到每个区放什么)</a> <br>
<a href="#3">3. JVM 的4种引用和使用场景?</a> <br>
<a href="#4">4. 说一下引用计数法与可达性分析算法。</a> <br>
<a href="#5">5. 如何判断对象是不是垃圾?</a> <br>
<a href="#6">6. 堆里面的分区和各自的特点。</a> <br>
<a href="#7">7. Minor GC 与 Full GC 分别在什么时候发生?</a> <br>
<a href="#8">8. 对象创建方法,对象的内存布局,对象的访问定位。</a> <br>
<a href="#9">9. 说一下几种垃圾收集算法的原理和特点,应用的场景。怎么优化复制算法?</a> <br>
<a href="#10">10. GC 收集器有哪些?CMS 收集器与 G1 收集器的特点。</a> <br>
<a href="#11">11. 什么是内存泄露和内存溢出。</a> <br>
<a href="#12">12. 如何减少 gc 出现的次数(java 内存管理)。(重点!!!!)</a> <br>
<a href="#13">13. 数组多大放在 JVM 老年代? 永久代对象如何 GC?如果想不被 GC 怎么办?如果想在 GC 中生存 1 次怎么办?</a> <br>
<a href="#14">14. JVM 常见的启动参数。</a> <br>
<a href="#15">15. 说下几种常用的内存调试工具: jps、 jmap、 jhat、 jstack、 jconsole,jstat。</a> <br>
<a href="#16">16. 说下虚拟机的类加载机制。</a> <br>
<a href="#17">17. 说下双亲委派模型。双亲委派模型中有哪些方法。用户如何自定义类加载器 。怎么打破双亲委托机制?</a> <br>
<a href="#18">18. 描述 Java 类加载器的工作原理及其组织结构。</a> <br>
<a href="#21">21. Java 编译的过程。</a> <br>
<a href="#22">22. class 文件是什么类型文件(字节码文件的格式)?</a> <br>
<a href="#23">23. 即时编译器的优化方法。</a> <br>
<a href="#24">24. 静态分派与动态分派。</a> <br>
<a href="#25">25. 编译阶段对程序做了哪些优化?</a> <br>
<a href="#26">26. new 的对象如何不分配在堆而分配在栈上?</a> <br>


### <a name="1">1. 说一下Java的垃圾回收机制。</a>
&ensp;&ensp;&ensp;&ensp;它使得 Java 程序员在编写程序的时候不再需要考虑内存管理。垃圾回收器
通常是作为一个单独的低级别的线程运行,不可预知的情况下对内存堆中已经
死亡的或者长时间没有使用的对象进行清除和回收,程序员不能实时的调用垃
圾回收器对某个对象或所有对象进行垃圾回收。程序员可以手动执行
System.gc(),通知 GC 运行,但是 Java 语言规范并不保证 GC 一定会执行。 <br>
&ensp;&ensp;&ensp;&ensp; 垃圾回收机制可以用3个词来概括:where,when和how? <br>
&ensp;&ensp;&ensp;&ensp; Where:运行时的内存分布情况。见下一题。<br>
&ensp;&ensp;&ensp;&ensp; When:对象何时需要被回收的?也就是何时回收无效对象,已死对象的? <br>
&ensp;&ensp;&ensp;&ensp; 这里涉及到两种做法:引用计数法和可达性分析算法。这里还涉及到java
中4种引用方式:强引用,软引用,弱引用和虚引用,其引用强度越来越来低,意味着引用越弱的对象越容易被垃圾回收的。<br>
&ensp;&ensp;&ensp;&ensp; how:对象如何被回收的?4 种垃圾回收算法。

### <a name="2">2. JVM的内存布局/内存模型。(需要详细到每个区放什么)</a>
区别于”JAVA 的内存模型”
图图图
参见《深入理解 java 虚拟机》。

### <a name="3">3. JVM的4种引用和使用场景?</a>
&ensp;&ensp;&ensp;&ensp; 
 这4种级别由高到低依次为:强引用、软引用、弱引用和虚引用。 <br>
&ensp;&ensp;&ensp;&ensp; 
    (1)强引用(StrongReference) <br>
&ensp;&ensp;&ensp;&ensp; 
    强引用是使用最普遍的引用。如果一个对象具有强引用,那垃圾回收器绝
不会回收它。当内存空间不足, Java 虚拟机宁愿抛出 OutOfMemoryError 
错误,使程序异常终止,也不会靠随意回收具有强引用的对象来解决内存不足的问
题。 ps:强引用其实也就是我们平时 A a = new A()这个意思。 <br>
&ensp;&ensp;&ensp;&ensp; 
    (2)软引用(SoftReference) <br>
&ensp;&ensp;&ensp;&ensp;     
    如果一个对象只具有软引用,则内存空间足够,垃圾回收器就不会回收它;
如果内存空间不足了,就会回收这些对象的内存。只要垃圾回收器没有回收它,
该对象就可以被程序使用。软引用可用来实现内存敏感的高速缓存(下文给出
示例)。 <br>
&ensp;&ensp;&ensp;&ensp; 
    软引用可以和一个引用队列(ReferenceQueue)联合使用,如果软引用所
引用的对象被垃圾回收器回收,Java 虚拟机就会把这个软引用加入到与之关联
的引用队列中。 <br>
&ensp;&ensp;&ensp;&ensp; 
    示例:实现学生信息查询操作时有两套数据操作的方案。 <br>
    &ensp;&ensp;&ensp;&ensp; 
    一、将得到的信息存放在内存中,后续查询则直接读取内存信息(优点:
读取速度快;缺点:内存空间一直被占,若资源访问量不高,则浪费内存空间)。 <br>
&ensp;&ensp;&ensp;&ensp; 
    二、每次查询均从数据库读取,然后填充到 TO 返回。(优点:内存空间
将被 GC 回收,不会一直被占用;缺点:在 GC 发生之前已有的 TO 依然存在,
但还是执行了一次数据库查询,浪费 IO)。可以通过软引用来解决。 <br>
&ensp;&ensp;&ensp;&ensp; 
    (3)弱引用(WeakReference) <br>
&ensp;&ensp;&ensp;&ensp;    
    弱引用与软引用的区别在于:只具有弱引用的对象拥有更短暂的生命周期。
在垃圾回收器线程扫描它所管辖的内存区域的过程中,一旦发现了只具有弱引
用的对象,不管当前内存空间足够与否,都会回收它的内存。不过,由于垃圾
回收器是一个优先级很低的线程,因此不一定会很快发现那些只具有弱引用的
对象。 <br>
&ensp;&ensp;&ensp;&ensp; 
    弱引用可以和一个引用队列(ReferenceQueue)联合使用,如果弱引用所
引用的对象被垃圾回收,Java 虚拟机就会把这个弱引用加入到与之关联的引用
队列中。 <br>
&ensp;&ensp;&ensp;&ensp; 
    (4)虚引用(PhantomReference) <br>
&ensp;&ensp;&ensp;&ensp; 
    “虚引用”顾名思义,就是形同虚设,与其他几种引用都不同,虚引用并不会
决定对象的生命周期。如果一个对象仅持有虚引用,那么它就和没有任何引用
一样,在任何时候都可能被垃圾回收器回收。 <br>
&ensp;&ensp;&ensp;&ensp; 
    虚引用主要用来跟踪对象被垃圾回收器回收的活动。虚引用与软引用和弱
引用的一个区别在于:虚引用必须和引用队列 (ReferenceQueue)联合使用。
当垃圾回收器准备回收一个对象时,如果发现它还有虚引用,就会在回收对象
的内存之前,把这个虚引用加入到与之关联的引用队列中。 <br>
ReferenceQueue queue = new ReferenceQueue (); <br>
PhantomReference pr = new PhantomReference (object, queue); <br>
&ensp;&ensp;&ensp;&ensp; 
    比较容易理解的是 Java 垃圾回收器会优先清理可达强度低的对象。 <br>
&ensp;&ensp;&ensp;&ensp;
    那现在问题来了,若一个对象的引用类型有多个,那到底如何判断它的可
达性呢?其实规则如下:(“单弱多强”) <br>
&ensp;&ensp;&ensp;&ensp;
1. 单条引用链的可达性以最弱的一个引用类型来决定; <br>
2. 多条引用链的可达性以最强的一个引用类型来决定; <br>
&ensp;&ensp;&ensp;&ensp;
    我们假设图 2 中引用1和3为强引用,5为软引用,7为弱引用,对于对
象 5 按照这两个判断原则,路径1-5取最弱的引用5,因此该路径对对象 5 的
引用为软引用。同样,3-7为弱引用。在这两条路径之间取最强的引用,于是
对象 5 是一个软可及对象。

### <a name="4">4. 说一下引用计数法与可达性分析算法</a>
&ensp;&ensp;&ensp;&ensp;
    参见《深入理解 java 虚拟机》。

*  扩展:GC 用的可达性分析算法中,哪些对象可作为 GC Roots 对象? <br>
    1.虚拟机栈中引用的对象。 <br>
    2.本地方法栈中引用的对象。 <br>
    3.方法区中静态成员或常量引用的对象。 <br>

&ensp;&ensp;&ensp;&ensp;
引用计数法与可达性分析算法。

### <a name="6">6. 堆里面的分区和各自的特点。</a>
* 年轻代: <br>
&ensp;&ensp;&ensp;&ensp;
年轻代又进一步可以划分为一个伊甸园(Eden)和两个存活区
(Survivor space),伊甸园是进行内存分配的地方,是一块连续的空闲内存区域,
在里面进行内存分配速度非常快,因为不需要进行可用内存块的查找。新对象
是总是在伊甸园中生成,只有经受住了一定的考验后才能后顺利地进入到存活
区中,这种考验是什么在后面会讲到。把存活区划分为两块,其实也是为了满
足垃圾回收的需要,因为在年轻代中经历了“回收大劫”未必就能够进入到年
老代中。系统总是把对象放在伊甸园和一个存活区(任意的一个),在垃圾回收时,
根据其存活时间被复制到另一个存活区或者年老代中,则之前的存活区和伊甸
园中剩下的都是需要被回收的对象,只对这两个区域进行清除即可,两个存活
区是交替使用,循环往复,在下一次垃圾回收时,之前被清除的存活区又用来
放置存活下来的对象了。一般来说,年轻代区域较小,而且大部分对象是需要
进行清除的,采用“复制算法”进行垃圾回收。
* 年老代: <br>
&ensp;&ensp;&ensp;&ensp;
在年轻代中经历了 N 次回收后仍然没有被清除的对象,就会被放
到年老代中,都是生命周期较长的对象。对于年老代和永久代,采用一种称为
“标记-清除-压缩(Mark-Sweep-Compact)”的算法。标记的过程是找出当前
还存活的对象,并进行标记;清除则是遍历整个年老区,找到已标记的对象并
进行清除;而压缩则是把存活的对象移动到整个内存区的一端,使得另一端是
一块连续的空间,方便进行内存分配和复制。

 (1) Minor GC: <br>
&ensp;&ensp;&ensp;&ensp;
    当新对象生成,但在Eden申请空间失败时就会触发 Minor GC,对 Enden 区
    进行 GC,清除掉非存活的对象,并且把存活的对象移动到 Survivor 区中的其
中一个区中。前面的提到考验就是 Minor GC,也就是说对象经过了 Minor
GC 才能
够进入到存活区中。这种形式的 GC 只会在年轻代中进行,因为大部分对象都是从 Eden
区开始的,同时 Eden 区不会分配得太大,所以对 Eden 区的 GC 会非常地频繁。

(2) Full GC: <br>
&ensp;&ensp;&ensp;&ensp;
    对整个对进行整理,包括了年轻代、年老代和持久代。Full GC 要对整个
块进行回收,所以要比 Minor GC 慢得多,因此应该尽可能减少 Full GC 的次数。

### <a name="7">7. Minor GC与Full GC分别在什么时候发生?</a>
&ensp;&ensp;&ensp;&ensp;
    如果 Eden 空间占满了, 会触发 minor GC。 Minor GC 后仍然存活的对
象会被复制到 S0 中去。这样 Eden 就被清空可以分配给新的对象。
又触发了一次 Minor GC , S0 和 Eden 中存活的对象被复制到 S1 中, 并且 S0
和 Eden 被清空。 在同一时刻, 只有 Eden 和一个 Survivor Space 同时被操作。
当每次对象从 Eden 复制到 Survivor Space 或者从 Survivor Space 中的一个复制
到另外一个,有一个计数器会自动增加值。 默认情况下如果复制发生超过 16次, 
JVM 会停止复制并把他们移到老年代中去。
如果一个对象不能在 Eden 中被创建,它会直接被创建在老年代中。 如果
老年代的空间被占满会触发老年代的 GC,也被称为 Full GC。Full GC 是一个
压缩处理过程,所以它比 Minor GC 要慢很多。

* 内存分配规则: <br>
    1.对象优先分配在 Eden 区,如果 Eden 区没有足够的空间时,虚拟机执行一次 Minor GC。<br>
    2.大对象直接进入老年代(大对象是指需要大量连续内存空间的对象)。这样做的目的是
    避免在 Eden 区和两个 Survivor 区之间发生大量的内存拷贝(新生代采用复制算法收集内存)。<br>
    3.长期存活的对象进入老年代。虚拟机为每个对象定义了一个年龄计数器,如果对象经过
    了 1 次 Minor GC 那么对象会进入 Survivor 区,之后每经过一次 Minor GC 那么对象
    的年龄加 1,直到达到阀值,对象进入老年区。 <br>
    4.动态判断对象的年龄。如果 Survivor 区中相同年龄的所有对象大小的总和大于
    Survivor 空间的一半,年龄大于或等于该年龄的对象可以直接进入老年代。 <br>
    5.空间分配担保。每次进行 Minor GC 时,JVM 会计算 Survivor 区移至老年区的对象的
    平均大小,如果这个值大于老年区的剩余值大小则进行一次 Full GC,如果小于检查
    HandlePromotionFailure 设置,如果 true 则只进行 Monitor GC,如果 false 则进
    行 Full GC。

### <a name="8">8. 对象创建方法,对象的内存布局,对象的访问定位。</a>
四种不同的方法创建 java 对象。<br>
1.用 new 语句创建对象,这是最常用的创建对象的方式。<br>
2.调用对象的 clone()方法。<br>
MyObject anotherObject = new MyObject();<br>
MyObject object = anotherObject.clone();<br>
使用 clone()方法克隆一个对象的步骤:<br>
1.被克隆的类要实现 Cloneable 接口。<br>
2.被克隆的类要重写 clone()方法。<br>


图图

* 扩展: <br>
&ensp;&ensp;&ensp;&ensp;
        原型模式主要用于对象的复制,实现一个接口(实现 Cloneable 接口),
    重写一个方法(重写 Object 类中的 clone 方法),即完成了原型模式。
    原型模式中的拷贝分为"浅拷贝"和"深拷贝":
    浅拷贝: 对值类型的成员变量进行值的复制,对引用类型的成员变量只复制
    引用,不复制引用的对象.
    深拷贝: 对值类型的成员变量进行值的复制,对引用类型的成员变量也进行
    引用对象的复制.
    (Object 类的 clone 方法只会拷贝对象中的基本数据类型的值,对于数组、
    容器对象、引用对象等都不会拷贝,这就是浅拷贝。如果要实现深拷贝,必须
    将原型模式中的数组、容器对象、引用对象等另行拷贝。)
    原型模式的优点。 <br>
    1.如果创建新的对象比较复杂时,可以利用原型模式简化对象的创建过程。 <br>
    2.使用原型模式创建对象比直接 new 一个对象在性能上要好的多,因为
    Object 类的 clone 方法是一个本地方法,它直接操作内存中的二进制流,特别
    是复制大对象时,性能的差别非常明显。
    原型模式的使用场景。
    因为以上优点,所以在需要重复地创建相似对象时可以考虑使用原型模式。
    比如需要在一个循环体内创建对象,假如对象创建过程比较复杂或者循环次数
    很多的话,使用原型模式不但可以简化创建过程,而且可以使系统的整体性能
    提高很多。 <br>
    3.运用反射手段, 使用 Class.forName()
    MyObject object = (MyObject) Class.forName("subin.rnd.MyObject
    ").newInstance();
    其他部分见“反射的原理”部分。
    4.运用反序列化手段,调用 java.io.ObjectInputStream 对象的
    readObject()方法。 <br>
    其余部分见“序列化和反序列化”部分。 <br>
    其余 2 问参见《深入理解 java 虚拟机》。 <br>

### <a name="9">9. 说一下几种垃圾收集算法的原理和特点,应用的场景。怎么优化复制算法?</a>
&ensp;&ensp;&ensp;&ensp;
    参见《深入理解 java 虚拟机》。
    &ensp;&ensp;&ensp;&ensp;
    优化复制算法:由于每次执行复制算法的时候,所有存活的对象都要被复
制,这样效率很低。由于程序中创建的大部分对象的生命周期都很短,只有一
部分对象有较长的生命周期,因此可以针对这个特点对复制算法进行优化,采
用分代垃圾回收算法。

### <a name="10">10. GC收集器有哪些?CMS收集器与G1收集器的特点。</a>
&ensp;&ensp;&ensp;&ensp;
    参见《深入理解 java 虚拟机》。

### <a name="11">11. 什么是内存泄露和内存溢出。</a>

图图

  &ensp;&ensp;&ensp;&ensp;
    内存泄漏的典型例子是一个没有重写 hashCode 和 equals 方法的 Key 类在
HashMap 中保存的情况,最后会生成很多重复的对象。所有的内存泄露最后都
会 抛 出OutOfMemoryError异 常 ( Exceptionjava.lang.OutOfMemoryError: Java heap space)。<br>

造成内存泄露的原因:

图图

*   内存泄露的解决方案(重要!!): <br>
    1、避免在循环中创建对象。 <br>
    2、尽早释放无用对象的引用。(最基本的建议) <br>
    3、尽量少用静态变量,因为静态变量存放在永久代(方法区),永久代基本不参与垃圾回收。 <br>
    4、使用字符串处理,避免使用 String,应大量使用 StringBuffer,每一个 String对象都得独立占用内存一块区域。
    
*   在实际场景中,你怎么查找内存泄露?<br>
    可以使用 Jconsole。
    
没有内存泄露的:

图图

造成内存泄露的:如果内存的大小持续地增长,则说明系统存在内存泄漏。

图图

*   内存溢出:指程序运行过程中无法申请到足够的内存而导致的一种错误。

*  内存溢出的几种情况(OOM 异常): <br>
    OutOfMemoryError 异常: <br>
    &ensp;&ensp;&ensp;&ensp;
    除了程序计数器外,虚拟机内存的其他几个运行时区域都有发生OutOfMemoryError(OOM)异常的可能。 <br>
    1.虚拟机栈和本地方法栈溢出 <br>
    &ensp;&ensp;&ensp;&ensp;
    如果线程请求的栈深度大于虚拟机所允许的最大深度,将抛出StackOverflowError 异常。 <br>
    &ensp;&ensp;&ensp;&ensp;
    如果虚拟机在扩展栈时无法申请到足够的内存空间,则抛出OutOfMemoryError 异常。 <br>
    2.堆 溢出 <br>
        &ensp;&ensp;&ensp;&ensp;
        一般的异常信息:java.lang.OutOfMemoryError:Java heap spaces。 <br>
        &ensp;&ensp;&ensp;&ensp;
        出现这种异常,一般手段是先通过内存映像分析工具(如 Eclipse Memory
    Analyzer)对 dump 出来的堆转存快照进行分析,重点是确认内存中的对象是否
    是必要的,先分清是因为内存泄漏(Memory Leak)还是内存溢出(MemoryOverflow)。 <br>
        &ensp;&ensp;&ensp;&ensp;
        如果是内存泄漏,可进一步通过工具查看泄漏对象到 GC Roots 的引用链。
    于是就能找到泄漏对象是通过怎样的路径与 GC Roots 相关联并导致垃圾收集器
    无法自动回收。 <br>
        &ensp;&ensp;&ensp;&ensp;
        如果不存在泄漏,那就应该检查虚拟机的参数(-Xmx 与-Xms)的设置是否适当。 <br>
    3.方法区溢出 <br>
        &ensp;&ensp;&ensp;&ensp;
        异常信息:java.lang.OutOfMemoryError:PermGen space。 <br>
    4.运行时常量池溢出 <br>
        &ensp;&ensp;&ensp;&ensp;
        异常信息:java.lang.OutOfMemoryError:PermGen space。 <br>
        &ensp;&ensp;&ensp;&ensp;
        如果要向运行时常量池中添加内容,最简单的做法就是使用
    String.intern()这个 Native 方法。该方法的作用是:如果池中已经包含一个
    等于此 String 的字符串,则返回代表池中这个字符串的 String 对象;否则,
    将此 String 对象包含的字符串添加到常量池中,并且返回此 String 对象的引
    用 。 由于常量池分配在方法区内, 我们可以通过-XX:PermSize 和
    -XX:MaxPermSize 限制方法区的大小,从而间接限制其中常量池的容量。
    
*  导致内存溢出的原因: <br>
    1.内存中加载的数据量过于庞大,如一次从数据库取出过多数据; <br>
    2.集合类中有对对象的引用,使用完后未清空,使得 JVM 不能回收; <br>
    3.代码中存在死循环或循环产生过多重复的对象实体; <br>
    4.启动参数内存值设定的过小。 <br>

*  内存溢出的解决方法: <br>
    第一步,修改 JVM 启动参数,直接增加内存。(-Xms,-Xmx 参数一定不要忘记加。 <br>
    一般要将-Xms 和-Xmx 选项设置为相同,以避免在每次 GC 后调整堆的大小;建议堆的最大值设置为可用内存的最大值的 80%)。
    第二步,检查错误日志,查看“OutOfMemory”错误前是否有其它异常或错误。 <br>
    第三步,对代码进行走查和分析,找出可能发生内存溢出的位置。 <br>
    第四步,使用内存查看工具动态查看内存使用情况(Jconsole)。

*  扩展:SOF 你遇到过哪些情况? <br>
    基本上如果抛出 OutOfMemory 有两种原因: <br>
    1.内存泄露。 <br>
    2.应用程序本身就是需要这么多的内存。 <br>

### <a name="12">12. 如何减少GC出现的次数(Java内存管理)。(重点!!!!)</a>
(1)对象不用时最好显式置为 Null <br>
    &ensp;&ensp;&ensp;&ensp;
    一般而言,为 Null 的对象都会被作为垃圾处理,所以将不用的对象显式地设
为 Null,有利于 GC 收集器判定垃圾,从而提高了 GC 的效率。 <br>
(2)尽量少用 System.gc() <br>
    &ensp;&ensp;&ensp;&ensp;
    此函数建议 JVM 进行主 GC,虽然只是建议而非一定,但很多情况下它会触发
主 GC,从而增加主 GC 的频率,也即增加了间歇性停顿的次数。 <br>
(3)尽量少用静态变量 <br>
    &ensp;&ensp;&ensp;&ensp;
    静态变量属于全局变量,不会被 GC 回收,它们会一直占用内存。 <br>
(4)尽量使用 StringBuffer,而不用 String 来累加字符串。 <br>
    &ensp;&ensp;&ensp;&ensp;
    由于 String 是固定长的字符串对象,累加 String 对象时,并非在一个 String
对象中扩增,而是重新创建新的 String 对象,如 Str5=Str1+Str2+Str3+Str4,这条
语句执行过程中会产生多个垃圾对象,因为对次作“+”操作时都必须创建新
的 String 对象,但这些过渡对象对系统来说是没有实际意义的,只会增加更多
的垃圾。避免这种情况可以改用 StringBuffer 来累加字符串,因 StringBuffer
是可变长的,它在原有基础上进行扩增,不会产生中间对象。 <br>
(5)分散对象创建或删除的时间 <br>
&ensp;&ensp;&ensp;&ensp;
    集中在短时间内大量创建新对象,特别是大对象,会导致突然需要大量内
存,JVM 在面临这种情况时,只能进行主 GC,以回收内存或整合内存碎片,从
而增加主 GC 的频率。 <br>
&ensp;&ensp;&ensp;&ensp;
    集中删除对象,道理也是一样的。它使得突然出现了大量的垃圾对象,空
闲空间必然减少,从而大大增加了下一次创建新对象时强制主 GC 的机会。 <br>
(6)尽量少用 finalize 函数。因为它会加大 GC 的工作量,因此尽量少用finalize 方式回收资源。 <br>
(7)如果需要使用经常用到的图片,可以使用软引用类型,它可以尽可能将图片保存在内存中,供程序调用,而不引起 OutOfMemory。 <br>
(8)能用基本类型如 int,long,就不用 Integer,Long 对象 <br>
&ensp;&ensp;&ensp;&ensp;
    基本类型变量占用的内存资源比相应包装类对象占用的少得多,如果没有必要,最好使用基本变量。 <br>
(9)增大-Xmx 的值。

### <a name="13">13. 数组多大放在JVM老年代?永久代对象如何GC?如果想不被GC怎么办?如果想在 GC 中生存 1 次怎么办?</a> 
  &ensp;&ensp;&ensp;&ensp;
    虚拟机提供了一个-XX:PretenureSizeThreshold 参数(通常是 3MB),
令大于这个设置值的对象直接在老年代分配。这样做的目的是避免在 Eden
区及两个 Survivor 区之间发生大量的内存复制(复习一下:新生代采用复制
算法收集内存)。 <br>
&ensp;&ensp;&ensp;&ensp;
    垃圾回收不会发生在永久代,如果永久代满了或者是超过了临界值,会
触发完全垃圾回收(FullGC)。如果仔细查看垃圾收集器的输出信息,就会发
现永久代也是被回收的。这就是为什么正确的永久代大小对避免 FullGC 是
非常重要的原因。 <br>
让对象实现 finalize()方法,一次对象的自我拯救。

### <a name="14">14. JVM 常见的启动参数。</a> 
   &ensp;&ensp;&ensp;&ensp;
    -Xms:设置堆的最小值。<br>
    &ensp;&ensp;&ensp;&ensp;
    -Xmx:设置堆的最大值。<br>
    &ensp;&ensp;&ensp;&ensp;
    -Xmn: 设置新生代的大小。<br>
    &ensp;&ensp;&ensp;&ensp;
    -Xss:设置每个线程的栈大小。<br>
    &ensp;&ensp;&ensp;&ensp;
    -XX:NewSize:设置新生代的初始值。<br>
    &ensp;&ensp;&ensp;&ensp;
    -XX:MaxNewSize :设置新生代的最大值。<br>
    &ensp;&ensp;&ensp;&ensp;
    -XX:PermSize:设置永久代的初始值。<br>
    &ensp;&ensp;&ensp;&ensp;
    -XX:MaxPermSize:设置永久代的最大值。<br>
    &ensp;&ensp;&ensp;&ensp;
    -XX:SurvivorRatio:年轻代中 Eden 区与 Survivor 区的大小比值。<br>
    &ensp;&ensp;&ensp;&ensp; 
    -XX:PretenureSizeThreshold: 令大于这个设置值的对象直接在老年代分配。<br>

### <a name="15">15. 说下几种常用的内存调试工具: jps、 jmap、 jhat、 jstack、 jconsole,jstat。</a> 
Java 内存泄露的问题调查定位:jmap,jstack 的使用等等。<br>
    &ensp;&ensp;&ensp;&ensp;
    jps: 查看虚拟机进程的状况,如进程 ID。<br>
    &ensp;&ensp;&ensp;&ensp;
    jmap: 用于生成堆转储快照文件(某一时刻的)。<br>
    &ensp;&ensp;&ensp;&ensp;
    jhat: 对生成的堆转储快照文件进行分析。<br>
    &ensp;&ensp;&ensp;&ensp;
    jstack: 用来生成线程快照(某一时刻的)。生成线程快照的主要目的是定位线程长时停顿的原因(如死锁,死循环,等待 I/O 等),
通过查看各个线程的调用堆栈,就可以知道没有响应的线程在后台做了什么或者等待什么资源。 <br>
    &ensp;&ensp;&ensp;&ensp;
    jstat: 虚拟机统计信息监视工具。如显示垃圾收集的情况,内存使用的情况。<br>
    &ensp;&ensp;&ensp;&ensp;
    Jconsole: 主要是内存监控和线程监控。内存监控:可以显示内存的使用情况。线程监控:遇到线程停顿时,可以使用这个功能。<br>

图图图

### <a name="16">16. 说下虚拟机的类加载机制。</a> 
参见《深入理解 java 虚拟机》。

### <a name="17">17. 说下双亲委派模型。双亲委派模型中有哪些方法。用户如何自定义类加载器 。怎么打破双亲委托机制?</a> 
参见《深入理解 java 虚拟机》。<br>
双亲委派模型中用到的方法:<br>
    &ensp;&ensp;&ensp;&ensp; 
    findLoadedClass(),<br>
    &ensp;&ensp;&ensp;&ensp; 
    loadClass()<br>
    &ensp;&ensp;&ensp;&ensp; 
    findBootstrapClassOrNull()<br>
    &ensp;&ensp;&ensp;&ensp; 
    findClass()<br>
    &ensp;&ensp;&ensp;&ensp; 
    defineClass():把二进制数据转换成字节码。<br>
    &ensp;&ensp;&ensp;&ensp; 
    resolveClass()<br>
自定义类加载器的方法:<br>
    &ensp;&ensp;&ensp;&ensp; 
    继承 ClassLoader 类,<br>
    &ensp;&ensp;&ensp;&ensp; 
    重写 findClass()方法。<br>

### <a name="18">18. 描述Java类加载器的工作原理及其组织结构。</a> 
Java 类加载器的作用就是在运行时加载类。<br>
Java 类加载器基于三个机制:委托性、可见性和单一性。<br>
    &ensp;&ensp;&ensp;&ensp; 
    (1) 委托机制是指双亲委派模型。当一个类加载和初始化的时候,类仅在有需
要加载的时候被加载。假设你有一个应用需要的类叫作 Abc.class,首先加载这
个类的请求由 Application 类加载器委托给它的父类加载器 Extension 类加载器,
然后再委托给 Bootstrap 类加载器。 Bootstrap 类加载器 会先看看 rt.jar 中有没有
这个类,因为并没有这个类,所以这个请求又回到 Extension 类加载器,它会查
看 jre/lib/ext 目录下有没有这个类,如果这个类被 Extension 类加载器找到了,
那么它将被加载,而 Application 类加载器不会加载这个类;而如果这个类没有
被 Extension 类加载器找到,那么再由 Application 类加载器从 classpath 中寻找,如果没找到,就会抛出异常。<br>
    &ensp;&ensp;&ensp;&ensp; 
    双亲委托机制的优点就是能够提高软件系统的安全性。因为在此机制下,
用户自定义的类加载器不可能加载本应该由父加载器加载的可靠类,从而防止
不可靠的恶意代码代替由父类加载器加载的可靠代码。如, java.lang.Object 类总
是由根类加载器加载的,其他任何用户自定义的类加载器都不可能加载含有恶
意代码的 java.lang.Object类。<br>
    &ensp;&ensp;&ensp;&ensp; 
    (2) 可见性原理是子类的加载器可以看见所有的父类加载器加载的类,而父类
加载器看不到子类加载器加载的类。<br>
    &ensp;&ensp;&ensp;&ensp; 
    (3) 单一性原理是指仅加载一个类一次,这是由委托机制确保子类加载器不会
再次加载父类加载器加载过的类。
    &ensp;&ensp;&ensp;&ensp; 
    Java 的类加载器有三个,对应 Java 的三种类:<br>
    &ensp;&ensp;&ensp;&ensp; 
    Bootstrap Loader // 负责加载系统类 (指的是内置类,像 String)<br>
    &ensp;&ensp;&ensp;&ensp; 
    |
    &ensp;&ensp;&ensp;&ensp; 
    -- ExtClassLoader //负责加载扩展类(就是继承类和实现类)<br>
    &ensp;&ensp;&ensp;&ensp; 
    |
    &ensp;&ensp;&ensp;&ensp; 
    -- AppClassLoader //负责加载应用类(程序员自定义的类)<br>
    &ensp;&ensp;&ensp;&ensp; 
    Java 提供了显式加载类的 API:Class.forName(classname)。

### <a name="21">21. Java编译的过程。</a> 
见《深入理解 java 虚拟机》。P304

### <a name="22">22. class文件是什么类型文件(字节码文件的格式)?</a> 
参见《深入理解 java 虚拟机》。

### <a name="23">23. 即时编译器的优化方法。</a> 

参见《深入理解 java 虚拟机》。P345

### <a name="24">24.静态分派与动态分派。</a> 
参见《深入理解 java 虚拟机》。 P246

### <a name="25">25. 编译阶段对程序做了哪些优化?</a> 
编译期其实是个“不确定”的操作过程,它既可能指的是前端编译器的编译过程,也可能指的是后端运行期编译器的编译过程。<br>
详细参见《深入理解 java虚拟机》。

### <a name="26">26. new 的对象如何不分配在堆而分配在栈上?</a> 
方法逃逸。
