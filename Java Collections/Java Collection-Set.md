java.util.Set 是 java.util.Collection 的子接口。Set 代表了对象的集合，意思是每个对象只能在 Set 中出现一次。

下面是内容列表：

- Java Set 例子
- Set 的实现类
- 添加和访问元素
- 移除元素
- 泛型集合
- JavaDoc 中的更多细节

### Java Set 例子
下面是 Java Set 的第一个例子，给大家一个怎么使用 Set 的印象：

    Set setA = new HashSet();
    String element = "element 1";
    setA.add(element);
    System.out.println(setA.contains(element));

在上面的例子中创建了一个 HashSet ，HashSet 是 Java API 中实现了 Set 接口的一个类。然后把一个 String 对象添加到 Set 中，最后检查在 Set 中是否包含刚才被添加的那个元素。

### Set 的实现类
Set 接口是 Collection 接口的子类型，Collection 接口中的所有方法在 Set 接口中都可用。
由于 Set 是接口，所以在使用的时候必须要实例化一个具体的实现。
在 Java 集合 API 中，下面的类都实现了 Set 接口，需要实例化 Set 的时候可以在下面的类中选择：

- java.util.EnumSet
- java.util.HashSet
- java.util.LinkedHashSet
- java.util.TreeSet

每种 Set 的实现类在迭代的时候的元素顺序、插入时间和访问时间（大 O 记法）方面都稍有不同。

HashSet 的背后实质是 HashMap 。HashSet 不保证迭代时返回的元素的顺序。
LinkedHashSet 不同于 HashSet，LinkedHashSet 保证元素在迭代期间的顺序和其在被插入时的顺序是一致的。
重复插入一个元素并不会改变这种顺序。

**************************
TreeSet 也会保证迭代时的顺序，但这个顺序指的是元素的排序的顺序。换句话说，如果对一个



**************************
java.util.concurrent 包中也有 Set 的实现类，并发的使用不在本教程中涉及。
下面是创建 Set 的实例的一些例子：

    Set setA = new EnumSet();
    Set setB = new HashSet();
    Set setC = new LinkedHashSet();
    Set setD = new TreeSet();

### 添加和访问元素
可以调用 add() 方法来往 Set 中添加元素。add() 方法继承 Collecting 接口。
下面是几个例子：

    Set setA = new HashSet();
    set.add("element 1");
    set.add("element 2");
    set.add("element 3");

三次调用 add() 方法，每次调用都会往 Set 中添加一个 String 实例。
当迭代 Set 中的元素时，元素的顺序依赖于 Set 的实现类，这在前面已经提到过了。下面是一个迭代的例子：

    Set setA = new HashSet();

    setA.add("element 1");
    setA.add("element 2");
    setA.add("element 3");

    // 通过 Iterator 访问
    Iterator iterator = setA.iterator();
    while (iterator.hasNext()) {
        String element = (String) iterator.next();
    }

    // 通过 for-each 循环访问
    for (Object object : setA) {
        String element = (String) object;
    }

### 移除元素
可以调用 remove(Object object) 方法来移除元素。在 Set 中没有基于索引的移除方法，这是因为元素的顺序依赖于 Set 的实现类。

### 泛型 Sets
默认，可以往 Set 里存储任何对象，但自从 Java 5 以后，Java 泛型可以限制往 Set 里插入的对象的种类。下面是一个例子：

    Set<MyObject> set = new HashSet<MyObject>();

现在，这个 set 中只可以插入 MyObject 的实例。现在，访问 set 中的元素不需要做强制转换了。下面是代码：

    for (MyObject anObject : set) {
        // 对 anObject 做一些事
    }

想要获取更多的 Java 泛型信息，参见 Java 泛型教程。

### JavaDoc 中的更多细节
还可以对 Set 做很多操作，但得通过查阅 Java 文档来了解细节。本文集中于最常见的两种操作：添加移除元素和迭代元素。


