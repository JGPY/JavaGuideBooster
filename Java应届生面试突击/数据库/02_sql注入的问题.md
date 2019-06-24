# SQL 注入的问题

### 目录

---
<a href="#1">1. SQL 语句应该考虑哪些安全问题？</a> <br>
<a href="#2">2. 什么叫SQL注入，如何防止？请举例说明。</a> <br>


### <a name="1">1. SQL 语句应该考虑哪些安全问题？</a>
&ensp;&ensp;&ensp;&ensp;
   1.防止 sql 注入， 对特殊字符进行过滤、 转义或者使用预编译的 sql 语句绑定变量。 <br>
&ensp;&ensp;&ensp;&ensp;
   2.当 sql 语句运行出错时， *不要把数据库返回的错误信息*全部显示给用户， 以*防止
泄漏*服务器和数据库相关信息。 <br>

### <a name="2">2. 什么叫SQL注入，如何防止？请举例说明。</a>
举个例子： <br>
&ensp;&ensp;&ensp;&ensp;
    你后台写的 java 代码拼的 sql 如下：
```java
 // 该 ename 为前台传过来的一个查询条件
    public List getInfo(String ename){
        StringBuffer buf = new StringBuffer();
        buf.append("select empno,ename,deptno from emp where ename = '").append(ename).append("'");
        ...
        ...
        ...
    }
```
   
而前台页面有个输入框如下： <br>
职员姓名： __________ <br>
该文本域对应上面方法的 ename 参数。 <br>
如果用户在查询时向职员姓名文本域中输入的是如下信息： <br>
```sql
' or '1'='1 
```
那么这时就会涉及到 sql 注入这个概念了。 <br>
*上面的字符串传到后台后， 与其它 select 等字符串拼成了如下的语句*： <br>
```sql
select empno,ename,deptno from emp where ename = '' or '1'='1'
``` 
*上面的 where 条件是永远成立的*， 如果你的表中有权限限制， 比如只能查询本地市的信息，
过滤条件中有地市过滤， 不过因为输入 ' or '1'='1 字符串后， 条件永远成立， 导致你能看到
所有城市的职员信息， 那就会产生权限问题了， 用户能看到不该看到的信息。 同理， 如果
是 insert 或者 update 等语句的话， 通过 sql 注入会产生不可估量的问题。 <br>
&ensp;&ensp;&ensp;&ensp;
    这种不安全的情况是在 SQL 语句*在拼接的情况下*发生。 <br>
&ensp;&ensp;&ensp;&ensp;

####  解决方法：
1. 参数绑定 <br>
&ensp;&ensp;&ensp;&ensp;
    为了防范这样” SQL 注入安全“可以用预编译解决（不要用拼
接 SQL 字符串,可以用 prepareStatement,参数用 set 方法进行填装 ） 。 <br>
```java
String sql= "insert into userlogin values(?,?)";
try {
    PreparedStatement ps=conn.prepareStatement(sql);
    for(int i=1;i<100;i++){
        ps.setInt(1, i);
        ps.setInt(2, 8888);
        ps.executeUpdate();
    }
    ps.close();
    conn.close(); 
} catch (SQLException e) {
    e.printStackTrace();
} 
```

2. 检查变量的数据类型和格式 <br>
&ensp;&ensp;&ensp;&ensp;
    如果你的 SQL 语句是类似 where id={$id}这种形式， *数据库里所有的 id 都是
数字， 那么就应该在 SQL 被执行前， 检查确保变量 id 是 int 类型*； 如果是接受
邮箱， 那就应该检查并严格确保变量一定是邮箱的格式， 其他的类型比如日期、
时间等也是一个道理。 总结起来： *只要是有固定格式的变量， 在 SQL 语句执行
前， 应该严格按照固定格式去检查， 确保变量是我们预想的格式， 这样很大程
度上可以避免 SQL 注入攻击。* <br>
&ensp;&ensp;&ensp;&ensp;
    比如， 我们前面接受 username 参数例子中， 我们的产品设计应该是在用户
注册的一开始， *就有一个用户名的命名规则*， 比如 5-20 个字符， 只能由大小写
字母、 数字以及一些安全的符号组成， 不包含特殊字符。 此时我们应该有一个
check_username 的函数来进行统一的检查。 不过， 仍然有很多例外情况并不能
应用到这一准则， 比如文章发布系统， 评论系统等必须要允许用户提交任意字
符串的场景， 这就需要采用过滤等其他方案了。 （*使用正则表达式进行格式验
证！*） <br>

3. 所有的 SQL 语句都封装在*存储过程*中。 <br>
&ensp;&ensp;&ensp;&ensp;
    所有的 SQL 语句都封装在存储过程中， 这样不但可以避免 SQL 注入， 还能
提高一些性能。

---
### 搬运工信息
Author:Jason Lou <br>
Email:vip.iotworld@gmail.com <br>
Blog:https://blog.csdn.net/qq_21508727 <br>
Github:https://github.com/JGPY/JavaGuideBooster <br>
---