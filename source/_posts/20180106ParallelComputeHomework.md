---
layout: '[default_layout]'   
title: 分布并行计算机技术作业         
date: 2018-01-06 21:47:41  
updated: 
permalink: 
render_drafts: true
copyright: true
password: 
comments: true
toc: true                  
tags:                        
- 分布式
- 并行
- Hadoop
- Spark

categories:                  
- OTHER

---
[超级详细的Hadoop和Spark 开发环境搭建](https://www.jianshu.com/p/e84d0973099f)
[马士兵的hadoop环境搭建视频也不错](http://www.mashibing.com/hadoop_install.html)
# 测试是否可以上网
wget http://www.scala-lang.org/download/
或者ping www.baidu.com

哈希吧，一开始master和slave123之间互相ping不通，但是slave123之间互相能ping通，而且主机和所有虚拟机之间都能互相ping通。但是，启动集群后或者是其他操作后，一脸懵逼的发现能ping通了。不知道什么原因，可能是mac地址冲突吧。

<!--more-->

```
  好久没写博客了，这两天做实验：
1、起初一台电脑上装了win7系统，里面装了vmware虚拟机，并在虚拟机中虚拟了一台linux系统；
2、由于实验需要，遂在另一台win7系统上也装了个vmware；
3、将第一台电脑里面linux虚拟机目录直接拷贝到了第二台电脑里，并在第二台电脑中打开了vmware，用其打开拷贝过来的虚拟机时，选择了"I move it“。
4、之后两台电脑直连，并配置两个虚拟机中的地址在同一网段，结果无法ping通；
5、各种原因排查无果之后，发现可能是复制过程中，两个虚拟机的网卡mac地址一样了，导致无法ping通，因此，修改第二台虚拟机的网卡mac地址，问题解决！

    vmware虚拟机mac地址修改方法：
  找到虚拟机目录下的.vmx文件，打开，然后修改以下两行：
 ethernet0.generatedAddress = "00:0c:29:1c:35:cc"
   uuid.bios = "56 4d e0 c4 a2 41 24 1b-5b 6e 4b a0 0b 1c:35:cc"
    注释：
     其中 00:0c:29: 不能够修改
          1c:35:cc可以修改

PS:下次注意，在复制了虚拟机目录之后，并采用vmware打开时，如果复制前的虚拟机也打算使用，那么此处一定要选择"I copy it”，如果是因为换电脑等原因，原来的虚拟机不再使用了，那么才选择"I move it“。
```

# 
<!--more-->
```
2017级“分布并行计算机技术”试卷
学号：                姓名：                  专业：


利用不少于5台计算机组成集群系统，在同一硬件环境下，分别利用不同的软件平台进行大数据并行处理。
设计与实现内容：
1.自己下载或利用各自实验室已有的数据集（不小于100MB），编程实现大数据并行处理功能，撰写完整的设计、实验文档。编程语言自定。
2. 对数据集进行详细说明，具体定义并行处理需求。
3. 撰写Hadoop环境安装及在该平台下的程序设计文档。
4. 撰写Spark环境安装及该平台下的程序设计文档。
5. 实验结果对比分析与优化建议。

要求：
1．不需要单独的封面（本页为第1页及封面）
2．A4纸张纵向打印（最好双面打印）
3．左侧装订
4．正文小四号宋体，1.25倍行距
5．提交截止日期：2018年1月31日（过期无效）
6．提交方式：纸质版+电子版
7．提交地址：B603，希望班长收齐后统一提交
8．电子版提交内容：文档及源程序、执行程序和数据集
9．文件名：
文档名：学号-姓名-分布并行计算机技术.docx
数据集：学号-姓名-数据集及源程序名称（可为文件夹名）
   上述红色斜体部分用具体内容代替，-为半角符号。
不符合上述要求者将以0分计
```


# 第一步：搭建虚拟机Hadoop环境不少于5台计算机，一台master，其余分别叫slave1、slave2、slave3、slave4、slave5。
以前跟着马士兵的视频已经搭建好hadoop集群，现在需要的是增加两台salve计算机。
1、在虚拟机VertuBOX中右键完全复制slave，分别取名slave4、slave5.
2、查看网关地址，改成虚拟机ip地址。vim /etc/sysconfig/network
3、设置本机的ip地址。vim /etc/sysconfig/network-sripts/ifcfg-enp0s3
4、修改主机名hostnamectl set-hostname master (主机名千万不能有下划线！)，重启生效。
5、修改机器的/etc/hosts,让他们通过名字认识对方，测试一下互相用名字可以ping通。
6、修改master下的vim /usr/local/hadoop/etc/hadoop/slaves
7、格式化配置
```
(1)启动namenode和datanode
master上需要格式化namenode，执行指令：
hadoop namenode -format
(2)启动master上的namenode，在master上执行：
hadoop-daemon.sh start namonode
(3)启动slave上的datanode，在每个slave上执行：
hadoop-daemon.sh start datanode
使用jps查看namenode和datanode的启动情况。
```
8、[出现hadoop datanode启动后自动关闭问题](https://www.cnblogs.com/sasan/p/5740367.html)
```
方案一：直接格式化hdfs：
关闭hadoop：stop-all.sh
删除tmp:rm -rf hadoop/tmp
从日志中可以看出，原因是因为datanode的clusterID 和 namenode的clusterID 不匹配。
打开hdfs-site.xml里配置的datanode和namenode对应的目录，分别打开current文件夹里的VERSION，可以看到clusterID项正如日志里记录的一样，确实不一致，修改datanode里VERSION文件的clusterID 与namenode里的一致，再重新启动dfs（执行start-dfs.sh）再执行jps命令可以看到datanode已正常启动。
出现该问题的原因：在第一次格式化dfs后，启动并使用了hadoop，后来又重新执行了格式化命令（hdfs namenode -format)，这时namenode的clusterID会重新生成，而datanode的clusterID 保持不变。
解决主机节点 txid不一致问题
把主机下namenode（name文件夹）下的current文件删除或者移走，重新格式化

很容易出现这个问题，我的解决方法删除tmp：
cat /usr/local/hadoop/etc/hadoop/core-site.xml里面写了hadoop的垃圾文件夹地址
cd /
rm -rf tmp
格式化:hadoop namenode -format
启动:start-all.sh

存在问题：会删除hdfs的数据；
```
9、浏览器地址栏输入：http://192.168.56.100:50070    hadoop集群环境完成。

# 第二步：搭建Spark环境
在使用shell连接虚拟机时连接等待时长太长，ssh的服务端在连接时会自动检测dns环境是否一致导致的，修改为不检测即可。
1、打开sshd服务的配置文件/etc/ssh/sshd_config，把UseDNS yes,改为UseDNS no
2、重启sshd服务 /etc/init.d/sshd restart 

# 解压.tar.gz出错gzip: stdin: not in gzip format tar
https://www.cnblogs.com/yajing-zh/p/4952940.html
阳痿和太监还是不一样的，虽然都是不能 
String s1="",s2=null; 

s1.toString();//这个不报错 
s2.toString();//这个报错



# 数据集详细说明
使 用 Audioscrobbler 公 开 发 布 的 一 个 数 据 集。Audioscrobbler 是 last.fm 的 第一个音乐推荐系统。last.fm 创建于 2002 年，是最早的互联网流媒体广播站点之一。Audioscrobbler 提供了开放的“scrobbling”API，“scrobbling”可以记录听众播放过哪些艺术家的歌曲。last.fm 使用这些音乐播放记录构建了一个强大的音乐推荐引擎。由于第三方应用和网站可以把音乐播放数据反馈给这个推荐引擎，这个推荐引擎系统覆盖了数百万的用户。2005 年 last.fm 发布了该数据集的一个版本，读者可以在网上下载到压缩的归档文件（http://www-etud.iro.umontreal.ca/~bergstrj/audioscrobbler_data.html ）。下载归档文件后，你会发现里面有几个文件。主要的数据集在文件 user_artist_data.txt 中，它包含 141 000 个用户和 160 万个艺术家，记录了约 2420 万条用户播放艺术家歌曲的信息，其中包括播放次数信息。
数据集在 artist_data.txt 文件中给出了每个艺术家的 ID 和对应的名字。请注意，记录播放信息时，客户端应用提交的是艺术家的名字。名字如果有拼写错误，或使用了非标准的名称，事后才能被发现。比如，“The Smiths”“Smiths, The”和“the smiths”看似代表不同艺术家的 ID，但它们其实明显是指同一个艺术家。因此，为了将拼写错误的艺术家 ID 或ID 变体对应到该艺术家的规范 ID，数据集提供了 artist_alias.txt 文件。

# 交替最小二乘推荐算法
现在我们要给这个隐式反馈数据选择一个合适的推荐算法。这个数据集只记录了用户和歌曲之间的交互情况。除了艺术家名字外，数据集没有包含用户的信息，也没有提供歌手的其他任何信息。我们要找的学习算法不需要用户和艺术家的属性信息。这类算法通常称为协同过滤算法（http://en.wikipedia.org/wiki/Collaborative_filtering ）。举个例子，根据两个用户的年龄相同来判断他们可能有相似的偏好，这不叫协同过滤。相反，根据两个用户播放过许多相同歌曲来判断他们可能都喜欢某首歌，这才叫协同过滤。
Audioscrobbler 数据集包含了数千万条某个用户播放了某个艺术家歌曲次数的信息，看起来是很大。但从另一方面来看数据集又很小而且不充足，因为数据集是稀疏的。虽然数据集覆盖 160 万个艺术家，但平均来算，每个用户只播放了大约 171 个艺术家的歌曲。有的用户只播放过一个艺术家的歌曲。对这类用户，我们也希望算法能给出像样的推荐。毕竟每个用户在某个时刻只能播放一首歌曲。
最后，我希望算法的扩展性好，不但能用于构建大型模型，而且推荐速度快。我们通常都要求推荐是接近实时的，也就是在一秒内给出推荐，而不是要等一天。
我将用到潜在因素（http://en.wikipedia.org/wiki/Factor_analysis ）模型中的一种模型，这类模型涉及的范围很广泛。潜在因素模型试图通过数量相对少的未被观察到的底层原因，来解释大量用户和产品之间可观察到的交互。打个比方：有几千个专辑可选，为什么数百万人偏偏只买其中某些专辑？可以用对类别（可能只有数十种）的偏好来解释用户和专辑的关系，其中偏好信息并不能直接观察到，而数据也没有给出这些信息。
说得更明确一些，我用的是一种矩阵分解模型（http://en.wikipedia.org/wiki/Nonnegative_matrix_factorization ）。数学上，这些算法把用户和产品数据当成一个大矩阵A，矩阵第 i 行和第 j 列上的元素有值，代表用户 i 播放过艺术家 j 的音乐。矩阵 A 是稀疏的：A中大多数元素都是 0，因为相对于所有可能的用户 - 艺术家组合，只有很少一部分组合会出现在数据中。算法将 A 分解为两个小矩阵 X 和 Y 的乘积。矩阵 X 和矩阵 Y 非常“瘦”，因为 A 有很多行和列，但 X 和 Y 的行很多而列很少（列数用 k 表示）。这 k 个列就是潜在因素，用于解释数据中的交互关系。由于 k 的值小，矩阵分解算法只能是某种近似，如图 3-1 所示：

矩阵分解算法有时称为矩阵补全（matrix completion）算法，因为原始矩阵 A 可能非常稀疏，但乘积 XYT 是稠密的，即使该矩阵存在非零元素，非零元素的数量也非常少。因此模型只是对 A 的一种近似。原始 A 中大量元素是缺失的（元素值为 0），算法为这些缺失元素生成（补全）了一个值，从这个角度讲，我们可以把算法称为模型。

# 准备数据
1、将三个数据文件全部复制到 HDFS。我的文件放在 /user/ds/ 目录下，启动 sparkshell。
构建模型的第一步是了解数据，对数据进行解析或转换，以便在 Spark 中做分析。
Spark MLlib 的 ALS 算法实现有一个小缺点：它要求用户和产品的 ID 必须是数值型，并且是 32 位非负整数。这意味着大于 Integer.MAX_VALUE（即 2147483647）的 ID 都是非法的。我们的数据集是否已经满足了这个要求？利用 SparkContext 的 textFile 方法，将数据文件转换成 String 类型的 RDD：


```
val rawUserArtistData = sc.textFile("/home/hejian/parallelcompute/user_artist_data.txt", 3)
```

默认情况下，RDD 为每个 HDFS 块生成一个分区，将 HDFS 块大小设为典型的 128 MB 或64 MB。由于 HDFS 文件大小为 400 MB，所以文件被拆为 3 个或 6 个分区。这通常没什么问题，但由于相比简单文本处理，ALS 这类机器学习算法要消耗更多的计算资源，因此减小数据块大小以增加分区个数会更好。减小数据块大小能使 Spark 处理任务时同时使用的处理器核数更多。可以为 textFile 方法设置第二个参数，用这个参数指定一个不同于默认值的分区数，这样就可以将分区数设得大一些。比如，可以考虑将这个参数设为集群处理器总核数。

文件的每行包含一个用户 ID、一个艺术家 ID 和播放次数，用空格分隔。要计算用户 ID 的统计信息，可以用空格拆分每行，并将第一个值（下标为 0）解析为一个数。方法 stats()返回统计信息对象，包括最大值和最小值。同样我们可以处理艺术家 ID：
```
rawUserArtistData.map(_.split(' ')(0).toDouble).stats()
rawUserArtistData.map(_.split(' ')(1).toDouble).stats()
```
打印出的结果统计信息显示，最大的用户 ID 和艺术家 ID 分别为 2443548 和 10794401，都远小于 2147483647，因此没必要对这些 ID 做进一步处理。
我们知道，在本章示例中的艺术家名字对应模糊的数值 ID。这些信息包含在 artist_data.txt中。现在 artist_data.txt 包含艺术家 ID 和名字，它们用制表符分隔。但是简单地把文件解析成二元组 (Int,String) 会出错：
```
val rawArtistData = sc.textFile("hdfs:///user/ds/artist_data.txt")
val artistByID = rawArtistData.map { line =>
 val (id, name) = line.span(_ != '\t')
 (id.toInt, name.trim)
}
```
这里 span() 用第一个制表符将一行拆分成两部分，接着将第一部分解析为艺术家 ID，剩余部分作为艺术家的名字（去掉了空白的制表符）。文件里有少量行看起来是非法的：有些行没有制表符，有些行不小心加入了换行符。这些行会导致 NumberFormatException，它们不应该有输出结果。
然而，map() 函数要求对每个输入必须严格返回一个值，因此这里不能用这个函数。另一种可行的方法是用 filter() 方法删除那些无法解析的行，但这会重复解析逻辑。当需要将每个元素映射为零个、一个或更多结果时，我们应该使用 flatMap() 函数，因为它将每个输入对应的零个或多个结果组成的集合简单展开，然后放入到一个更大的 RDD 中。它可以和 Scala 集合一起使用，也可以和 Scala 的 Option 类一起使用。Option 代表一个值可以不存在，有点儿像只有 1 或 0 的一个简单集合，1 对应子类 Some，0 对应子类 None。因此在以下代码中，虽然 flatMap 中的函数本可以简单返回一个空 List，或一个只有一个元素的 List，但使用 Some 和 None 更合理，这种方法简单明了。
```
val artistByID = rawArtistData.flatMap { line =>
 val (id, name) = line.span(_ != '\t')
 if (name.isEmpty) {
 None
 } else {
 try {
 Some((id.toInt, name.trim))
 } catch {
 case e: NumberFormatException => None
 }
 }
}
```
artist_alias.txt 将拼写错误的艺术家 ID 或非标准的艺术家 ID 映射为艺术家的正规名字。其
中每行有两个 ID，用制表符分隔。这个文件相对较小，有 200 000 个记录。有必要把它转
成 Map 集合的形式，将“不良的”艺术家 ID 映射到“良好的”ID，而不是简单地把它作
为包含艺术家 ID 二元组的 RDD。这里又有一点小问题：由于某种原因有些行没有艺术家
的第一个 ID。这些行将被过滤掉：
```
val rawArtistAlias = sc.textFile("/home/hejian/parallelcompute/artist_alias.txt") 
val artistAlias = rawArtistAlias.flatMap { line =>
 val tokens = line.split('\t')
 if (tokens(0).isEmpty) {
 None
 } else {
 Some((tokens(0).toInt, tokens(1).toInt))
 }
}.collectAsMap()
```

```
import org.apache.spark.mllib.recommendation._
val bArtistAlias = sc.broadcast(artistAlias)
val trainData = rawUserArtistData.map { line =>
 val Array(userID, artistID, count) = line.split(' ').map(_.toInt)
 val finalArtistID =
 bArtistAlias.value.getOrElse(artistID, artistID) 
 Rating(userID, finalArtistID, count)
}.cache()

val model = ALS.trainImplicit(trainData, 10, 5, 0.01, 1.0)
model.userFeatures.mapValues(_.mkString(", ")).first()
```

```
name := "scala"

version := "0.1"
//2.12.4
scalaVersion := "2.11.8"

//注意这里不要在第一个地方写两个%，否则会出现地址spark-core_2.11_2.12,反正会默认在末尾添加_2.12
libraryDependencies ++= Seq("org.apache.spark" % "spark-core_2.11" % "2.2.1")

import org.apache.spark.{SparkConf, SparkContext}

object WordCount {
  def main(args: Array[String]): Unit = {
    val conf = new SparkConf().setAppName("wordcount")
    val sc = new SparkContext(conf)

    val input = sc.textFile("/home/hejian/spark/testfile/helloSpark")

    val lines = input.flatMap(line => line.split(" "))
    //val count = lines.map(word => (word, 1)).reduceByKey(_+_)
    val count = lines.map(word => (word, 1)).reduceByKey{case (x, y) => x + y}

    val output = count.saveAsTextFile("/home/hejian/spark/testfile/helloSparkRes")
  }
}
```

启动master 
./sbin/start-master.sh
启动worker 
./bin/spark-class org.apache.spark.deploy.worker.Worker spark://sklse:7077
提交作业   
./bin/spark-submit  --master spark://sklse:7077 --class WordCount /home/hejian/spark/scala.jar
./bin/spark-submit  --master spark://master:7077 --class LogCountBySpark /root/LogCountBySpark.jar

./bin/spark-submit  --master spark://master:7077 --class LogCountBySpark /home/hejian/parallelcompute/ComputeMusicArtistBySpark/computemusicartistbyspark.jar

地址相关路径
http://192.168.201.17:8080/
http://192.168.201.171:8081/


https://repo1.maven.org/maven2/org/apache/spark/spark-mllib_2.11/


http://192.168.56.100:8088/cluster

http://itfish.net/article/60727.html

具体见下面说明：

管理界面：http://localhost:8088

NameNode界面：http://localhost:50070

HDFS NameNode界面：http://localhost:8042
