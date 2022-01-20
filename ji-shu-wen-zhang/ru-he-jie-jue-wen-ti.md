# 如何解决问题

最近帮一个朋友写一套非常复杂的递归算法，在向他解释具体的实现和如何解决这类问题时，归纳出来一套解决复杂问题的通用思路，在这里记录一下

### 总览全局，明确目标

首先，要纵览问题的全貌，了解问题的输入，确定问题输出和所有执行条件。

### 领域建模，统一问题要素语言

其次，要确定问题中所涉及的所有实体的命名和彼此之间的关系。给一个概念以名字是一个固化观念描述业务对象的很好方式，这点在团队协作中尤其重要，很多时间大家争执的关键其实说的是同一件事情，只不过对这件事情的命名不一样，导致的分歧。

### 拆分复杂问题

我了解的最有效解决复杂问题的方式就是拆分，把大问题拆分成小问题，逐个解决逐个击破是最好的解决复杂问题的方式。人脑的内存是有限的，无法同时关注过多的事情，那何不把事情拆分成原子状态在逐个击破。

说到问题拆分，这里推荐一个我个人在处理复杂数据流使非常喜欢的设计模式 —— 管道模式。我发现很多类似的问题也可以套用管道模式的思路去解决。在管道模式中，我们了解每一个pipe 的输入和输出，前一个pipe的输出可以是后一个pipe 的输入。最终问题经过逐步拆解，处理过程被原子化，分解到了不同的pipe 里。完美适配软件设计思想中的高内聚 低耦合，和解决复杂问题方法的问题拆分。

具体如何拆分有两个方法可以参考，归纳法和演绎法。拆分的注意事项，即拆分出的问题要有原子性，这样有利于低耦合，适当考虑复用，如何拆分出来的子问题还是很多很复杂，这时候我们就要考虑分层，在我的这篇文章中有介绍。

### 保持头脑清晰

时刻盯紧目标，保持头脑清晰。是解决复杂问题的首要原则。盯紧目标不是指大目标，而是你经过拆分后的每一个小目标。这首先要求你对大目标的解决步骤有精心设计，那么这个小目标就是解决大目标的必要路径，那么当你在解决这个小目标的时候，就把他当成你的全部目标去解决，要是分解的足够细致，小目标应该可以很容易被解决。如果发现这个小目标也太复杂，没关系不用怕，我们继续拆分即可。

在每一个阶段，你只需要紧盯当前目标，是不是瞅一眼大目标方式大路径的偏移。

目标可以给你方向感，是另外一个解决复杂问题的关键点：保持头脑清晰的必要条件。目标都不知道，你确定你能做到头脑清晰吗？

有了大小目标，你才能在实现的过程中，每当与各种小怪兽拦路虎搏斗时，近乎要丧失方向时，重新找到方向感，而这种方向感，是保证你能走出现有逻辑迷宫的等他（是的，当一个需求足够复杂，他的实现就会像逻辑迷宫一样）。
