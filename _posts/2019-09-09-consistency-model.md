---
layout: post
title: Consistency Model
description: "关于一致性模型的相关探讨"
modified: 2019-09-09
tags: [Distributed Systems]
---



本文将探讨分布式系统中最重要的概念之一：**一致性模型 (Consistency Model)**。


在分布式场景下，根据实际的需要，我们往往会将数据复制到不同的机器上作为缓存，以提升系统整体的性能、可用性及可靠性。然而，一旦数据被存储到不同的机器上，就必然会产生所谓的一致性问题，而一致性模型，则可以看作是一套用户和系统之间的协议。如果用户按照模型指定的规则去进行读写操作，那么，系统就能保证用户读写的结果是可预测的。

对于一致性模型，Todd Lipton曾给出过如下定义：

> Consistency model defines rules for the apparent order and visibility of updates, and it is a continuum with tradeoffs.    


系统行为及表现的约束的不同，也衍生出了不同的一致性模型。根据约束的强弱，不同的一致性模型也存在的强弱之分。为了更详细地介绍一致性模型，本文列举了一些经典的一致性模型：

* [Strict Consistency](#strict)
* [Sequential Consistency](#sequential)
* [Release Consistency](#release)
* [Causal Consistency](#causal)
* [Processor Consistency](#processor)
* [PRAM Consistency](#pram)
* [Cache Coherence](#cache)
* [Eventual Consistency](#eventual)

在之后的篇章中，本文会逐一对上述一致性模型进行介绍。


## <span id="strict">Strict Consistency</span>

先留个坑，明天再写。


