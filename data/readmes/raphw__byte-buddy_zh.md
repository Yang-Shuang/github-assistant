# Byte Buddy
==========

<a href="https://bytebuddy.net">
<img src="https://raw.githubusercontent.com/raphw/byte-buddy/gh-pages/images/logo-bg.png" alt="Byte Buddy logo" height="180px" align="right" />
</a>

用于 Java 虚拟机的运行时代码生成

[![Actions Status](https://github.com/raphw/byte-buddy/workflows/CI/badge.svg)](https://github.com/raphw/byte-buddy/actions)
[![Security Score](https://snyk-widget.herokuapp.com/badge/mvn/net.bytebuddy/byte-buddy/badge.svg)](https://snyk.io/test/github/raphw/byte-buddy)
[![Coverage Status](https://img.shields.io/coveralls/raphw/byte-buddy/master.svg)](https://coveralls.io/r/raphw/byte-buddy?branch=master)
[![Maven Central](https://img.shields.io/maven-central/v/net.bytebuddy/byte-buddy)](https://central.sonatype.com/artifact/net.bytebuddy/byte-buddy)
[![CII Best Practices](https://bestpractices.coreinfrastructure.org/projects/6251/badge)](https://bestpractices.coreinfrastructure.org/projects/6251)

Byte Buddy 是一个用于在 Java 应用程序运行期间创建和修改 Java 类的代码生成与操作库，且无需编译器协助。与 [Java 类库自带的](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Proxy.html) 代码生成工具不同，Byte Buddy 允许创建任意类，而不仅限于为实现接口以创建运行时代理（proxy）。此外，Byte Buddy 提供了便捷的 API，支持通过手动方式、Java agent 或在构建过程中更改类。

Java version compatibility
==========================

下表列出了 Byte Buddy 在无需实验性支持的情况下，为特定 Java class file version（class 文件版本）提供稳定支持所需的最低版本。Byte Buddy 支持的最低 Java 版本为 Java 5，而任何更早版本的 class 文件均可被转换。自 1.17.0 起，除非发现此前未知的 class 文件特性，否则 Byte Buddy 将持续支持新的 Java 版本。这得益于 Byte Buddy 对 Class File API 的支持。 

| Byte Buddy version | Supported Java version | Minimum JVM version |
|--------------------|------------------------|---------------------|
| 1.18.7             | 25+                    | 8                   |
| 1.18.7-jdk5        | 25+                    | 5                   |
| 1.17.0             | 25+                    | 5                   |
| 1.15.4             | 24                     | 5                   |
| 1.14.12            | 23                     | 5                   |
| 1.14.8             | 22                     | 5                   |
| 1.14.3             | 21                     | 5                   |
| 1.12.18            | 20                     | 5                   |
| 1.12.9             | 19                     | 5                   |
| 1.11.6             | 18                     | 5                   |
| 1.10.19            | 17                     | 5                   |

Usage
=====

使用 Byte Buddy 无需理解 Java byte code（字节码）或 [class file format](https://docs.oracle.com/javase/specs/jvms/se8/html/jvms-4.html)。相反，Byte Buddy 的 API 旨在让代码简洁易懂。尽管如此，Byte Buddy 仍支持完全自定义，甚至允许定义自定义 byte code。此外，API 设计尽可能不具侵入性，因此 Byte Buddy 不会在生成的类中留下任何痕迹。正因如此，生成的类无需将 Byte Buddy 置于 class path 即可运行。这也是为什么 Byte Buddy 的吉祥物被选为幽灵的原因。

Byte Buddy 基于 Java 5 编写，但支持生成任意 Java 版本的类。Byte Buddy 是一个轻量级库，仅依赖于 Java byte code 解析器库 [ASM](https://asm.ow2.io/) 的 visitor API，而 ASM 本身[无需任何额外依赖](https://repo1.maven.org/maven2/org/ow2/asm/asm/5.0.4/asm-5.0.4.pom)。

乍看之下，运行时代码生成似乎是一种应避免的“黑魔法”，只有少数开发者会在应用运行期间显式生成代码。然而，当创建需要与任意代码和编译时未知的类型进行交互的库时，情况就会发生变化。在此场景下，库实现者通常需要在要求用户实现库专属接口与在用户类型首次被库识别时在运行时生成代码之间做出选择。许多知名库（例如 *Spring* 或 *Hibernate*）都选择了后者，这种使用 [*Plain Old Java Objects (POJO)*](https://en.wikipedia.org/wiki/Plain_Old_Java_Object) 的方法深受用户喜爱。因此，代码生成已成为 Java 生态中无处不在的概念。Byte Buddy 旨在革新 Java 类型的运行时创建方式，为依赖代码生成的开发者提供更优的工具集。

___

<a href="https://bytebuddy.net">
<img src="https://raw.githubusercontent.com/raphw/byte-buddy/gh-pages/images/dukeschoice.jpg" alt="Duke's Choice award" height="110px" align="left" />
</a>

2015年10月，Byte Buddy 荣获 Oracle 颁发的 [*Duke's Choice award*](https://www.oracle.com/corporate/pressrelease/dukes-award-102815.html)。该奖项表彰了 Byte Buddy “在 Java 技术领域做出的巨大创新”。我们深感荣幸能获得此奖，并感谢所有用户及帮助 Byte Buddy 取得今日成就的每一个人。非常感谢大家的支持！

___

Byte Buddy 在生产环境中提供卓越的性能。它稳定可靠，被 [Mockito](https://site.mockito.org/)、[Hibernate](https://hibernate.org/)
、[Jackson](https://github.com/FasterXML/jackson)、Google 的 [Bazel 构建系统](https://bazel.build/)
以及[众多其他项目](https://github.com/raphw/byte-buddy/wiki/Projects-using-Byte-Buddy)等知名框架和工具所采用。Byte Buddy 也被大量商业产品广泛使用，效果显著。目前其年下载量超过 7500 万次。

Hello World
-----------

使用 Byte Buddy 实现 *Hello World* 非常简单。任何 Java 类的创建都始于 `ByteBuddy` 类的一个实例，该实例代表用于创建新类型的配置：

```java
Class<?> dynamicType = new ByteBuddy()
  .subclass(Object.class)
  .method(ElementMatchers.named("toString"))
  .intercept(FixedValue.value("Hello World!"))
  .make()
  .load(getClass().getClassLoader())
  .getLoaded();
assertThat(dynamicType.newInstance().toString(), is("Hello World!"));
```

上述示例中使用的默认 `ByteBuddy` 配置会在处理该代码的 Java 虚拟机所能理解的最新 class file format（class 文件格式）下创建一个 Java 类。从示例代码中可以明显看出，生成的类型将继承自 `Object` 类并重写其 `toString` 方法，该方法应返回固定值 `Hello World!`。待重写的方法通过所谓的 `ElementMatcher` 进行识别。在上述示例中，使用了预定义的元素匹配器 `named(String)`，它通过精确的类名来识别方法。Byte Buddy 内置了大量经过充分测试的预定义匹配器，它们被收集在 `ElementMatchers` 类中且易于组合使用。当然，自定义匹配器的实现同样简单，只需实现 ([functional](https://docs.oracle.com/javase/8/docs/api/java/lang/FunctionalInterface.html)) `ElementMatcher` 接口即可。

为了实现 `toString` 方法，`FixedValue` 类为被重写的方法定义了一个常量返回值。定义常数值只是 Byte Buddy 附带的大量方法拦截器（interceptor）中的一个示例。通过实现 `Implementation` 接口，甚至可以完全使用自定义 byte code 来定义方法。

最后，描述的 Java 类会被创建并加载到 Java 虚拟机中。为此需要指定一个目标 class loader（类加载器）。最终，我们可以通过调用生成类的实例的 `toString` 方法来验证结果，确认其返回值符合我们预期的常数值。

A more complex example
----------------------

当然，*Hello World 示例*对于评估代码生成库的质量来说过于简单。在实际使用中，你通常希望执行更复杂的操作，例如在 Java 程序的执行路径中引入钩子（hook）。使用 Byte Buddy 实现这些同样非常简单。以下示例展示了如何拦截方法调用。

Byte Buddy 通过 `Implementation` 接口的实例来表达动态定义的方法实现。在前面的示例中，已经演示了实现了该接口的 `FixedValue`。通过实现此接口，Byte Buddy 的用户甚至可以自定义方法的 byte code。不过，通常使用 Byte Buddy 的预定义实现（如 `MethodDelegation`）会更加容易，它允许使用纯 Java 代码实现任意方法。使用该实现的流程非常直观，因为它通过将控制流委托给任何 POJO 来工作。作为此类 POJO 的一个示例，Byte Buddy 可以将调用重定向到以下类的唯一方法：

```java
public class GreetingInterceptor {
  public Object greet(Object argument) {
    return "Hello from " + argument;
  }
}
```

请注意，上述 `GreetingInterceptor` 不依赖任何 Byte Buddy 类型。这是一个好消息，因为 Byte Buddy 生成的所有类都不需要在 class path 中包含 Byte Buddy！给定上述 `GreetingInterceptor`，我们可以使用 Byte Buddy 来实现 Java 8 的 `java.util.function.Function` 接口及其抽象 `apply` 方法：

```java
Class<? extends java.util.function.Function> dynamicType = new ByteBuddy()
  .subclass(java.util.function.Function.class)
  .method(ElementMatchers.named("apply"))
  .intercept(MethodDelegation.to(new GreetingInterceptor()))
  .make()
  .load(getClass().getClassLoader())
  .getLoaded();
assertThat((String) dynamicType.newInstance().apply("Byte Buddy"), is("Hello from Byte Buddy"));
```

执行上述代码后，Byte Buddy 实现了 Java 的 `Function` 接口，并将 `apply` 方法的实现委托给我们之前定义的 `GreetingInterceptor` POJO 实例。现在，每当调用 `Function::apply` 方法时，控制流就会被分发到 `GreetingInterceptor::greet`，并返回后者的返回值。

可以通过注解拦截器参数来定义接受更通用输入和输出的拦截器。当 Byte Buddy 发现此类注解时，库会自动注入拦截器参数所需的依赖项。以下是一个更通用的拦截器示例：

```java
public class GeneralInterceptor {
  @RuntimeType
  public Object intercept(@AllArguments Object[] allArguments,
                          @Origin Method method) {
    // intercept any method of any signature
  }
}
```

使用上述拦截器，可以匹配和处理任何被拦截的方法。例如，在匹配 `Function::apply` 时，方法的参数将作为数组的单个元素传入。此外，由于使用了 `@Origin` 注解，对 `Fuction::apply` 的 `Method` 引用会作为拦截器的第二个参数传入。通过在方法上声明 `@RuntimeType` 注解，Byte Buddy 最终会在必要时将返回值强制转换为被拦截方法的返回类型。在此过程中，Byte Buddy 还会自动应用装箱和拆箱操作。

除了已提到的注解外，还存在大量其他预定义注解。例如，在 `Runnable` 或 `Callable` 类型上使用 `@SuperCall` 注解时，Byte Buddy 会注入代理实例，允许调用非抽象的父类方法（如果存在）。即使 Byte Buddy 未覆盖某个用例，它也提供了扩展机制用于定义自定义注解。

你可能会认为使用这些注解会将代码绑定到 Byte Buddy。然而，Java 会在 class loader 无法识别注解时忽略它们。这样，生成的代码仍然可以在没有 Byte Buddy 的情况下运行！你可以在 `MethodDelegation` 的 *javadoc* 和 Byte Buddy 教程中找到更多关于它及其所有预定义注解的信息。

Changing existing classes
----------------------

Byte Buddy 不仅限于创建子类，还能够重新定义现有代码。为此，Byte Buddy 提供了便捷的 API 用于定义所谓的 [Java agents](https://docs.oracle.com/javase/8/docs/api/java/lang/instrument/package-summary.html)。Java agent（代理）是普通的 Java 程序，可用于在应用运行期间修改现有 Java 应用的代码。例如，我们可以使用 Byte Buddy 来更改方法以打印其执行时间。为此，我们首先定义一个与前面示例中类似的拦截器：

```java
public class TimingInterceptor {
  @RuntimeType
  public static Object intercept(@Origin Method method, 
                                 @SuperCall Callable<?> callable) {
    long start = System.currentTimeMillis();
    try {
      return callable.call();
    } finally {
      System.out.println(method + " took " + (System.currentTimeMillis() - start));
    }
  }
}
```

使用 Java agent，我们现在可以将此拦截器应用于所有匹配 `TypeDescription`（类型描述）的 `ElementMatcher` 的类型。在本例中，我们选择将上述拦截器添加到名称以 `Timed` 结尾的所有类中。这样做是为了演示简便起见，而在生产环境中，使用注解来标记此类类可能更为合适。借助 Byte Buddy 的 `AgentBuilder` API，创建 Java agent 就像定义以下代理类一样简单：

```java
public class TimerAgent {
  public static void premain(String arguments, 
                             Instrumentation instrumentation) {
    new AgentBuilder.Default()
      .type(ElementMatchers.nameEndsWith("Timed"))
      .transform((builder, type, classLoader, module, protectionDomain) -> 
          builder.method(ElementMatchers.any())
                 .intercept(MethodDelegation.to(TimingInterceptor.class))
      ).installOn(instrumentation);
  }
}
```

与 Java 的 `main` 方法类似，`premain` 方法是任何 Java agent 的入口点，我们在此处应用重定义操作。Java agent 会接收一个 `Instrumentation` 接口的实例作为参数之一，该接口允许 Byte Buddy 挂钩到 JVM 的标准 API 以实现运行时类重新定义。

此程序需与包含指向 `TimerAgent` 的 [`Premain-Class` 属性](https://docs.oracle.com/javase/8/docs/api/java/lang/instrument/package-summary.html) 的 manifest（清单）文件一起打包。生成的 *jar* 文件现在可以通过设置 `-javaagent:timingagent.jar` 添加到任何 Java 应用中，类似于将 jar 添加到 class path。启用 agent 后，所有以 `Timed` 结尾的类都会向控制台打印其执行时间。

Byte Buddy 还能够通过禁用 class file format（class 文件格式）更改并使用 `Advice` instrumentation（插装）来应用所谓的运行时附件（runtime attachments）。有关更多信息，请参阅 `Advice` 和 `AgentBuilder` 类的 *javadoc*。Byte Buddy 还可通过 `ByteBuddy` 实例或 Byte Buddy *Maven* 和 *Gradle* 插件显式更改 Java 类。

Where to go from here?
----------------------

Byte Buddy 是一个功能全面的库，我们仅触及了其能力的一小部分。不过，Byte Buddy 旨在通过提供用于创建类的领域特定语言（DSL）来确保易用性。大多数运行时代码生成只需编写可读的代码即可完成，无需任何关于 Java class file format（class 文件格式）的知识。如果你想了解更多关于 Byte Buddy 的内容，可以在 [Byte Buddy 官网的教程](https://bytebuddy.net/#/tutorial) 中找到（此外还有[中文翻译版](https://notes.diguage.com/byte-buddy-tutorial/)）。

此外，Byte Buddy 附带了[详细的代码内文档](https://bytebuddy.net/#/javadoc)和广泛的测试用例覆盖范围，这些也可以作为示例代码参考。最后，你可以在 [wiki](https://github.com/raphw/byte-buddy/wiki/Web-Resources) 中找到关于 Byte Buddy 的最新文章和演讲列表。在使用 Byte Buddy 时，请务必阅读以下有关维护项目依赖的信息。

Getting support
----------------------------

#### Commercial ####

Byte Buddy 的使用是免费的，无需购买许可证。但要充分利用该库或确保轻松上手，你也可以选择购买培训、开发工时或服务计划。费率取决于合作范围与持续时间。如需更多信息，请联系 <rafael.wth@gmail.com>。

#### Tidelift ####

Byte Buddy
已[收录于 Tidelift](https://tidelift.com/subscription/pkg/maven-net-bytebuddy-byte-buddy?utm_source=byte-buddy&utm_medium=referral)
。如果你尚未使用到需要购买显式支持的程度，但希望支持开源社区，请考虑订阅。

#### GitHub sponsors ####

你可以通过 [GitHub Sponsors](https://github.com/sponsors/raphw) 支持我的工作。请注意，此选项仅面向寻求简单支付渠道的商业用户，且不支持换取直接技术支持。通过 GitHub Sponsors 进行的支持无法用于满足增值税（VAT）合规要求。如需直接支持协议，请直接联系我们。

#### Free ####

一般性问题可在 [Stack Overflow](https://stackoverflow.com/questions/tagged/byte-buddy) 或
[Byte Buddy 邮件列表](https://groups.google.com/forum/#!forum/byte-buddy)上提出（该列表也作为问题存档）。当然，即使不在商业计划内，Bug 报告也会得到处理。对于开源项目，有时可以获得额外的帮助以更好地使用 Byte Buddy。

Dependency and API evolution
----------------------------

Byte Buddy 基于 [ASM](https://asm.ow2.io) 构建，ASM 是一个成熟且经过充分测试的用于读写已编译 Java 类的库。为了支持高级类型操作，Byte Buddy 有意将 ASM API 暴露给用户。当然，直接使用 ASM 完全是可选的，大多数用户很可能永远不需要它。做出此选择是为了确保 Byte Buddy 的用户不仅限于其高层功能，而且在必要时可以毫不费力地实现自定义逻辑。

ASM 曾更改过公共 API，但从版本 4 开始增加了 API 兼容性机制。为了避免与这些旧版本发生版本冲突，Byte Buddy 将 ASM 依赖项重新打包到了自己的命名空间中。如果你想直接使用 ASM，`byte-buddy-dep` artifact（构件）提供了显式依赖 ASM 的 Byte Buddy 版本。在使用时，你**必须**同时将 *两者*（Byte Buddy 和 ASM）重新打包到你的命名空间中，以避免版本冲突。

请注意本项目的 [安全策略](https://github.com/raphw/byte-buddy/blob/master/SECURITY.md)。

Byte Buddy 支持在从 Java 5 开始的所有 JVM 版本上运行于单个 jar 中。这是为了简化 Java agent 的开发，因为 agent 通常需要支持未被积极更新的旧版或未知应用。为了同时支持现代 Java 特性（如 CDS 或使用栈映射帧的类验证），Byte Buddy 的主 jar 采用多发行版（multi-release）jar 格式，其中包含版本 5 和版本 8 的 class 文件。因此，Byte Buddy 的 jar 体积比预期要大。通常这不是问题，因为 Byte Buddy 的大部分类永远不会被加载。然而，在分发 Java agent 时，文件大小可能会成为问题。由于 agent 本身需要打包为单个 jar，因此建议移除其中基础的 Java 5 版本或多发行版 Java 8 版本的 class 文件以减小体积。大多数为此目的设计的构建插件（如 [Maven Shade plugin](https://maven.apache.org/plugins/maven-shade-plugin/shade-mojo.html#filters)）均支持此操作。JDK Class File API 的集成包含在版本 24 及更高版本的多发行版文件夹中。这些文件夹可以安全移除，唯一的影响是失去对 Class File API 的支持。

License and development
-----------------------

Byte Buddy 采用宽松且适合商业使用的 [*Apache Licence, Version 2.0*](https://www.apache.org/licenses/LICENSE-2.0.html) 许可证发布，并在 GitHub 上免费提供。此外，*byte-buddy* 发行版捆绑了 ASM，ASM 根据 [3-clause BSD license（BSD 三条款许可证）](https://asm.ow2.io/license.html) 发布。

Byte Buddy 的二进制文件已发布到 Maven Central 和 JCenter 仓库中。自 Byte Buddy 1.10.3 起，构件签名可通过此 [PGP 公钥](https://keys.openpgp.org/search?q=rafael.wth@gmail.com) 进行验证。旧版本可通过[此较旧的证书](https://keyserver.ubuntu.com/pks/lookup?op=get&search=0xf42b96b8648b5c4a1c43a62fbb2914c1fa0811c3) 进行验证。

该项目使用 <a href="https://maven.apache.org/">Maven</a> 构建。在你的终端中，克隆和构建项目的命令大致如下：

```shell
git clone https://github.com/raphw/byte-buddy.git
cd byte-buddy
mvn package
```

执行这些命令后，Byte Buddy 将从 GitHub 克隆并在你的机器上构建。更多构建选项列在根 POM 文件中。Byte Buddy 可以使用任何至少版本为 6 的 JDK 进行构建。但建议使用至少版本为 8 的 JDK，因为版本 6 和 7 的构建设计使用了未加密的 HTTP。这些构建仅用于针对该 JDK 版本运行测试，且可能使你面临中间人攻击（MITM）的风险。因此应避免使用这些构建配置。目前 Byte Buddy 在 CI 服务器上针对 JDK 6 及以上版本进行测试。

请使用 GitHub 的 [issue tracker](https://github.com/raphw/byte-buddy/issues) 报告 Bug。提交代码时，请提供证明你功能正常或展示 Bug 修复的测试用例。此外，请确保你没有破坏任何现有测试用例。如果可能，请花些时间编写相关文档。对于功能请求或一般反馈，你也可以使用
[issue tracker](https://github.com/raphw/byte-buddy/issues) 或在
[我们的邮件列表](https://groups.google.com/forum/#!forum/byte-buddy)上联系我们。

Supporters
----------

Byte Buddy 的开发工作也得益于多位支持者的定期资源与关注投入。请花些时间了解这些支持者及其提供的服务。

<a href="https://www.scienta.no">
<img src="https://bytebuddy.net/logos/scienta.png" height="50" alt="Scienta AS"/> 
</a>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
<a href="https://www.instana.com">
<img src="https://bytebuddy.net/logos/instana.png" height="50" alt="Instana"/>
</a>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
<a href="https://www.sqreen.com">
<img src="https://bytebuddy.net/logos/sqreen.png" height="50" alt="Sqreen"/>
</a>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
<a href="https://www.elastic.co">
<img src="https://bytebuddy.net/logos/elastic.png" height="50" alt="Elastic"/>
</a>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
<a href="https://www.spotify.com">
<img src="https://bytebuddy.net/logos/spotify.png" height="50" alt="Spotify"/>
</a>