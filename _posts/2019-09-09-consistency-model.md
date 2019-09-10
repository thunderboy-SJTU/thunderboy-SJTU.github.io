---
layout: post
title: Consistency Model
description: "关于一致性模型的相关探讨"
modified: 2019-09-09
tags: [Distributed Systems, Consistency]
---



本文将探讨分布式系统中最重要的概念之一：**一致性模型 (Consistency Model)**。


在分布式场景下，根据实际的需要，我们往往会将数据复制到不同的机器上作为缓存，以提升系统整体的性能、可用性及可靠性。然而，一旦数据被存储到不同的机器上，就必然会产生所谓的一致性问题。

对于一致性模型，Todd Lipton曾给出过如下定义：

> **Consistency model** defines rules for the apparent order and visibility of updates, and it is a continuum with tradeoffs.
> 　　　　　　　　　　　　　　　　　　　　　　　　　　　　　- - Todd Lipton

正如上文所述，一致性模型，可看作是一套用户和系统之间的协议。如果用户按照模型指定的规则去进行读写操作，那么，系统就能保证用户读写的结果是可预测的，即用户可以根据系统符合的一致性模型推演出系统可能的表现。一般来说，在一致性模型中提到的操作均指读操作或写操作。


不同的对于系统行为及表现的约束，也衍生出了一系列不同的一致性模型。根据约束的强弱，不同的一致性模型也存在强弱之分。为了更详细地介绍一致性模型，本文列举了一些经典的一致性模型：

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

在讨论Strict Consistency之前，我们先来辨析一下相关的概念：

#### Linearizability vs. Serializability

在许多情况下，我们往往会混用 Linearizability 和 Serializability 这两个词汇，但实际上两者分别代表着不同的概念。

Linearizability，是在单个变量（或者说同一内存位置）上对于单条操作顺序的保证。在每个节点上，它们看到的对于单个变量的操作顺序都是相同的，且严格按照真实发生的全局时间顺序。换句话说，任何读操作应能读到最新的写，从而保证单个变量的线性读写顺序。但是，Linearizability 并不保证多个变量之间的读写顺序关系。

Serializability，则是基于多个变量，且以多条操作为基本单位，也就是所谓的串行化。多条操作组成一个 transaction，如果最后的调度顺序的观测结果等价于某一串行调度 (total ordering)，我们就认为这一顺序满足 Serializability。

如果我们将 Linearizability 和 Serializability 相结合，又能得到什么呢？ Strict Consistency 给出了答案。 

#### Strict Consistency
Strict Consistency，即严格一致性模型。在 Strict Consistency 下，对于每个 operation，都应该有一个全局的 wall-clock time （也就是系统时间，或者称之为墙上时间）时间戳与之相对应。对于每个节点，它们看到的操作执行顺序都是唯一的，且该顺序由每个操作的全局时间戳唯一决定。

不同节点上的操作都按照全局唯一的时间戳进行排列，从而形成了一个完整的全序关系。Strict Consistency 结合了 Serializability 以及 Linearizability，最终的执行顺序等价于某一串行调度，并且串行顺序由全局的时间戳由real time顺序决定。

Strict Consistency 是最强的一致性模型，它可以保证不同节点上的数据和操作完全一致。然而，在大型分布式场景下，Strict Consistency理论上很难实现，因为它需要一个全局唯一时间的存在。对于不同的机器，保证它们的时间完全相同几乎是不可能的。除此之外，我们也一般不需要系统具有如此之强的一致性。在实际应用中，我们往往退而求其次，选择其它更为 relaxing 的一致性模型。

在 Google设计的 [Spanner](https://www.usenix.org/system/files/conference/osdi12/osdi12-final-16.pdf "spanner") 系统中，通过给不同机器配备 GPS 及原子钟，并以返回时间区间的方式，来实现并维护一个全局的唯一时间。时间区间由预计的最差时间漂移来决定，通过避免时间区间的重叠，来保证不同操作间遵循严格的时间顺序。在论文中，作者将由这种方式实现的一致性称之为 External Consistency，但本质上，External Consistency 就可看作是 Strict Consistency 的一种实现方式。

## <span id="sequential">Sequential Consistency</span>

明天继续填坑。




