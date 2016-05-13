# weblog
基于Hadoop的Web日志分析，包括日志的清洗、日志的统计分析、统计结果的导出、指标数据的Web展示

##主要要分析、统计的指标数据
浏览量PV：页面浏览量PV(Page View),是指用户浏览页面的总和，一个独立用户每打开一个页面就被记录一次。网站总流量，可以考核用户对网站的兴趣，就像收视率对电视剧一样。但是对于网站运营者说，更重要的是，每个栏目下的总浏览量。
访客数UV（包括新访客数、新访客比例）。访客数（UV）即唯一访客数，一天之内网站的独立访客数(以Cookie为依据)，一天内同一访客多次访问网站只计算1 个访客。在统计工具中，我们经常可以看到，独立访客和IP数的数据是不一样的，独立访客都多于IP数。那是因为，同一个IP地址下，可能有很多台电脑一同使用，这种情况，相信都很常见。还有一种情况就是同一台电脑上，用户清空了缓存，使用360等工具，将cookie删除，这样一段时间后，用户再使用该电脑，进入网站，这样访问数UV也被重新加一。
对于网站统计来说，关于访客数需要注意的另一个指标就是新访客数，新访客数据可以衡量网站通过推广活动所获得的用户数量。新访客对于总访客数的比值，可以看到网站吸引新鲜血液的能力以及如何保留旧有用户。
IP数：一天之内，访问网站的不同独立IP 个数加和。其中同一IP无论访问了几个页面，独立IP 数均为1。这是我们最熟悉的一个概念，无论同一个IP上有多少电脑，或者其他用户，从某种程度上来说，独立IP的多少，是衡量网站推广活动好坏最直接的数据。
跳出率:只浏览了一个页面便离开了网站的访问次数占总的访问次数的百分比，即只浏览了一个页面的访问次数/全部的访问次数汇总。跳出率是非常重要的访客黏性指标，它显示了访客对网站的兴趣程度：跳出率越低说明流量质量越好，访客对网站的内容越感兴趣，这些访客越可能是网站的有效用户、忠实用户。该指标也可以衡量网络营销的效果，指出有多少访客被网络营销吸引到宣传产品页或网站上之后，又流失掉了。比如，网站在某媒体上打广告推广，分析从这个推广来源进入的访客指标，其跳出率可以反映出选择这个媒体是否合适，广告语的撰写是否优秀，以及网站入口页的设计是否用户体验良好。

##系统架构设计
日志是由业务系统产生的，我们可以设置web服务器每天产生一个新的目录，目录下面会产生多个日志文件。设置系统定时器CRON，夜间在0点后，向HDFS导入昨天的日志文件。完成导入后，设置系统定时器，启动MapReduce程序，提取并经过Hive计算统计指标。完成计算后，设置系统定时器，从HDFS导出统计指标数据到MySQL数据库,然后通过web系统将KPI指标直观显示出来，供分析决策使用。


