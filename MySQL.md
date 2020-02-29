# MySQL



## 事务四大特性



- 原子性：事务要么全部执行，要么全部不执行，是不可分割的工作单位。

- 一致性：指事务开始之前和结束以后，完整性约束没有被破坏。

- 隔离性：多个事务并发访问时，事务之间是隔离的，一个事务不应该影响其它事务运行效果。

- 持久性：意味着事务在完成之后，该事务对数据库所作的更改便持久的保存在数据库中，并不会被回滚。



## 事务的并发、隔离级别



### 并发



理论上来说，事务应该彼此完全隔离，以避免并发事务所导致的问题，然而会对性能产生极大的影响，因为事务必须按顺序运行，**在实际开发中，为了提升性能，事务会以较低的隔离级别运行，事务的隔离级别可以通过隔离事务属性指定。**



### 事务的并发问题



1. 脏读：事务A读取了事务B更新的数据，然后B回滚操作，那么A读取到的数据是脏数据。

2. 丢失修改：指在一个事务读取一个数据时，另外一个事务也访问了该数据，那么在第一个事务中修改了这个数据后，第二个事务也修改了这个数据。这样第一个事务修改的结果就会丢失，因此称为丢失修改。

3. 不可重复读：事务A多次读取同一数据，事务B在事务A多次读取的过程中，对数据作了更新并提交，导致事务A多次读取同一数据时，出现的结果不一致。

4. 幻读：解决了不重复读，保证了同一个事务里，查询的结果都是事务开始时的状态。比如说，当A事务将表中c字段的值都改为3，而B事务新增一条数据，c字段为2，那么此时再查看数据会发现有一条并没有修改，这就是幻读。

   

### 事务隔离级别



1. 读未提交：即能够读取到没有被提交的数据。



2. 读已提交：能够读到已提交的数据。



3. 重复读取：即在数据读出来之后加锁，防止别人修改。MySQL默认隔离级别。



4. 串行化：最高的事务隔离级别，不管多少事务，挨个运行完一个事务的所有子事务之后才可以Y行另外一个事务里面的所有子事务。

   

5. | 事务隔离级别 | 脏读 | 不可重复读 | 幻读 |
   | ------------ | ---- | ---------- | ---- |
   | 读未提交     | Y    | Y          | Y    |
   | 读已提交     | N    | Y          | Y    |
   | 可重复读     | N    | N          | Y    |
   | 串行化       | N    | N          | N    |



### 索引



复合索引：可以只使用复合索引中的一部分，但必须是由最左部分开始，且可以存在常量。