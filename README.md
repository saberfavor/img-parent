# Redis使用初阶
+ **redis解释**：
1. redis 是一个基于 key-value 形式进行存储的内存型数据库。
	+ 数据存储方式为 key-value 
	+ 数据存储在内存中,优点:效率高.理论值:每秒 10K 数据读取
	+ 定位: 数据库软件
2. reids 是一个 NoSql 数据库
	+ 字面理解: 不使用 SQL 命令操作数据库软件
	+ NoSQL : 英文全称 Not Only SQL ,表示在应用程序开发时,不是必须使用关系型数据库,可以使用 NoSQl 替代关系型数据库的部分功能
	+ 目前 NoSQL 不能完全替代关系型数据库.使用关系型数据库结合 NoSQl 数据库进行完成项目
		1. 当数据比较复杂时不适用于 NoSQL 数据库
		2. 关系型数据库依然做为数据存储的主要软件.
		3. NoSQL 数据库当作缓存工具来使用.
			+ 把某些使用频率较高的内容不仅仅存储到关系型数据库中还存储到 NoSQL 数据中
			+ 考虑到: NoSQL 和关系型数据库数据同步的问题
3. Redis 持久化策略
	+ rdb
		1. 每隔一定时间后把内存中数据持久化到 dump.rdb 文件中
		2. 缺点:数据过于集中, 可能导致最后的数据没有持久化到 dump.rdb 中,解决办法:使用命令:SAVE 或 BGSAVE 手动持久化.
	+ aof
		1. 监听 Redis 的日志文件,监听如果发现执行了修改,删除,新增命令.立即根据这条命令把数据持久化.
		2.  缺点:效率降低	
+ **redis 数据类型**:
1. String
2. Hash
3. List
4. Set
5. SortedSet 有序集合
+ **redis 几个常用概念**:
1. Redis 默认有 16384 solts(槽),每个槽可以存储多个 hash 值.
2. Redis 默认不需要密码: requirepass	smalling	
3. 设置密码后需要通过
3.1. -h 主机 ip
3.2. -p 端口
3.3. -a 密码
./redis-cli -h 127.0.0.1 -p 6379 -a smallming
+ **Jedis**:
1. Jedis 是 Redis 客户端工具 jar
2. 使用非集群版示例代码
```java
	Jedis jedis = new Jedis("127.0.0.1", 6379);
	
	// 新增或修改
	 String result = jedis.set("address", "成都");
	// 查询
	 String result1 = jedis.get("address");
	// 删除
	Long index = jedis.del("address");
   ```
+ **Junit 4**:
1. 单元测试插件.
2. 使用 Junit 主要目的
	- 可以不用编写 main 方法
3. 要求:
	- 方法必须是 public void 且没有参数
	- 当前项目不要有 Test 否则@Test 引用自己 Test 类
4. 实现步骤:(Maven)
	- 在 pom.xml 中依赖 junit4
	- ```
		<dependency>
		<groupId>junit</groupId>
		<artifactId>junit</artifactId>
		<version>4.12</version>
		</dependency>
		```
- 在需要测试的方法上添加@Test
	1. @Before 在@Test 之前执行
	2. @After 在@Test 之后执行.
    3. 如果有多个@Test 每个@Test 前后都会执行@Before 和@After
