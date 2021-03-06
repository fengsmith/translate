原文链接：https://en.wikipedia.org/wiki/ACID

在计算机科学中，ACID（Atomicity 原子性、Consistency 一致性、Isolation 隔离性、Durability 持久性）是一系列属性。
这些属性保证了数据库事物的可靠。在数据库中，对数据的一系列操作在逻辑上可以看成一个整体的操作，这个整体的操作就叫事物。
例如，银行从一个账户往另外一个账户转账的过程中就牵涉到多个变更操作。比如，减少一个账户的资金，同时增加另外一个账户的资金，就是一个事物。
Jim Gray 在 20 世纪 70 年代后期定义了可信事物系统的这些操作，后来这些技术都得到了发展。
在 1983 年， Andreas Reuter 和 Theo Härder 发明了 ACID 这个缩略词来描述数据库事物的这些属性。
数据库事物的特点：
Atomicity（原子性）
原子性要求每个事物中的所有操作要么全部完成，要么就像全部没有发生一样：如果事物中的部分操作失败了，则整个事物事物失败了，结果就是数据库中的状态保持没变。原子性系统必须保证在各种情况下的原子性，包括主机断电、主机发生了错误、主机奔溃。对外界来说，一个提交了的事物看起来（通过事物对数据库产生的影响）是不可分的，一个失败了的事物，对外界来说就好像什么都没有发生过一样。
Consistency（一致性）
一致性确保了任何事物都会使数据库从一种合法的状态变为另一种合法的状态。通过定义的各种规则，包括约束（constraints）、级联（cascades）、触发器（triggers）以及它们的组合来保证写入数据库的所有数据都必须是合法的。持久性并不能保证事物（程序）的正确性，换句话说事物的持久性并不一定如程序员所期望的那样（这应该是由应用层代码来负责的），它只能保证数据库中的所有数据都不会违反定义好的规则，不管程序有没有发生错误甚至是发生了任何错误都不会违反定义好的规则。
## Isolation（隔离性）
隔离性保证了并发执行多个事物对系统的状态的影响和串行化执行多个事物对系统的状态的影响是一样的。隔离性是并发控制的主要目标。 通过并发控制的方法，一个未完成的事物的影响对其他事物是不可见的。

## Durability（持久性）
持久性保证了一个事物一旦被提交以后，其状态就保持不变，甚至是发生了主机断电、奔溃、错误等。例如，在关系数据库中，一旦一组 sql 语句被执行后，其结果就被永久保存（甚至事物刚被提交数据库系统就发生了奔溃）。为了主机抵御断电的风险，事物（或者是事物的结果）必须被记录在永久性存储中。

 例子
下面的例子进一步的说明了 ACID 属性。在下面的例子中数据库表有两列，A 和 B 。数据完整性约束要求 A 列的值和 B 列的值之和必须等于 100 。下面的 SQL 语句创建了一张表，这张表满足上面的约束条件——A+B=100 。
  
   
    CREATE TABLE acidtest (A INTEGER, B INTEGER, CHECK (A + B = 100));

## 原子性的反例
在数据库系统中，原子性是 ACID 事物的四个属性之一。在一个原子事物中，一系列的数据库操作要么全部发生，要么全部不发生。这一系列的操作不能被相互分开，只执行部分操作。原子性要求这一系列操作不可分，原子性正如其名。原子性可以保证数据库不会出现部分更新的情况。部分更新的情况带来的问题远远要比所有的操作全部失败带来的问题还要严重。原子性意味着不可分。

## 一致性的反例
一致性是个非常泛化的术语，它要求数据必须满足所有的合法规则。以前面的例子为例，合法性规则是要求 A + B = 100 ，同时 A 和 B 还必须为整数。对于 A 和 B 来说，其合法的范围是可以被推断出来的。所有的合法规则必须都被检查从而确保了事物的一致性。假设一个事物尝试着从 A 中减去 10 而不修改 B 。因为每个事物结束以后都会进行一致性检查，在事物开始之前数据库就知道 A + B = 100 。如果事物成功的从 A 中减去 10 ，原子性就生效了。然而，有效性校验会发现 A + B = 90 ，这与数据库的约束规则不一致。整个事物必须被取消，被影响到的行回滚到执行事物之前的状态。如果还有其他约束、触发器、级联，每一个独立改变的操作在事物被提交之前必须像前面一样进行一致性检查。

违反隔离性
为了演示隔离性，我们假设两个事物在同时修改同一块数据。为了维护隔离性，其中一个事物必须等到另外一个事物完成以后才能执行。考虑下面的两个事物， T1 从 A 中转出 10 到 B 。T2 从 B 中转出 10 到 A 。可以分析出共有四个操作：
1、T1 从 A 中减去 10 。
2、T1 给 B 中加上 10 。
3、T2 从 B 中减去 10 。
4、T2 给 A 中加上 10 。
 如果这些操作按照上面的顺序执行，就可以达到隔离性，尽管 T2 必须等待 T1 先执行。如果 T1 中途失败了，数据库系统会消除掉 T1 对数据库所产生的影响，T2 看到的仍然是合法的数据。

由于两个事物可能交错执行，这几个操作的实际执行顺序可能是：

- T1 从 A 中减去 10 。
- T2 从 B 中减去 10 。
- T2 给 A 增加 10 。
- T1 给 B 增加 10 。

再次假设，T1 中途失败了，将会发生什么。如果 T1 在第四步：T1 给 B 增加 10 时失败了，而此时 T2 已经修改完了 A 和 B；被改变的数据无法恢复到 T1 执行之前的状态，导致了数据库产生了不合法的状态。 这就是有名的 “write-write failure” 失败，由于两个事物尝试同时修改同一个数据块。 在一个典型的系统中，这个问题可以解决。通过取消失败的事物 T1 ，从而使数据库恢复到上次的合法状态，然后重新开始执行被中断的事物 T2 。

## 违反持久性
假设一个事物从 A 中减去 10 加到 B 中。首先，事物会从 A 中减去 10 ，然后再在 B 中加上 10 。 在此时，执行事物的程序会告诉用户，事物已经成功执行了。然后，此时这些改变的数据仍然还在磁盘缓冲区中排队等待写入磁盘中。如果这时主机发生断电，数据库中所有的改变就会丢失。用户还以为所有的改变都已经持久化到磁盘中了。
## 实现

处理一个事物通常需要一系列的操作，每个操作失败了都会导致整个事物的失败，因此，造成事物失败的原因有好多个。例如，系统的磁盘磁盘已经满了，再没有空间了，或者是事物已经用光了操作系统分配给它的 CPU 时间片。有两种大家都很熟悉的流行技术：预写式日志记录和影子分页。这两种技术中，必须要在将被更新的所有信息上获取锁。获取的锁依赖事物的隔离级别，有可能所有的数据仅仅是被读取，也需要获取锁。在预写式日志记录技术中，在改变数据库之前通过复制原始的（未改变的）数据到日志记录中来保证原子性。有了日志记录就可以使数据库恢复到发生奔溃事件之前的一致性状态。在影子分页技术中，更新被应用到数据库的部分拷贝中，当数据库事物提交时，新的拷贝才被激活了。
## 锁和多版本
好多数据库依赖锁来实现 ACID 能力。锁意味着事物在其需要访问的数据上打个标记，这样一来数据库管理系统就会知道这些数据在该事物完成（事物成功或失败）之前不允许其他事物修改这些被打了标记的数据。锁在数据被处理之前必须获取到，也包括处理那些只会被读取但不会被修改的数据之前也要获取锁。非平常事物通常需要大量锁，导致了可观的性能开销同时也阻塞了其他事物。例如，用户 A 正在执行一个事物，需要读取另外一个用户 B 想要修改的一行数据。用户 B 必须等到用户 A 的事物彻底完成。通常通过两个阶段锁来保证全隔离性。

除了锁之外还有一种技术是多版本并发控制。在多版本并发控制技术总，数据库给每一个读事物都提供了优先级。不会改变的数据版本将会被另外一个活动事物修改。这允许读事物不需要获取锁，写事物不会阻塞读事物。回到之前的例子，当用户 A 正在执行的事物用到了用户 B 将要修改的数据。数据库会提供给 A 用户所需要数据的一个版本，这个版本的数据是用户 B 执行事物之前已经存在的一个版本。用户 A 获取到了具有一致性的数据库的一个视图即使其他用户正在修改数据。一个实现，即快照隔离，解放了隔离性。


原文链接：[https://en.wikipedia.org/wiki/ACID](https://en.wikipedia.org/wiki/ACID)


在计算机科学中，ACID（Atomicity 原子性、Consistency 一致性、Isolation 隔离性、Durability 持久性）是一系列属性。
这些属性保证了数据库事物的可靠性。在数据库中，对数据的一系列操作在逻辑上可以看成是一个整体的操作，这个整体的操作就叫做事物。
例如，银行从一个账户往另外一个账户转账的过程中就牵涉到多个变更操作。比如，减少一个账户的资金，同时增加另外一个账户的资金，这两个操作合起来就是一个事物。




Jim Gray 在 20 世纪 70 年代后期定义了可信事物系统的这些操作，后来这些技术都得到了发展。
在 1983 年， Andreas Reuter 和 Theo H?rder 发明了 ACID 这个缩略词来描述数据库事物的这些属性。


# 数据库事物的特点


## Atomicity（原子性）


原子性要求每个事物中的所有操作要么全部完成，要么就像没有发生任何改变一样：如果事物中的部分操作失败了，则整个事物事物失败了（事物失败后会发生回滚），结果就是数据库的状态保持没变。原子性系统必须保证各种情况下的原子性，包括主机断电、主机发生错误、主机奔溃。对外界来说，一个提交了的事物看起来（通过事物对数据库产生的影响）是不可分的，一个失败了的事物，对外界来说就好像什么都没有发生过一样（失败的事物会回滚，所以对外界来说好像什么都没有发生过一样）。


##Consistency（一致性）


一致性确保了任何事物都只能使数据库从一种合法的状态变为另一种合法的状态。通过定义的各种规则，包括约束（constraints）、级联（cascades）、触发器（triggers）以及它们的组合来保证写入数据库的所有数据都必须是合法的。一致性并不能保证事物（程序）的正确性，换句话说事物的持久性并不一定如程序员所期望的那样（这应该是由应用层代码来负责的），它只能保证数据库中的所有数据都不会违反定义好的规则，不管程序有没有发生错误甚至是发生了任何错误都不会违反定义好的规则。


## Isolation（隔离性）


隔离性保证了并发执行多个事物对系统的状态的影响和串行化执行多个事物对系统的状态的影响是一样的。隔离性是并发控制的主要目标。 通过并发控制的方法，一个未完成的事物产生的影响对其他事物是不可见的。


## Durability（持久性）


持久性保证了一个事物一旦被提交以后，其状态就保持不变，甚至是发生了主机断电、奔溃、错误等。例如，在关系数据库中，一旦一组 sql 语句被执行后，其结果就被永久保存（甚至事物刚被提交数据库系统就发生了奔溃）。为了抵御主机断电的风险，事物（或者是事物产生的结果）必须被记录在永久性存储中。


#例子


下面的例子进一步的说明了 ACID 属性。在下面的例子中，假设数据库表有两列：A 和 B 。数据完整性约束要求 A 列的值和 B 列的值之和必须等于 100 ，即：A + B = 100 。下面的 SQL 语句创建了一张表，这张表满足上面的约束条件：A + B = 100 。
  
   
    CREATE TABLE acidtest (A INTEGER, B INTEGER, CHECK (A + B = 100));


## 原子性的反例


在数据库系统中，原子性是 ACID 事物的四个属性之一。在一个原子事物中，一系列的数据库操作要么全部发生，要么全部不发生。这一系列的操作相互不能被分开，只执行部分操作。原子性要求这一系列操作不可分，原子性正如其名。原子性可以保证数据库不会出现部分更新的情况。部分更新的情况带来的问题远远要比所有的操作全部失败带来的问题还要严重。原子性意味着不可分。


## 一致性的反例


一致性是个非常泛化的术语，它要求数据必须满足所有的合法规则。以前面的例子为例，合法性规则是要求 A + B = 100 ，同时 A 和 B 还必须为整数。对于 A 和 B 来说，其合法的范围是可以被推断出来的。所有的合法规则必须都被检查从而确保了事物的一致性。假设一个事物尝试着从 A 中减去 10 而不修改 B 。因为每个事物结束以后都会进行一致性检查，在事物开始之前数据库管理系统就知道 A + B = 100 。如果事物成功的从 A 中减去 10 ，原子性就生效了。然而，有效性检查会发现 A + B = 90 ，这与数据库的约束规则不一致。整个事物必须被取消，被影响到的行回滚到执行事物之前的状态。如果还有其他约束、触发器、级联，每一个单独改变的操作在事物被提交之前必须像前面一样进行一致性检查。


## 违反隔离性


为了演示隔离性，我们假设两个事物在同时试图修改同一块数据。为了维护隔离性，其中一个事物必须等到另外一个事物完成以后才能执行。


考虑下面的两个事物， T1 从 A 中减去 10 加到 B 中。T2 从 B 中减去 10 加到 A 中。可以分析出共需要四个操作：


- T1 从 A 中减去 10 
- T1 给 B 中加上 10 
- T2 从 B 中减去 10 
- T2 给 A 中加上 10
 
 如果这些操作按照上面的顺序执行，就可以达到隔离性，但 T2 必须等待 T1 先执行。如果 T1 中途失败了，数据库系统会消除掉 T1 对数据库所产生的影响，T2 看到的仍然是合法的数据。


由于两个事物可能交替执行，这几个操作的实际执行顺序可能是：


- T1 从 A 中减去 10
- T2 从 B 中减去 10
- T2 给 A 加上 10
- T1 给 B 加上 10


再次假设，T1 中途失败了，将会发生什么。如果 T1 在第四步：T1 给 B 加上 10 时失败了，而此时 T2 已经修改完了 A 和 B；被改变的数据无法恢复到 T1 执行之前的状态，导致了数据库产生了不合法的状态。 这就是有名的 ”write-write failure” 失败，由于两个事物试图同时修改同一个数据块。 在一个典型的系统中，这个问题可以解决。通过取消失败的事物 T1 ，从而使数据库恢复到上次的合法状态，然后重新开始执行被中断的事物 T2 。


## 违反持久性


假设一个事物从 A 中减去 10 加到 B 中。首先，事物会从 A 中减去 10 ，然后再给 B 加上 10 。 此时，执行事物的程序会告诉用户，事物已经被成功执行了。然而，此时这些被改变的数据仍然还躺在磁盘缓冲区中排队等待被写入磁盘。如果这时主机发生断电，数据库中所有的改变就会丢失。然而，用户还以为所有的改变都已经被持久化到磁盘中了。


# 实现


处理一个事物通常需要一系列的操作，每个操作失败了都会导致整个事物的失败，因此，造成事物失败的原因有好多个。例如，系统的磁盘空间已经满了，或者是执行事物的用户已经用光了操作系统分配给它的 CPU 时间片。有两种大家都很熟悉的流行技术：预写式日志记录和影子分页。这两种技术中，必须要在将被更新的所有信息上获取锁。获取的锁依赖事物的隔离级别，有可能所有的数据仅仅是被读取，仍然需要获取锁。在预写式日志记录技术中，在改变数据库之前通过复制原始的（未改变的）数据到日志记录中来保证原子性。有了日志记录就可以使数据库恢复到发生奔溃事件之前的一致性状态。在影子分页技术中，更新被应用到数据库的部分拷贝中，当数据库事物提交时，新的拷贝才被激活。


## 锁和多版本


好多数据库依赖锁来实现 ACID 能力。锁意味着事物需要在其需要访问的数据上打个标记，这样一来数据库管理系统就会知道这些数据在该事物完成（事物成功或失败）之前不允许其他事物修改这些被打了标记的数据。锁在数据被处理之前必须获取到，也包括那些只会被读取但不会被修改的数据也要获取锁。非平常事物通常需要大量锁，导致了可观的性能开销同时也阻塞了其他事物。例如，用户 A 正在执行一个事物，需要读取另外一个用户 B 想要修改的一行数据。用户 B 必须等到用户 A 的事物彻底完成。通常通过两个阶段锁来保证全隔离性。


除了锁之外还有一种技术是多版本并发控制。在多版本并发控制技术中，数据库给每一个读事物都提供了优先级，未改变的数据版本将会被另外一个活动事物修改（这一句话没看懂，翻译出来后我自己也不理解，以后会读相关的文章，理解了后会更正）。这允许读事物不需要获取锁，写事物不会阻塞读事物。回到之前的例子，当用户 A 正在执行的事物用到了用户 B 将要修改的数据。数据库会提供给 A 用户所需要数据的一个版本，这个版本的数据是用户 B 执行事物之前已经存在的一个版本。用户 A 获取到了具有一致性的数据库的一个视图即使其他用户正在修改数据。一个实现，即快照隔离，解放了隔离性。


 








