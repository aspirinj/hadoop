## 关于Spark

Spark最初由美国加州伯克利大学（UCBerkeley）的AMP（Algorithms, Machines and People）实验室于2009年开发，是基于内存计算的大数据并行计算框架，可用于构建大型的、低延迟的数据分析应用程序。Spark在诞生之初属于研究性项目，其诸多核心理念均源自学术研究论文。2013年，Spark加入Apache孵化器项目后，开始获得迅猛的发展，如今已成为Apache软件基金会最重要的三大分布式计算系统开源项目之一（即Hadoop、Spark、Storm）。  
  
Spark作为大数据计算平台的后起之秀，在2014年打破了Hadoop保持的基准排序（Sort Benchmark）纪录，使用206个节点在23分钟的时间里完成了100TB数据的排序，而Hadoop则是使用2000个节点在72分钟的时间里完成同样数据的排序。也就是说，Spark仅使用了十分之一的计算资源，获得了比Hadoop快3倍的速度。新纪录的诞生，使得Spark获得多方追捧，也表明了Spark可以作为一个更加快速、高效的大数据计算平台。  
Spark具有如下几个主要特点：  
 运行速度快：Spark使用先进的DAG（Directed Acyclic Graph，有向无环图）执行引擎，以支持循环数据流与内存计算，基于内存的执行速度可比Hadoop MapReduce快上百倍，基于磁盘的执行速度也能快十倍；  
 容易使用：Spark支持使用Scala、Java、Python和R语言进行编程，简洁的API设计有助于用户轻松构建并行程序，并且可以通过Spark Shell进行交互式编程；  
 通用性：Spark提供了完整而强大的技术栈，包括SQL查询、流式计算、机器学习和图算法组件，这些组件可以无缝整合在同一个应用中，足以应对复杂的计算；  
 运行模式多样：Spark可运行于独立的集群模式中，或者运行于Hadoop中，也可运行于Amazon EC2等云环境中，并且可以访问HDFS、Cassandra、HBase、Hive等多种数据源。  
Spark源码托管在Github中，截至2016年3月，共有超过800名来自200多家不同公司的开发人员贡献了15000次代码提交，可见Spark的受欢迎程度。

此外，每年举办的全球Spark顶尖技术人员峰会Spark Summit，吸引了使用Spark的一线技术公司及专家汇聚一堂，共同探讨目前Spark在企业的落地情况及未来Spark的发展方向和挑战。Spark Summit的参会人数从2014年的不到500人暴涨到2015年的2000多人，足以反映Spark社区的旺盛人气。  
Spark如今已吸引了国内外各大公司的注意，如腾讯、淘宝、百度、亚马逊等公司均不同程度地使用了Spark来构建大数据分析应用，并应用到实际的生产环境中。相信在将来，Spark会在更多的应用场景中发挥重要作用。
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTg2ODEzNTk2MV19
-->