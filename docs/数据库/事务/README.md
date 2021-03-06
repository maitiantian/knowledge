<div style="position: fixed; bottom: 20px; right: 39px; border-radius: 5px; background-color: #797979; z-index: 100;">
    <a href="#目录" style="color: white; border-right: 1px solid white; text-decoration: none; font-size: 14px; font-weight: bold; display: inline-block; padding: 5px 8px; line-height: 20px;">back to top ▲</a>
    <a href="javascript:void(0)" style="color: white; border-right: 1px solid white; text-decoration: none; font-weight: bold; display: inline-block; padding: 5px 8px; line-height: 20px;" onclick="(function(){document.querySelector('.btn.pull-left.js-toolbar-action').click()})()"><i class="fa fa-align-justify"></i></a>
</div>

# 事务

* [事务四大特性](#事务四大特性)
* [隔离级别](#隔离级别)



数据库事务(Database Transaction)，是指作为单个逻辑工作单元执行的一系列操作，要么完全地执行，要么完全地不执行。

# <p align="center" style="border-bottom: 3px solid #e7e7e7;">事务四大特性</p>


一个逻辑工作单元要成为事务，必须满足所谓的ACID（原子性、一致性、隔离性和持久性）属性。

1. 原子性(Atomicity)

    *事务包含的所有操作要么全部成功，要么全部失败回滚*
2. 一致性(Consistency)

    *事务必须使数据库从一个一致性状态变换到另一个一致性状态*

    *转账来说，假设用户A和用户B两者的钱加起来一共是5000，那么不管A和B之间如何转账，转几次账，事务结束后两个用户的钱相加起来应该还得是5000，这就是事务的一致性。*
3. 隔离性(Isolation)

    *当多个用户并发访问数据库时，比如操作同一张表时，数据库为每一个用户开启的事务，不能被其他事务的操作所干扰，多个并发事务之间要相互隔离。*

    *对于任意两个并发的事务T1和T2，在事务T1看来，T2要么在T1开始之前就已经结束，要么在T1结束之后才开始，这样每个事务都感觉不到有其他事务在并发地执行。*
4. 持久性(Durability)

    *一个事务一旦被提交了，那么对数据库中的数据的改变就是永久性的，即便是在数据库系统遇到故障的情况下也不会丢失提交事务的操作。*


# <p align="center" style="border-bottom: 3px solid #e7e7e7;">隔离级别</p>


SET Transaction Isolation Level { READ COMMITTED | READ UNCOMMITTED | REPEATABLE READ | SERIALIZABLE };

1. READ UNCOMMITTED

    读未提交：一个事务可以读取另一个未提交事务的数据。

    老板要给程序员发工资，程序员的工资是3.6万/月。但是发工资时老板不小心按成3.9万/月，该钱已经打到程序员的账户，但事务还没提交。这时，程序员去查看自己的工资发现比往常多了3千元，以为涨工资了非常高兴。但是老板及时发现了不对并马上回滚了差点就提交的事务，将数字改成3.6万再提交。

    程序员看到的是老板还没提交事务时的数据，这就是**脏读**。

2. READ COMMITTED

    读提交：一个事务要等另一个事务提交后才能**读取数据**。**解决脏读问题。**

    程序员拿着有3.6万余额的工资卡去消费，当他买单时（程序员事务开启），收费系统事先查询到他的卡里有3.6万（程序员事务查询）。就在这时！程序员的老婆要把钱全部转出充当家用（老婆事务开启，进行更新操作UPDATE），并提交（老婆事务提交）。当收费系统准备扣款时，再检测卡里的金额（程序员事务查询），发现已经没钱了（第二次查询操作要等待老婆事务的更新操作完成后才能返回结果）。程序员很郁闷：明明卡里是有钱的……

    在这个事例中，**一个事务范围内两个相同的查询返回了不同数据**，这就是**不可重复读**。

3. REPEATABLE READ

    重复读：当一个事务开启时，不再允许其它事务的修改操作（UPDATE）。**解决不可重复读问题。**

    程序员拿着有3.6万余额的工资卡去消费，当他买单时（程序员事务开启，不再允许其他事务的UPDATE修改操作），收费系统查询到他的卡里有3.6万（程序员事务查询）。这时程序员的老婆就不能转出金额了（转账，UPDATE操作）。接下来收费系统就可以扣款了。

    **不可重复读对应的是修改，即UPDATE操作**。但是可能还会有幻读问题。因为**幻读问题对应的是插入INSERT操作**，不是UPDATE操作。

    程序员某天去消费，花了2千元，这时他的老婆去查看他今天的消费记录（老婆事务开启，查询），看到确实是花了2千元，就在这时，程序员又花了1万元买了一部电脑，即新增INSERT了一条消费记录，并提交。当老婆打印程序员的消费记录清单时（老婆事务提交，查询），发现花了1.2万元，似乎出现了幻觉，这就是幻读。

4. SERIALIZABLE

    SERIALIZABLE是最高的事务隔离级别，在该级别下，**事务串行化顺序执行**，可以避免脏读、不可重复读与幻读。
    
    但是这种事务隔离级别效率低下，比较耗数据库性能，一般不使用。


* SQL Server，Oracle默认的隔离级别是READ COMMITTED；
* MySQL默认的隔离级别是REPEATABLE READ；
* 一次只能设置一个选项，且设置的选项将一直对那个连接保持有效，直到显式更改该选项为止。这是默认行为，除非在语句的FROM子句中在表级上指定优化选项。