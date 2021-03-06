---
title: 概叙 & 应用场景
layout: plain_cn
top-nav-title: 概叙 & 应用场景
top-nav-group: 快速开始
top-nav-pos: 1
sub-nav-title: 概叙 & 应用场景
sub-nav-group: 快速开始
sub-nav-pos: 1
---
# JStorm 是一个分布式实时计算引擎。 

JStorm 是一个类似Hadoop MapReduce的系统， 用户按照指定的接口实现一个任务，然后将这个任务递交给JStorm系统，JStorm将这个任务跑起来，并且按7 * 24小时运行起来，一旦中间一个Worker 发生意外故障， 调度器立即分配一个新的Worker替换这个失效的Worker。

因此，从应用的角度，JStorm应用是一种遵守某种编程规范的分布式应用。从系统角度， JStorm是一套类似MapReduce的调度系统。 从数据的角度，JStorm是一套基于流水线的消息处理机制。

实时计算现在是大数据领域中最火爆的一个方向，因为人们对数据的要求越来越高，实时性要求也越来越快，传统的Hadoop MapReduce，逐渐满足不了需求，因此在这个领域需求不断。

**Storm组件和Hadoop组件对比**

| | *Storm* | *Hadoop* |
| ------------- | ------------- | ------------- |
|角色|Nimbus|JobTracker|
||Supervisor|TaskTracker|
||Worker|Child|
|应用名称|Topology|Job|
|编程接口|Spout/Bolt|Mapper/Reducer|

# 优点
在Storm和JStorm出现以前，市面上出现很多实时计算引擎，但自Storm和JStorm出现后，基本上可以说一统江湖：
究其优点:

* 开发非常迅速：接口简单，容易上手，只要遵守Topology、Spout和Bolt的编程规范即可开发出一个扩展性极好的应用，底层RPC、Worker之间冗余，数据分流之类的动作完全不用考虑
* 扩展性极好：当一级处理单元速度，直接配置一下并发数，即可线性扩展性能
* 健壮强：当Worker失效或机器出现故障时， 自动分配新的Worker替换失效Worker
* 数据准确性：可以采用Ack机制，保证数据不丢失。 如果对精度有更多一步要求，采用事务机制，保证数据准确。

# 应用场景

JStorm处理数据的方式是基于消息的流水线处理， 因此特别**适合无状态计算**，也就是计算单元的依赖的数据全部在接受的消息中可以找到， 并且最好一个数据流不依赖另外一个数据流。

因此，常常用于:

* 日志分析，从日志中分析出特定的数据，并将分析的结果存入外部存储器如数据库。目前，主流日志分析技术就使用JStorm或Storm
* 管道系统， 将一个数据从一个系统传输到另外一个系统， 比如将数据库同步到Hadoop
* 消息转化器， 将接受到的消息按照某种格式进行转化，存储到另外一个系统如消息中间件
* 统计分析器， 从日志或消息中，提炼出某个字段，然后做count或sum计算，最后将统计值存入外部存储器。中间处理过程可能更复杂。
