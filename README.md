# Double My TPS

成员: @flowbehappy, @iosmanthus, @pingyu, @tangenta (in alphabetical order)

## 项目介绍

一键让 TiDB 的 TPS 翻倍

## 背景&动机

众所周知，TiDB 具有良好的扩展性，可以通过简单扩容集群来获得更高的 TPS。但是在某些场景，仍然无法完美的满足需求：

1. 双 11 马上到了，你去找老板要求给 TiDB 集群扩容一倍，以应对预期翻倍的流量。老板的回复：采购来不及了，想办法撑一下吧。
2. 你的应用总是有各种突发几个小时的热点，即使上了 TiDB Cloud，等 TiKV 扩容出来热点可能已经消退了。
3. 定时跑批任务，但又是 TP 负载（比如银行结算），用户只关心啥时候跑完，不关心每一条 SQL 的耗时，能否不扩容的情况下跑快点？
4. 就是穷，想用更少的机器跑更多的负载，SQL 耗时高点可以忍，TPS 能打高可以撑住业务就行

**核心思路**：在不增加 TiDB 节点的前提下，通过各种优化，以及牺牲其他性能指标，换取尽可能高的 TPS

## 项目设计

本项目包含两种优化方向：

1. 通用的，特别是可以提高 TPS 的。比如使用 pipeline 模型
2. 会劣化其他性能指标的（比如 P99 latency），但是可以提高 TPS 的。比如修改默认攒批的粒度

为了方便对比效果，我们使用最常见的 TPCC 负载，并且把这些优化打包到一个开关中：`set tidb_performance_mode = "double_my_tps";`

详细优化方向：TODO




