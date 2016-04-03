可以泛化 Java 集合 API 中的各种 Collection 和 Map 类型及其子类型。本文不会覆盖泛型的细节。Java 泛型会在 Java 泛型教程系列中讲。

可以这样来泛化集合接口：

    Collection<String> stringCollection = new HashSet<String>();

现在 stringCollection 只能包含 String 类型的实例。如果尝试添加其他的类型，或者是集合中的元素强制转换为非 String 类型的任意类型（当然，把 String 类型强制转换为 String 类型的父类是可以的，比如强制转换为 Object 类型），编译器都是不允许的。
事实上，也可以欺骗编译器，在 stringCollection 中插入除了 String 类型之外的其他类型的实例，不过不推荐这样做。
可以使用 for-each 循环来迭代上面的集合：

    Collection<String> stringCollection = new HashSet<String>();

    for (String stringElement : stringCollection) {
        // 对 stringElement 做一些事
    }

也可以对 list、set 中的元素做同样的事。
在这里不会对泛型做深入的探讨，正如我在最开始时说的，我有一个单独的 Java 泛型教程。另外，在特定的泛型类型中会列举更多的例子。
