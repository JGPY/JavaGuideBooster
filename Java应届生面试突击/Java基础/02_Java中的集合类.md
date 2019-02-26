# Java中的集合类

### 目录

---
<a href="#1">1. ArrayList、LinkedList、Vector的区别和实现原理。</a> <br>
<a href="#2">2. HashMap、HashTable、LindedHashMap、ConcurrentHashMap、WeakHashMap的区别和实现原理。</a> <br>
<a href="#3">3. 讲一下集合中的fail-fast机制。</a> <br>
<a href="#4">4. 介绍一下Java中的集合框架?</a> <br>
<a href="#5">5. Collection包结构与Collections的区别。</a> <br>


### <a name="1">1. ArrayList、LinkedList、Vector的区别和实现原理。</a>
&ensp;&ensp;&ensp;&ensp; 
    ArrayList 和 Vector 只能按顺序存储元素(从下标为 0 的位置开始),删除元素的时
候,需要移位并置空,**默认初始容量都是 10。** <br>
&ensp;&ensp;&ensp;&ensp; 
    ArrayList 和 Vector 基于数组实现的,LinkedList 基于**双向循环链表**实现的(含有头结点)。
* 一.线程安全性 <br>
&ensp;&ensp;&ensp;&ensp; 
    ArrayList 不具有线程安全性,用在单线程环境中。LinkedList 也是线程不安全的,**如
果在并发环境下使用它们**, 可 以 用 Colletions 类 中 的 静 态 方 法 **synchronizedList()** 对
ArrayList 和 LinkedList 进行调用即可。
&ensp;&ensp;&ensp;&ensp; 
    **Vector 是线程安全的**,即它的大部分方法都包含有关键字 synchronized。Vector 的效
率没有 ArrayList 和 LinkedList 高。
* 二.扩容机制 <br>
&ensp;&ensp;&ensp;&ensp; 
    从内部实现机制来讲,ArrayList 和 Vector 都是使用 Objec 的数组形式来存储的。当你
向这两种类型中增加元素的时候,若容量不够,需要进行扩容。ArrayList 扩容后的容量是
之前的 **1.5** 倍,然后,把之前的数据拷贝到新建的数组。Vector 默认情况下扩容后的容量
是之前的 **2** 倍。 <br>
&ensp;&ensp;&ensp;&ensp;
    Vector 可以**设置容量增量**,而 ArrayList 不可以。在 Vector 中有 capacityIncrement:
向量的大小大于其容量时, 容量自动增加的量。 如果在创建 Vector 时 , 指定了
capacityIncrement 的大小;则每次当 Vector 中动态数组容量需要增加时,如果**容量的增量
大于零**,增加的大小都是 capacityIncrement。如果**容量的增量小于等于零**,则每次需要增
大容量时,向量的容量将增大为之前的 2 倍。 <br>
&ensp;&ensp;&ensp;&ensp;
    可变长度数组的原理:当元素个数超过数组的长度时,会产生一个新数组,将原数组
的数据复制到新数组,再将新的元素添加到新数组中。 <br>
* 三.增删查改的效率 <br>
&ensp;&ensp;&ensp;&ensp;
    ArrayList 和 Vector 中,**从指定的位置(用 index)检索一个对象,或在集合的末尾插
入、删除一个对象的时间是一样的,可表示为 O(1)**。但是,如果在集合的其他位置增加或
移除元素那么花费的时间是 O(n)。LinkedList 中,在插入、删除集合中任何位置的元素
所花费的时间都是一样的—O(1),但它在索引一个元素的时候比较慢 O(n)。 <br>
&ensp;&ensp;&ensp;&ensp;
    所以,如果只是查找特定位置的元素或只在集合的末端增加、移除元素,那么使用
Vector 或 ArrayList 都可以。如果是对其它**指定位置的插入、删除操作**,最好选择 LinkedList。

### <a name="2">2. HashMap、HashTable、LindedHashMap、ConcurrentHashMap、WeakHashMap的区别和实现原理。</a>
* 一.HashMap VS HashTable <br>
    1.首先说下 HashMap 的原理。 <br>
![图02_2_1](/data/images/Java应届生面试突击/Java基础/02_2_1.png) <br>
![图02_2_2](/data/images/Java应届生面试突击/Java基础/02_2_2.png) <br>
**HashMap 的数据结构** <br>
![图02_2_3](/data/images/Java应届生面试突击/Java基础/02_2_3.png) <br>
**HashMap 存储函数的实现 put(K key, V value):** <br>
&ensp;&ensp;&ensp;&ensp;
    根据下面 put 方法的源代码可以看出,当程序试图将一个 key-value 对放入 HashMap
中时,程序首先计算该 key 的 hashCode() 值,然后对该哈希码值进行再哈希,然后把哈
希值和(数组长度-1)进行按位与操作,得到存储的数组下标,如果该位置处没有链表节
点,那么就直接把包含<key,value>的节点放入该位置。如果该位置有结点,就对链表进行
遍历,看是否有 hash, key 和要放入的节点相同的节点,如果有的话,就替换该节点的 value
值,如果没有相同的话,就创建节点放入值,并把该节点插入到链表表头(头插法)。 <br>
![图02_2_4](/data/images/Java应届生面试突击/Java基础/02_2_4.png) <br>
![图02_2_5](/data/images/Java应届生面试突击/Java基础/02_2_5.png) <br>
    void resize(int newCapacity) {
        Entry[] oldTable = table;
        int oldCapacity = oldTable.length;
        if (oldCapacity == MAXIMUM_CAPACITY) {
            threshold = Integer.MAX_VALUE;
            return;
        }
        Entry[] newTable = new Entry[newCapacity];//新创建一个数组
        transfer(newTable);
        table = newTable;
        threshold = (int) (newCapacity * loadFactor);
    }
    
    void transfer(Entry[] newTable) {
        Entry[] src = table;
        int newCapacity = newTable.length;
        for (int j = 0; j < src.length; j++) {
            Entry<K, V> e = src[j];
            if (e != null) {
                src[j] = null;
                do {
                    //过程(1)
                    Entry<K, V> next = e.next;
                    int i = indexFor(e.hash, newCapacity);
                    e.next = newTable[i];
                    newTable[i] = e;
                    e = next;
                } while (e != null);
            }
        }
    }
    
    static int indexFor(int h, int length) {
        return h & (length-1);
    }
    
    static int hash(int h) {
        h ^= (h >>> 20) ^ (h >>> 12);
        return h ^ (h >>> 7) ^ (h >>> 4);    
    }
    
&ensp;&ensp;&ensp;&ensp;    
    再哈希,其目的是为了减少哈希冲突,使元素能够均匀的分布在数组上,从而提高数
组的存取效率。 <br>
**扩展:为何数组的长度是 2 的 n 次方呢?**
&ensp;&ensp;&ensp;&ensp;
    1. 这 个 方 法 非 常 巧 妙 , 它 通 过 h & (table.length -1) 来 得 到 该 对 象 的 保 存 位 , 而
HashMap 底层**数组的长度总是 2 的 n 次方**,2 n -1 得到的二进制数的每个位上的值都为 1,
那么与全部为 1 的一个数进行与操作,速度会大大提升。 <br>
&ensp;&ensp;&ensp;&ensp;
    2.当 length 总是 2 的 n 次方时,h& (length-1)运算等价于对 length 取模,也就是
h%length,**但是&比%具有更高的效率**。 <br>
&ensp;&ensp;&ensp;&ensp;
    3.当数组长度为 2 的 n 次幂的时候,**不同的 key 算得的 index 相同的几率较小**,那么
数据在数组上分布就比较均匀,也就是说**碰撞的几率小**,相对的,查询的时候就不用遍历
某个位置上的链表,这样**查询效率也就较高了**。 <br>

**HashMap 读取函数的实现 get(Object key):** <br>
![图02_2_7](/data/images/Java应届生面试突击/Java基础/02_2_7.png) <br>
&ensp;&ensp;&ensp;&ensp;
    hashMap 的 get 方法,是首先通过 key 的两次 hash 后的值与数组的长度-1 进行与操
作,定位到数组的某个位置,然后对该列的链表进行遍历,一般情况下,hashMap 的这种查
找速度是非常快的,hash 值相同的元素过多,就会造成链表中数据很多,而链表中的数据
查找是通过遍历所有链表中的元素进行的,这可能会影响到查找速度,找到即返回。特别
注意: 当返回为 null 时,你不能判断是没有找到指定元素,还是在 hashmap
中存着一个 value 为 null 的元素,因为 hashmap 允许 value 为 null. <br>
**HashMap 的扩容机制:** <br>
&ensp;&ensp;&ensp;&ensp;
    当 HashMap 中的结点个数超过数组大小*loadFactor(加载因子)时,就会进行数组
扩容, loadFactor 的默认值为 0.75。也就是说,默认情况下,数组大小为 16,那么当 HashMap
中结点个数超过 16*0.75=12 的时候,就把数组的大小扩展为 2*16=32,即扩大一倍,然后
重新计算每个元素在数组中的位置,并放进去,而这是一个非常消耗性能的操作。
多线程下 HashMap 出现的问题: <br>
&ensp;&ensp;&ensp;&ensp;
    1.多线程 put 操作后,get 操作导致死循环,导致 cpu100%的现象。主要是多线程同时
put 时,如果同时触发了 rehash 操作,会导致扩容后的 HashMap 中的链表中出现循环节
点,进而使得后面 get 的时候,会死循环。 <br>
&ensp;&ensp;&ensp;&ensp;
    2.多线程 put 操作,导致元素丢失,也是发生在多个线程对 hashmap 扩容时。 <br>
    
* 2.hashTable 的原理。 <br>
&ensp;&ensp;&ensp;&ensp;
    它的原理和 hashMap 基本一致。 <br>
* 3.HashMap 和 HashTable 的区别。 <br>
&ensp;&ensp;&ensp;&ensp;
    1. Hashtable 是线程安全的,方法是 Synchronized 的,适合在多线程环境中使用,效率
稍低;HashMap 不是线程安全的,方法不是 Synchronized 的,效率稍高,适合在单线程环
境下使用, 所以在多线程场合下使用的话, 需要手动同步 HashMap, <br>
**Collections.synchronizedMap()。** <br>
    **PS:HashTable 的效率比较低的原因?** <br>
&ensp;&ensp;&ensp;&ensp;
    在线程竞争激烈的情况下 HashTable 的效率非常低下。 因为当一个线程访问
HashTable 的同步方法时,访问其他同步方法的线程就可能会进入阻塞或者轮训状态。如
线程 1 使用 put 进行添加元素,线程 2 不但不能使用 put 方法添加元素,并且也不能使用
get 方法来获取元素,所以竞争越激烈效率越低。 <br>
&ensp;&ensp;&ensp;&ensp;
    2.HashMap 的 key 和 value 都可以为 null 值,HashTable 的 key 和 value 都不允许
有 Null 值。 <br>
&ensp;&ensp;&ensp;&ensp;
    3.HashMap 中数组的默认大小是 16,而且一定是 2 的倍数,扩容后的数组长度是之
前数组长度的 2 倍。HashTable 中数组默认大小是 11,扩容后的数组长度是之前数组长度
的 2 倍+1。 <br>
&ensp;&ensp;&ensp;&ensp;
    4.哈希值的使用不同。 <br>
而 HashMap 重新计算 hash 值,而且**用&代替求模**: <br>


    int hash = hash(key.hashcode());
    
    int i = indexFor(hash, table.length);
    
    static int hash(Object x) {
        int h = x.hashCode();
        h += ~(h << 9);
        h ^= (h >>> 14);
        h += (h << 4);
        h ^= (h >>> 10);
        return h;
    }
    
    static int indexFor(int h, int length) {
        return h & (length-1); //hashmap 的表长永远是 2^n。
    }
    
    HashTable 直接使用对象的 hashCode 值:
    int hash = key.hashCode();
    //注意区分 2 者的 hash 值!!
    int index = (hash & 0x7FFFFFFF) % tab.length;

&ensp;&ensp;&ensp;&ensp;
    5.判断是否含有某个键 <br>
&ensp;&ensp;&ensp;&ensp;
    在 HashMap 中,null 可以作为键,这样的键只有一个;可以有一个或多个键所对
应的值为 null。当 get()方法返回 null 值时,既可以表示 HashMap 中没有该键,也可
以表示该键所对应的值为 null。因此,在 HashMap 中不能用 get()方法来判断 HashM
ap 中是否存在某个键,而应该用 containsKey()方法来判断。Hashtable 的键值都不能
为 null,所以可以用 get()方法来判断是否含有某个键。

* 二.ConcurrentHashMap 的原理。 <br>
&ensp;&ensp;&ensp;&ensp;
    在 ConcurrentHashMap 中,不允许用 null 作为键和值。 <br>
&ensp;&ensp;&ensp;&ensp;
    ConcurrentHashMap 使用分段锁技术,将数据分成一段一段的存储,然后
给每一段数据配一把锁,当一个线程占用锁访问其中一个段数据的时候,其他
段的数据也能被其他线程访问,能够实现真正的并发访问。读操作大部分时候
都不需要用到锁。只有在 size 等操作时才需要锁住整个 hash 表。 <br>
&ensp;&ensp;&ensp;&ensp;
    它把区间按照并发级别(concurrentLevel),分成了若干个 segment。默认情
况下内部按并发级别为 16 来创建。对于每个 segment 的容量,默认情况也是
16。当然并发级别(concurrentLevel)和每个段(segment)的初始容量都是可以通
过构造函数设定的。ConcurrentHashMap 使用 segment 来分段和管理锁,
segment 继 承 自 ReentrantLock , 因 此 ConcurrentHashMap 使 用
ReentrantLock 来保证线程安全。 <br>
&ensp;&ensp;&ensp;&ensp;
    创建好默认的 ConcurrentHashMap 之后,它的结构大致如下图: <br>
    
![图02_2_8](/data/images/Java应届生面试突击/Java基础/02_2_8.png) <br>
![图02_2_9](/data/images/Java应届生面试突击/Java基础/02_2_9.png) <br>
![图02_2_10](/data/images/Java应届生面试突击/Java基础/02_2_10.png) <br>
&ensp;&ensp;&ensp;&ensp;
    可以看到除了 value 不是 final 的,其它值都是 final 的,这意味着不能从
hash 链的中间或尾部添加或删除节点,因为这需要修改 next 引用值,所有的节
点的修改只能从头部开始。为了确保读操作能够看到最新的值,将 value 设置成
volatile,这避免了加锁。 <br>

&ensp;&ensp;&ensp;&ensp;
    **1.get(Object key)的实现** <br>
![图02_2_11](/data/images/Java应届生面试突击/Java基础/02_2_11.png) <br>
&ensp;&ensp;&ensp;&ensp;
    get 操作的高效之处在于整个 get 过程不需要加锁,**除非读到的值是空的才
会加锁重读**。<br>
&ensp;&ensp;&ensp;&ensp;
    之所以不会读到过期的值,是根据 java 内存模型的 happen before 原则,
**对 volatile 字段的写入操作先于读操作,即使两个线程同时修改和获取 volatile
变量,get 操作也能拿到最新的值**,这是**用 volatile 替换锁**的经典应用场景。

&ensp;&ensp;&ensp;&ensp;
    **2.put(K key,V value)的实现--用 lock 加锁** <br>
首先,根据 key 计算出对应的 hash 值: <br>
**清单 4.Put 方法的实现** <br>
![图02_2_12](/data/images/Java应届生面试突击/Java基础/02_2_12.png) <br>
然后,根据 hash 值找到对应的 Segment 对象: <br>
**清单 5.根据 hash 值找到对应的 Segment** <br>
![图02_2_13](/data/images/Java应届生面试突击/Java基础/02_2_13.png) <br>
最后,在这个 Segment 中执行具体的 put 操作: <br>
**清单 6.在 Segment 中执行具体的 put 操作** <br>
![图02_2_14](/data/images/Java应届生面试突击/Java基础/02_2_14.png) <br>
&ensp;&ensp;&ensp;&ensp;
    插入操作需要经历两个步骤,第一步判断是否需要对 Segment 里的
HashEntry 数组进行扩容,第二步定位添加元素的位置然后放在 HashEntry 数
组里。 <br>
&ensp;&ensp;&ensp;&ensp;
    **是否需要扩容。在插入元素前**会先判断 Segment 里的 HashEntry 数组是否
超过容量(threshold),如果超过阀值,数组进行扩容。值得一提的是, **Segment
的扩容判断比 HashMap 更恰当,因为 HashMap 是在插入元素后判断元素是
否已经到达容量的**,如果到达了就进行扩容,但是很有可能扩容之后没有新元
素插入,这时 HashMap 就进行了一次无效的扩容。 <br>
    **如何扩容**。扩容的时候首先会创建一个两倍于原容量的数组,然后将原数
组里的元素进行再 hash 后插入到新的数组里。 <br>
------------------------------------------------------------------------------------
&ensp;&ensp;&ensp;&ensp;
    注意:这里的加锁操作是针对某个具体的 Segment,锁定的是该 Segment
而不是整个 ConcurrentHashMap。因为插入键 / 值对操作只是在这个
Segment 包含的某个桶中完成,不需要锁定整个 ConcurrentHashMap。此时,
其他写线程对另外 15 个 Segment 的加锁并不会因为当前线程对这个
Segment 的加锁而阻塞。同时,所有读线程几乎不会因本线程的加锁而阻塞(***除
非读线程刚好读到这个 Segment 中某个 HashEntry 的 value 域的值为
null,此时需要加锁后重新读取该值**)。 <br>
&ensp;&ensp;&ensp;&ensp;
    空值的唯一源头就是 HashEntry 中的默认值,因为 HashEntry 中的 value
不是 final 的,非同步读取有可能读取到空值。仔细看下 put 操作的语句:
**tab[index] = new HashEntry<K,V>(key, hash, first, value),在这条语句中,
HashEntry 构造函数中对 value 的赋值以及对 tab[index]的赋值可能被重新排
序,这就可能导致结点的值为空**。这种情况应当很罕见,一旦发生这种情况,
ConcurrentHashMap 采取的方式是在持有锁的情况下再读一遍,这能够保证读
到最新的值,并且一定不会为空值。(newEntry 对象是通过 new HashEntry(K
k , V v, HashEntry next) 来创建的。如果另一个线程刚好 new 这个对象时,当
前线程来 get 它。因为没有同步,就可能会出现当前线程得到的 newEntry 对象
是一个没有完全构造好的对象引用。这里同样有可能一个线程 new 这个对象的
时候还没有执行完构造函数就被另一个线程得到这个对象引用。) <br>
&ensp;&ensp;&ensp;&ensp;
    由于 HashEntry 的 next 域为 final 型,所以新节点只能在链表的表头处
插入。下图是在一个空桶中依次插入 A,B,C 三个 HashEntry 对象后的结构
图: <br>
**图 1. 插入三个节点后桶的结构示意图:** <br>
![图02_2_15](/data/images/Java应届生面试突击/Java基础/02_2_15.png) <br>
&ensp;&ensp;&ensp;&ensp;
    注意:由于只能在表头插入,所以链表中节点的顺序和插入的顺序相反。 <br>
    **3.remove(Object key)的实现** <br>
&ensp;&ensp;&ensp;&ensp;
    下面来分析 remove 操作,先让我们来看看 remove 操作的源代码实现。 <br> 
![图02_2_15](/data/images/Java应届生面试突击/Java基础/02_2_16.png) <br>
![图02_2_15](/data/images/Java应届生面试突击/Java基础/02_2_17.png) <br>  
&ensp;&ensp;&ensp;&ensp;  
    首先根据散列码找到具体的链表,然后遍历这个链表找到要删除的节点;
最后把待删除节点之后的所有节点原样保留在新链表中,把待删除节点之前的
每个节点克隆到新链表中。下面通过图例来说明 remove 操作。假设写线程执
行 remove 操作,要删除链表的 C 节点,另一个读线程同时正在遍历这个链
表。 <br>
 
图 4. 执行删除之前的原链表: <br>
![图02_2_15](/data/images/Java应届生面试突击/Java基础/02_2_18.png) <br>
图 5. 执行删除之后的新链表 <br>
![图02_2_15](/data/images/Java应届生面试突击/Java基础/02_2_19.png) <br>
&ensp;&ensp;&ensp;&ensp;
    从上图可以看出,节点 C 之后的所有节点原样保留到新链表中;删除节点
C 之前的每个节点被克隆到新链表中,注意:它们在新链表中的链接顺序被反
转了。 <br>
&ensp;&ensp;&ensp;&ensp;
    在执行 remove 操作时,原始链表并没有被修改,也就是说:读线程不会
受同时执行 remove 操作的并发写线程的干扰。 <br>
&ensp;&ensp;&ensp;&ensp;
    综合上面的分析我们可以看出,写线程对某个链表的结构性修改不会影响
其他的并发读线程对这个链表的遍历访问。 <br>

用 HashEntry 对象的不变性来降低读操作对加锁的需求 <br>
&ensp;&ensp;&ensp;&ensp;
    HashEntry 类的 value 域被声明为 Volatile 型,Java 的内存模型可以保
证:某个写线程对 value 域的写入马上可以被后续的某个读线程“看”到。在
ConcurrentHashMap 中,不允许用 Null 作为键和值,当读线程读到某个
HashEntry 的 value 域的值为 null 时,便知道产生了冲突——发生了重排序
现象,需要加锁后重新读入这个 value 值。这些特性互相配合,使得读线程即
使在不加锁状态下,也能正确访问 ConcurrentHashMap。 <br>
&ensp;&ensp;&ensp;&ensp;
    下面分别来分析线程写入的两种情形:对散列表做非结构性修改的操作和
对散列表做结构性修改的操作。 <br>
&ensp;&ensp;&ensp;&ensp;
    非结构性修改操作只是更改某个 HashEntry 的 value 域的值。由于对
Volatile 变量的写入操作将与随后对这个变量的读操作进行同步。当一个写线
程修改了某个 HashEntry 的 value 域后,另一个读线程读这个值域, Java 内
存模型能够保证读线程读取的一定是更新后的值。所以,写线程对链表的非结
构性修改能够被后续不加锁的读线程“看到”。 <br>
&ensp;&ensp;&ensp;&ensp;
    结构性修改,实质上是对某个桶指向的链表做结构性修改。如果能够确保:
在读线程遍历一个链表期间,写线程对这个链表所做的结构性修改不影响读线
程继续正常遍历这个链表。那么读 / 写线程之间就可以安全并发访问这个
ConcurrentHashMap。 <br>
&ensp;&ensp;&ensp;&ensp;
    从上面的代码清单“在 Segment 中执行具体的 put 操作”中,我们可以看
出:put 操作如果需要插入一个新节点到链表中时 , 会在链表头部插入这个新
节点。此时,链表中的原有节点的链接并没有被修改。也就是说:插入新健 / 值
对到链表中的操作不会影响读线程正常遍历这个链表。 <br>

ConcurrentHashMap 的高并发性主要来自于三个方面: <br>
&ensp;&ensp;&ensp;&ensp;
    1.用分离锁实现多个线程间的更深层次的共享访问。 <br>
&ensp;&ensp;&ensp;&ensp;
    2.用 HashEntry 对象的不变性来降低执行读操作的线程在遍历链表期间对
加锁的需求。 <br>
&ensp;&ensp;&ensp;&ensp;
    3.通过对同一个 Volatile 变量的写 / 读访问,协调不同线程间读 / 写操作
的内存可见性。 <br>
&ensp;&ensp;&ensp;&ensp;
    通过 HashEntry 对象的不变性及对同一个 Volatile 变量的读 / 写来协调
内存可见性,使得读操作大多数时候不需要加锁就能成功获取到需要的值。 <br>

ConcurrentHashMap 存在的问题? <br>
&ensp;&ensp;&ensp;&ensp;
    弱一致性的。 <br>
    
**三.WeakHashMap VS HashMap** <br>
&ensp;&ensp;&ensp;&ensp;
    WeakHashMap 中的 key 采用的是“弱引用”的方式,只要 WeakHashMap
中的 key 不再被外部引用,所对应的键值对就可以被垃圾回收器回收。 <br>
&ensp;&ensp;&ensp;&ensp;
    HashMap 中的 key 采用的是“强引用”的方式,当 key 不再被外部引用
时,只有当这个 key 从 HashMap 中删除后,才可以被垃圾回收器回收。 <br>

**HashMap 和 TreeMap 区别: <br>
1.实现方式的区别: <br>
HashMap:基于哈希表实现。TreeMap:基于红黑树实现。 <br>
2.TreeMap 能够把它保存的记录根据键排序. <br>
3.HashMap:适用于在 Map 中插入、删除和查找元素。 <br>
Treemap:适用于按自然顺序或自定义顺序遍历键(key)。 <br>
HashMap 通常比 TreeMap 快一点。** <br>

**Hashset 的实现原理**。 <br>
&ensp;&ensp;&ensp;&ensp;
    对于 HashSet 而言,它是基于 HashMap 实现的,HashSet 底层使用
HashMap 来保存所有元素,因此 HashSet 的实现比较简单,相关 HashSet 的
操作,基本上都是直接调用底层 HashMap 的相关方法来完成。 HashSet 中的元
素都存放在 HashMap 的 key 上面,而 value 中的值都是统一的一个 
private static final Object PRESENT = new Object(); <br>
 
    
    // 底层使用 HashMap 来保存 HashSet 中所有元素。
    private transient HashMap<E,Object> map;
    // 定义一个虚拟的 Object 对象作为 HashMap 的 value,将此对象定义为
    static final。
    private static final Object PRESENT = new Object();
    /*
    * 默认的无参构造器,构造一个空的 HashSet。
    * 实际底层会初始化一个空的 HashMap,并使用默认初始容量为 16 和加载
    因子 0.75 */

    public HashSet() {
        map = new HashMap<E,Object>();
    }
    
    public boolean add(E e) {
        return map.put(e, PRESENT)==null;
    }

### <a name="3">3. 讲一下集合中的fail-fast机制。</a>
&ensp;&ensp;&ensp;&ensp;
    例如:假设存在两个线程(线程 1、线程 2),线程 1 通过 Iterator 在遍历
集合 A 中的元素,在某个时候线程 2 修改了集合 A 的结构(是结构上面的修改,
而不是简单的修改集合元素的内容),那么这个时候程序就会抛出
ConcurrentModificationException 异常,从而产生 fail-fast 机制。
&ensp;&ensp;&ensp;&ensp;
    产生的原因:
&ensp;&ensp;&ensp;&ensp;
    当调用容器的 iterator()方法返回 Iterater 对象时,把容器中包含对象
的个数赋值给了一个变量 expectedModCount,在调用 next()方法时,会比较
expectedModCount 与容器中实际对象的个数是否相等,若二者不相等,则会抛
出 ConcurrentModificationException 异常。
    如果在遍历集合的同时,需要删除元素的话,可以用 iterator 里面的
remove()方法删除元素。

### <a name="4">4. 介绍一下Java中的集合框架?</a>

![图02_4_1](/data/images/Java应届生面试突击/Java基础/02_4_1.png)

### <a name="5">5. Collection包结构与Collections的区别。</a>
集合框架:Collection:List 列表 ,Set 集 <br>
Map:Hashtable,HashMap,TreeMap <br>

List 元素是有序的、可重复。 <br>
List 接口中常用类 <br>
    Vector :线程安全,但速度慢,已被 ArrayList 替代。底层数据结构是数组 <br>
    ArrayList :线程不安全,查询速度快。底层数据结构是数组 <br>
    LinkedList :线程不安全。增删速度快。底层数据结构是链表 <br>
    
Set(集)元素无序的、不可重复。
&ensp;&ensp;&ensp;&ensp;
    取出元素的方法只有迭代器。不可以存放重复元素,元素存取是无序的。因此存入
Set 中的每个对象都必须重写 equals()和 hashCode()方法来确保对象的唯一性。

Set 接口中常用的类 <br>
    HashSet :线程不安全,存取速度快。 <br>
    它是如何保证元素唯一性的呢?依赖的是元素的 hashCode 方法和 euqals 方法。 <br>
    TreeSet :线程不安全,可以对 Set 集合中的元素进行排序。TreeSet 底层数据结构是二叉树。 <br>
&ensp;&ensp;&ensp;&ensp;
    它的排序是如何进行的呢?通过 compareTo 或者 compare 方法来保证元素的有
序性。元素是以二叉树的形式存放的。

Map 是一个双列集合 <br>
|-- Hashtable :线程安全,速度慢。底层是哈希表数据结构。是**同步**的。
不允许 null 作为键,null 作为值。**(当用自定义类型对象作为 HashTable 的
key 时,需要重新改写该对象的 equals()和 hashCode()方法来确保 key 的唯一性)**。 <br>
|-- Properties :用于配置文件的定义和操作,使用频率非常高,同时键和值都
是字符串,**线程安全类**。 <br>
|-- HashMap :线程不安全,速度快。底层也是哈希表数据结构。是**不同步**的。 
允许 null 作为键,null 作为值。替代了 Hashtable。(当用自定义类型对象
作为 HashMap 的 key 时,需要重新改写该对象的 equals()和 hashCode()方法来确保 key
的唯一性)。 <br>
|-- LinkedHashMap : 可以保证 HashMap 集合**有序。存入的顺序和取出的顺序一致**。 <br>
|-- TreeMap :可以用来对 Map 集合中的**键进行排序**。 <br>

* Collection 和 Collections 的区别: <br>
*Collection 是集合类的上级接口*,子接口主要有 Set 和 List。 <br>
Collections 是针对集合类的一个帮助类,*提供了操作集合的工具方法*:一系列**静态方法**
实现对各种集合的**搜索、排序、线程安全化**等操作。

