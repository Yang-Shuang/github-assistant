# Concurrent Ruby

[![Gem Version](https://badge.fury.io/rb/concurrent-ruby.svg)](http://badge.fury.io/rb/concurrent-ruby)
[![License](https://img.shields.io/badge/license-MIT-green.svg)](http://opensource.org/licenses/MIT)
[![Gitter chat](https://img.shields.io/badge/IRC%20(gitter)-devs%20%26%20users-brightgreen.svg)](https://gitter.im/ruby-concurrency/concurrent-ruby)

适用于 Ruby 的现代并发工具。灵感来源于
[Erlang](http://www.erlang.org/doc/reference_manual/processes.html)、
[Clojure](http://clojure.org/concurrent_programming)、
[Scala](http://akka.io/)、
[Haskell](http://www.haskell.org/haskellwiki/Applications_and_libraries/Concurrency_and_parallelism#Concurrent_Haskell)、
[F#](http://blogs.msdn.com/b/dsyme/archive/2010/02/15/async-and-parallel-design-patterns-in-f-part-3-agents.aspx)、
[C#](http://msdn.microsoft.com/en-us/library/vstudio/hh191443.aspx)、
[Java](http://docs.oracle.com/javase/7/docs/api/java/util/concurrent/package-summary.html)
以及经典的并发模式。

<img src="https://raw.githubusercontent.com/ruby-concurrency/concurrent-ruby/master/docs-source/logo/concurrent-ruby-logo-300x300.png" align="right" style="margin-left: 20px;" />

本 gem 的设计目标如下：

*   作为一个“中立（unopinionated）”的工具箱，提供实用的工具函数，而不争论哪种方案更好或为什么
*   保持无外部 gem 依赖
*   忠于提供灵感的语言的精神
*   但以符合 Ruby 的方式实现
*   尽可能保持语义的 Ruby 风格（Idiomatic）
*   支持在 Ruby 中有意义的特性
*   排除在 Ruby 中无意义的特性
*   保持小巧、精简且松耦合
*   线程安全（Thread-safe）
*   向后兼容

## Contributing

**本 gem 依赖于社区贡献，我们非常感谢你的帮助。** 想要参与贡献吗？太好了！请查看 [带有 `looking-for-contributor` 标签的 issue](https://github.com/ruby-concurrency/concurrent-ruby/issues?q=is%3Aissue+is%3Aopen+label%3Alooking-for-contributor)。如果你认领了某个任务，请在该 issue 下告知我们。

你也可以从整理 issue 开始，这可能包括复现 bug 报告或询问关键信息（如版本号或复现步骤）。如果你想开始处理 issue，一个简单的方法是 [订阅 CodeTriage 上的 concurrent-ruby](https://www.codetriage.com/ruby-concurrency/concurrent-ruby)。 [![Open Source Helpers](https://www.codetriage.com/ruby-concurrency/concurrent-ruby/badges/users.svg)](https://www.codetriage.com/ruby-concurrency/concurrent-ruby)

## Thread Safety

*Concurrent Ruby 提供了所有 Ruby 并发库中最强的线程安全保证之一，在所有三种主要 Ruby 解释器（MRI/CRuby、JRuby、TruffleRuby）上均提供一致的行为和保证。*

本库中的每个抽象都是线程安全的。具体的线程安全保证会在每个抽象的文档中说明。

然而，必须牢记的是，Ruby 是一门基于可变引用的语言。*任何* Ruby 并发库都无法阻止用户犯下线程安全错误（例如在多个线程间共享可变对象并在两个线程中修改它），或因锁使用不当而创建死锁。库能做的只是提供鼓励安全实践的安全抽象。Concurrent Ruby 提供了比其他任何 Ruby 库更多的安全并发抽象，其中许多都支持“**不要通过共享内存来通信；相反，应通过通信来共享内存**”的理念（https://blog.golang.org/share-memory-by-communicating）。Concurrent Ruby 也是唯一一个提供完整线程安全和不可变变量类型及数据结构套件 的 Ruby 库。

我们还发起了关于文档化 Ruby [内存模型](docs-source/synchronization.md) 的讨论，这将为所有三种主要 Ruby 解释器（MRI/CRuby、JRuby、TruffleRuby）提供一致的行为和保证。

## Features & Documentation

**主要的文档站点是自动生成的 [API 文档](http://ruby-concurrency.github.io/concurrent-ruby/index.html)，它与最新版本同步。** 本 README 基于 master 分支，可能包含尚未发布的新内容。

我们还有 [IRC (Gitter) 频道](https://gitter.im/ruby-concurrency/concurrent-ruby)。

### Versioning

*   `concurrent-ruby` 遵循 [语义化版本控制（Semantic Versioning）](http://semver.org/)
*   `concurrent-ruby-ext` 始终与 `concurrent-ruby` 保持相同版本号
*   `concurrent-ruby-edge` 将始终保持为 0.y.z，因此适用 [第4点](http://semver.org/#spec-item-4) *“主版本号为零 (0.y.z) 表示初始开发阶段。任何内容都可能随时更改。公共 API 不应视为稳定。”* 此外我们额外遵循以下规则：
    *   次版本号递增意味着引入了不兼容的变更
    *   修订号递增仅意味着引入的是兼容变更


#### General-purpose Concurrency Abstractions

*   [Async](http://ruby-concurrency.github.io/concurrent-ruby/master/Concurrent/Async.html):
    一个 Mixin 模块，为类提供简单的异步行为。设计灵感部分来源于 Erlang 的 
    [gen_server](http://www.erlang.org/doc/man/gen_server.html)。
*   [ScheduledTask](http://ruby-concurrency.github.io/concurrent-ruby/master/Concurrent/ScheduledTask.html):
    类似于在未来特定时间执行的 Future。
*   [TimerTask](http://ruby-concurrency.github.io/concurrent-ruby/master/Concurrent/TimerTask.html):
    一个定期唤醒以固定间隔执行任务的线程。
*   [Promises](http://ruby-concurrency.github.io/concurrent-ruby/master/Concurrent/Promises.html):
    统一实现 Future 和 Promise，将之前 `Future`、`Promise`、`IVar`、`Event`、`dataflow`、`Delay` 和部分 `TimerTask` 的功能整合到单一框架中。它广泛使用新的同步层使所有功能**非阻塞（non-blocking）**且**无锁（lock-free）**（`#wait`、`#value` 等明显阻塞操作除外）。同时提供更好的性能。    

#### Thread-safe Value Objects, Structures, and Collections

原本属于已弃用的 `thread_safe` gem 的集合类：

*   [Array](http://ruby-concurrency.github.io/concurrent-ruby/master/Concurrent/Array.html) Ruby 标准 [Array](http://ruby-doc.org/core/Array.html) 的线程安全子类。
*   [Hash](http://ruby-concurrency.github.io/concurrent-ruby/master/Concurrent/Hash.html) Ruby 标准 [Hash](http://ruby-doc.org/core/Hash.html) 的线程安全子类。
*   [Set](http://ruby-concurrency.github.io/concurrent-ruby/master/Concurrent/Set.html) Ruby 标准 [Set](http://ruby-doc.org/stdlib-2.4.0/libdoc/set/rdoc/Set.html) 的线程安全子类。
*   [Map](http://ruby-concurrency.github.io/concurrent-ruby/master/Concurrent/Map.html) 一个类似哈希的对象，在高并发场景下比 `Concurrent::Hash` 具有更好的性能表现。
*   [Tuple](http://ruby-concurrency.github.io/concurrent-ruby/master/Concurrent/Tuple.html) 固定大小的数组，带有支持同步访问（线程安全）的 getter/setter。

受其他语言启发的值对象：

*   [Maybe](http://ruby-concurrency.github.io/concurrent-ruby/master/Concurrent/Maybe.html) 一个线程安全的不可变对象，表示可选值，基于 
    Haskell 的 [Data.Maybe](https://hackage.haskell.org/package/base-4.2.0.1/docs/Data-Maybe.html)。

源自 Ruby 的 [Struct](http://ruby-doc.org/core/Struct.html) 的结构类：

*   [ImmutableStruct](http://ruby-concurrency.github.io/concurrent-ruby/master/Concurrent/ImmutableStruct.html)
    不可变结构体，值在构造时设定且之后无法更改。
*   [MutableStruct](http://ruby-concurrency.github.io/concurrent-ruby/master/Concurrent/MutableStruct.html)
    同步的可变结构体，其值可随时安全地修改。
*   [SettableStruct](http://ruby-concurrency.github.io/concurrent-ruby/master/Concurrent/SettableStruct.html)
    同步的只写一次结构体，其值最多只能设置一次（在构造时或之后的任意时间）。

线程安全变量：

*   [Agent](http://ruby-concurrency.github.io/concurrent-ruby/master/Concurrent/Agent.html): 
    一种管理共享、可变、*异步*独立状态的方式。基于 Clojure 的 
    [Agent](http://clojure.org/agents)。
*   [Atom](http://ruby-concurrency.github.io/concurrent-ruby/master/Concurrent/Atom.html): 
    一种管理共享、可变、*同步*独立状态的方式。基于 Clojure 的 
    [Atom](http://clojure.org/atoms)。
*   [AtomicBoolean](http://ruby-concurrency.github.io/concurrent-ruby/master/Concurrent/AtomicBoolean.html)
    可原子更新的布尔值。
*   [AtomicFixnum](http://ruby-concurrency.github.io/concurrent-ruby/master/Concurrent/AtomicFixnum.html)
    可原子更新数值。
*   [AtomicReference](http://ruby-concurrency.github.io/concurrent-ruby/master/Concurrent/AtomicReference.html)
    可原子更新的对象引用。
*   [Exchanger](http://ruby-concurrency.github.io/concurrent-ruby/master/Concurrent/Exchanger.html)
    线程可以配对并交换元素的同步点。基于 Java 的 [Exchanger](http://docs.oracle.com/javase/7/docs/api/java/util/concurrent/Exchanger.html)。
*   [MVar](http://ruby-concurrency.github.io/concurrent-ruby/master/Concurrent/MVar.html) 
    一个同步的单元素容器。基于 Haskell 的 
    [MVar](https://hackage.haskell.org/package/base-4.8.1.0/docs/Control-Concurrent-MVar.html) 和 
    Scala 的 [MVar](http://docs.typelevel.org/api/scalaz/nightly/index.html#scalaz.concurrent.MVar$)。
*   [ThreadLocalVar](http://ruby-concurrency.github.io/concurrent-ruby/master/Concurrent/ThreadLocalVar.html)
    一个值因线程而异的变量。
*   [TVar](http://ruby-concurrency.github.io/concurrent-ruby/master/Concurrent/TVar.html) 
    实现软件事务内存（STM）的事务性变量。基于 Clojure 的 
    [Ref](http://clojure.org/refs)。

#### Java-inspired ThreadPools and Other Executors

*   请参阅 [线程池](http://ruby-concurrency.github.io/concurrent-ruby/master/file.thread_pools.html)
    概述，其中还包含其他可用执行器的列表。

#### Thread Synchronization Classes and Algorithms

*   [CountDownLatch](http://ruby-concurrency.github.io/concurrent-ruby/master/Concurrent/CountDownLatch.html)
    允许一个线程等待多个其他线程的同步对象。
*   [CyclicBarrier](http://ruby-concurrency.github.io/concurrent-ruby/master/Concurrent/CyclicBarrier.html)
    一种同步辅助工具，允许一组线程互相等待到达公共屏障点。
*   [Event](http://ruby-concurrency.github.io/concurrent-ruby/master/Concurrent/Event.html) 
    传统内核风格的事件。
*   [ReadWriteLock](http://ruby-concurrency.github.io/concurrent-ruby/master/Concurrent/ReadWriteLock.html)
    支持多读单写的锁。
*   [ReentrantReadWriteLock](http://ruby-concurrency.github.io/concurrent-ruby/master/Concurrent/ReentrantReadWriteLock.html)
    具有可重入和升级功能的读写锁。
*   [Semaphore](http://ruby-concurrency.github.io/concurrent-ruby/master/Concurrent/Semaphore.html)
    基于计数的许可机制锁。
*   [AtomicMarkableReference](http://ruby-concurrency.github.io/concurrent-ruby/master/Concurrent/AtomicMarkableReference.html)

#### Deprecated

已弃用的功能仍可用且正在修复 bug，但不会添加新功能。
  
*   ~~[Future](http://ruby-concurrency.github.io/concurrent-ruby/master/Concurrent/Future.html):
    产生值的异步操作。~~ Replaced by 
    [Promises](http://ruby-concurrency.github.io/concurrent-ruby/master/Concurrent/Promises.html)。
    *   ~~[.dataflow](http://ruby-concurrency.github.io/concurrent-ruby/master/Concurrent.html#dataflow-class_method):
        基于 Future，Dataflow 允许你创建一个任务，当所有数据依赖项就绪时调度执行。~~ Replaced by 
        [Promises](http://ruby-concurrency.github.io/concurrent-ruby/master/Concurrent/Promises.html)。
*   ~~[Promise](http://ruby-concurrency.github.io/concurrent-ruby/master/Concurrent/Promise.html): Similar
    to Futures, with more features.~~ Replaced by 
    [Promises](http://ruby-concurrency.github.io/concurrent-ruby/master/Concurrent/Promises.html)。
*   ~~[Delay](http://ruby-concurrency.github.io/concurrent-ruby/master/Concurrent/Delay.html) Lazy evaluation
    of a block yielding an immutable result. Based on Clojure's 
    [delay](https://clojuredocs.org/clojure.core/delay).~~ Replaced by 
    [Promises](http://ruby-concurrency.github.io/concurrent-ruby/master/Concurrent/Promises.html)。
*   ~~[IVar](http://ruby-concurrency.github.io/concurrent-ruby/master/Concurrent/IVar.html) Similar to a
    "future" but can be manually assigned once, after which it becomes immutable.~~ Replaced by 
    [Promises](http://ruby-concurrency.github.io/concurrent-ruby/master/Concurrent/Promises.html)。
    
### Edge Features

这些功能在 `concurrent-ruby-edge` 配套 gem 中提供。

这些功能处于积极开发阶段，可能会频繁变更。它们不保证向后兼容（也可能缺少测试和文档）。但仍会遵循语义化版本控制。最终稳定后，`concurrent-ruby-edge` 中的特性预计将迁移至
`concurrent-ruby`。

*   [Actor](http://ruby-concurrency.github.io/concurrent-ruby/master/Concurrent/Actor.html): Implements
    the Actor Model, where concurrent actors exchange messages.
    *Status: Partial documentation and tests; depends on new future/promise framework; stability is good.*
*   [Channel](http://ruby-concurrency.github.io/concurrent-ruby/master/Concurrent/Channel.html):
    通信顺序进程（[CSP](https://en.wikipedia.org/wiki/Communicating_sequential_processes)）。
    功能上等同于 Go [channels](https://tour.golang.org/concurrency/2)，并额外受 Clojure 
    [core.async](https://clojure.github.io/core.async/) 启发。
    *Status: Partial documentation and tests.*
*   [LazyRegister](http://ruby-concurrency.github.io/concurrent-ruby/master/Concurrent/LazyRegister.html)
*   [LockFreeLinkedSet](http://ruby-concurrency.github.io/concurrent-ruby/master/Concurrent/Edge/LockFreeLinkedSet.html)
    *Status: will be moved to core soon.*
*   [LockFreeStack](http://ruby-concurrency.github.io/concurrent-ruby/master/Concurrent/LockFreeStack.html)
    *Status: missing documentation and tests.*
*   [Promises::Channel](http://ruby-concurrency.github.io/concurrent-ruby/master/Concurrent/Promises/Channel.html)
    一个先进先出（FIFO）通道，使用 push 系列方法接收消息，使用 pop 系列方法返回消息。
    Pop 和 push 操作可以表示为 futures，参见 `#pop_op` 和 `#push_op`。
    可通过 `#initialize` 中的 capacity 选项限制通道容量以支持反压（back pressure）。
    如果通道中没有消息，`#pop` 方法会阻塞，而 `#pop_op` 返回待处理的 future。
    如果容量受限，`#push` 方法会阻塞，而 `#push_op` 返回待处理的 future。
*   [Cancellation](http://ruby-concurrency.github.io/concurrent-ruby/master/Concurrent/Cancellation.html)
    Cancellation 抽象提供协作式取消机制。

    Ruby 中标准的 `Thread#raise` 和 `Thread#kill` 方法非常危险（详见下方链接的博客文章）。
    因此 concurrent-ruby 提供了替代方案。
    
    *   <https://jvns.ca/blog/2015/11/27/why-rubys-timeout-is-dangerous-and-thread-dot-raise-is-terrifying/>
    *   <http://www.mikeperham.com/2015/05/08/timeout-rubys-most-dangerous-api/>
    *   <http://blog.headius.com/2008/02/rubys-threadraise-threadkill-timeoutrb.html>

    它提供一个表示可执行任务的对象，任务需获取该对象的引用并定期协作检查是否已被取消。
    使任务支持取消的良好实践：
    *   在执行大量工作的循环中，每个周期都检查取消状态；
    *   将所有阻塞操作放在带超时的循环中，超时后检查取消状态，若未取消则再次以相同超时时间阻塞 
*   [Throttle](http://ruby-concurrency.github.io/concurrent-ruby/master/Concurrent/Throttle.html)
    管理任务并发级别的工具。
*   [ErlangActor](http://ruby-concurrency.github.io/concurrent-ruby/master/Concurrent/ErlangActor.html)
    精确匹配 Erlang actor 行为的 Actor 实现。 
    需要至少 Ruby 2.1，否则不会加载。
*   [WrappingExecutor](http://ruby-concurrency.github.io/concurrent-ruby/master/Concurrent/WrappingExecutor.html) 
    委托执行器，在将任务交给目标执行器之前修改每个任务。

## Supported Ruby versions

* MRI 2.3 and above
* Latest JRuby 9000
* Latest TruffleRuby

## Usage

只需 require 即可加载本 gem 中的所有功能：

```ruby
require 'concurrent'
```

从 concurrent-ruby 1.2.0 开始，你也可以按需引入特定的抽象（[参见公共文档](https://ruby-concurrency.github.io/concurrent-ruby/master/index.html)），例如：
```ruby
require 'concurrent/map'
require 'concurrent/atomic/atomic_reference'
require 'concurrent/executor/fixed_thread_pool'
```

要使用 Edge gem 中的工具，需单独 require：

```ruby
require 'concurrent-edge'
```

如果库的行为不符合预期，可调用 `Concurrent.use_simple_logger(:DEBUG)` 来排查问题。

## Installation

```shell
gem install concurrent-ruby
```

或在 Gemfile 中添加以下行：

```ruby
gem 'concurrent-ruby', require: 'concurrent'
```

然后在终端运行 `bundle install`。

### Edge Gem Installation

Edge gem 需与核心 gem 分开安装：

```shell
gem install concurrent-ruby-edge
```

或在 Gemfile 中添加以下行：

```ruby
gem 'concurrent-ruby-edge', require: 'concurrent-edge'
```

然后在终端运行 `bundle install`。


### C Extensions for MRI

在 MRI 下安装可选的 C 扩展可获得潜在的性能提升。为最小化安装错误，C 扩展提供在 `concurrent-ruby-ext` 
扩展 gem 中。`concurrent-ruby` 和 `concurrent-ruby-ext` 始终同步发布且版本号相同。只需同时安装该扩展 gem：

```ruby
gem install concurrent-ruby-ext
```

或在 Gemfile 中添加以下行：

```ruby
gem 'concurrent-ruby-ext'
```

然后在终端运行 `bundle install`。

在代码中只需引入

```ruby
require 'concurrent'
```

`concurrent-ruby` gem 将自动检测 `concurrent-ruby-ext` gem 的存在并加载相应的 C 扩展。

#### Note For gem developers

任何 gem 都不应依赖 `concurrent-ruby-ext`。这样做会强制你的用户使用 C 扩展。最佳实践是仅依赖 `concurrent-ruby`，由用户自行决定是否安装 C 扩展。

## Building the gem

### Requirements

* Recent CRuby
* JRuby, `rbenv install jruby-9.2.17.0`
* Set env variable `CONCURRENT_JRUBY_HOME` to point to it, e.g. `/usr/local/opt/rbenv/versions/jruby-9.2.17.0`
* Install Docker or Podman, required for Windows builds
* If `bundle config get path` is set, use `bundle config set --local path.system true` otherwise the `gem name, path: '.'` gems won't be found (Bundler limitation).

### Publishing the Gem

* Update `version.rb`
* Update the CHANGELOG
* Add the new version to `docs-source/signpost.md`. Needs to be done only if there are visible changes in the documentation.
* Commit (and push) the changes.
* Use `bundle exec rake release` to release the gem.
  It consists of `['release:checks', 'release:build', 'release:test', 'release:publish']` steps.
  It will ask at the end before publishing anything. Steps can also be executed individually.

## Maintainers

* [Benoit Daloze](https://github.com/eregon)
* [Matthew Draper](https://github.com/matthewd)
* [Rafael França](https://github.com/rafaelfranca)
* [Charles Oliver Nutter](https://github.com/headius)
* [Ben Sheldon](https://github.com/bensheldon)
* [Samuel Williams](https://github.com/ioquatix)
* [Joshua Young](https://github.com/joshuay03)

### Special Thanks to

* [Jerry D'Antonio](https://github.com/jdantonio) for creating the gem
* [Brian Durand](https://github.com/bdurand) for the `ref` gem
* [Charles Oliver Nutter](https://github.com/headius) for the `atomic` and `thread_safe` gems
* [thedarkone](https://github.com/thedarkone) for the `thread_safe` gem

**历任维护者（Past Maintainers）**

* [Chris Seaton](https://github.com/chrisseaton)
* [Petr Chalupa](https://github.com/pitr-ch)
* [Michele Della Torre](https://github.com/mighe)
* [Paweł Obrok](https://github.com/obrok)
* [Lucas Allan](https://github.com/lucasallan)

以及向 [Ruby 协会（Ruby Association）](https://www.ruby.or.jp/en/) 致谢，感谢其在 2018 年赞助了“[增强 Ruby 并发工具链](https://www.ruby.or.jp/en/news/20181106)”项目。 

## License and Copyright

*Concurrent Ruby* is free software released under the 
[MIT License](http://www.opensource.org/licenses/MIT).

The *Concurrent Ruby* [logo](https://raw.githubusercontent.com/ruby-concurrency/concurrent-ruby/master/docs-source/logo/concurrent-ruby-logo-300x300.png) was
designed by [David Jones](https://twitter.com/zombyboy). It is Copyright &copy; 2014 
[Jerry D'Antonio](https://twitter.com/jerrydantonio). All Rights Reserved.