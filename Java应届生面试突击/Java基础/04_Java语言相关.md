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

### <a name="2">2. instanceof 关键字的作用。</a>

### <a name="3">3. strictfp 关键字的作用。</a>
### <a name="4">4. 什么是不可变类?</a>
### <a name="5">5. Java 中的基本数据类型占据几个字节?</a>
### <a name="6">6. 运算符的优先级。</a>
### <a name="7">7. 强制类型转换时的规则有哪些。</a>
### <a name="8">8. 数组初始化时需要注意的问题。</a>
### <a name="9">9. 如何在 main()方法执行前输出“Hello world”?</a>
### <a name="10">10. Java 程序初始化的顺序(对象实例化的过程)。</a>
### <a name="11">11. 构造函数的特点。</a>
### <a name="12">12. 序列化与反序列化。</a>
### <a name="13">13. Switch 能否用 string 做参数?</a>
### <a name="14">14. equals 与==的区别。</a>
### <a name="15">15. Hashcode 的作用。</a>
### <a name="16">16. hashCode() 与 equals() 生成算法、方法怎么重写。</a>
### <a name="17">17. Object 有哪些公用方法?</a>
### <a name="18">18. String、StringBuffer 与 StringBuilder 的区别。</a>
### <a name="19">19. try catch finally,try 里有 return,finally 还执行么?如果会的话,什么时候执行,在 return 之前还是 return 之后?</a>
### <a name="20">20. 说下异常的原理。</a>
### <a name="21">21. Java 面向对象的三个特征与含义。</a>
### <a name="22">22. java 多态的实现原理(实现机制)。</a>
### <a name="23">23. Override(覆盖、重写)和 Overload(重载)的区别。</a>
### <a name="24">24. 接口与抽象类的区别。</a>
### <a name="25">25. 静态内部类和非静态内部类的区别。</a>
### <a name="26">26. static 的使用方式。</a>
### <a name="27">27. 反射的作用与原理。如何提高反射效率?</a>
### <a name="28">28. Java 和 C++/C 的区别,JAVA 的优点。</a>
### <a name="29">29. 同一个.java 文件中是否可以有多个 main()方法?</a>
### <a name="30">30. JAVA 中的类和成员的访问控制。</a>
### <a name="31">31. System.out.println()方法使用时需要注意的问题。</a>
### <a name="32">32. 继承和组合区别。</a>
### <a name="33">33. final finally finalize 的区别。</a>
### <a name="34">34. JDK1.7 和 1.8 的区别。</a>
### <a name="35">35. List<String>能否转为List<Object>?能否List<Object>list=newArrayList<String>()?List<String>list=new ArrayList<Object>()?原因? </a>
### <a name="36">36. 泛型的好处?</a>

