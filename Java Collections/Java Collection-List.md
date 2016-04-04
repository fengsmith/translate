java.util.List 接口是 java.util.Collection 接口的子类型。List 代表了一组有序的对象，意味着可以以特定的顺序来访问 List 中的元素，也可以通过索引来访问。也可以往 List 中多次添加同一个元素。

### List 的实现
List 是 Collection 的子类型，List 继承了 Collection 的所有方法。
由于 List 是接口，所以在使用的时候必须要实例化一个具体的实现。
在 Java 集合 API 中，下面的类都实现了 List 接口，需要实例化 List 的时候可以在下面的类中选择：

- java.util.ArrayList
- java.util.LinkedList
- java.util.Vector
- java.util.Stack

在 java.util.concurrent 包中也有 List 接口的实现类，并发的使用不在本教程中涉及。
下面是怎样创建 List 实例的例子：

    List listA = new ArrayList();
    List listB = new LinkedList();
    List listC = new Vector();
    List listD = new Stack();

### 添加和访问元素
调用 add() 方法可以往 List 中添加元素。add() 方法继承自 Collection 接口。
下面是几个例子：

    List listA = new ArrayList();

    listA.add("element 1");
    listA.add("element 2");
    listA.add("element 3");

    listA.add(0, "element 0");

前三次的 add() 方法调用每次都往 list 的末尾添加了一个 String 的实例。最后一次调用 add() 方法往 list 的最开始添加了一个 String 的实例。

元素添加时的顺序就是 List 最终存储的顺序，所以可以以同样的顺序来访问元素。可以使用 get(int index) 方法或者是调用 iterator() 方法返回的 Iterator 来访问元素。
下面是代码：

    List listA = new ArrayList();
    listA.add("element 0");
    listA.add("element 1");
    listA.add("element 2");

    // 通过索引访问元素
    String element0 = listA.get(0);
    String element1 = listA.get(1);
    String element2 = listA.get(2);

    // 通过 Iterator 访问
    Iterator iterator = listA.iterator();
    while (iterator.hasNext()) {
        String element = (String) iterator.next();
    }

    // 通过 for-each 循环来访问
    for (Object object : listA) {
        String element = (String) object;
    }

当通过 Iterator 或 for-each（实际上在背后也是使用了 Iterator）迭代 list 时，元素被迭代的顺序和它们在 list 中被存储时的顺序是一致的。

### 移除元素
有两种方式移除元素：

    1、remove(Object element)
    2、remove(int index)

如果 element 在 list 中存在，则 remove(Object element) 方法移除这个元素。list 中所有紧接其后的元素都被向上移动了一个位置。因此，这些被移动的元素的索引都减少了 1 。

remove(int index) 方法移除了给定索引对应的元素。list 中所有紧接其后的元素都被向上移动了一个位置。因此，这些被移动的元素的索引都减少了 1 。

### 清空 List
Java List 接口有一个 clear() 方法，调用 clear() 方法时所有的元素都会被移除的。
下面的这个简单的例子用 clear() 方法清空了 List 。

    List list = new ArrayList();
    list.add("object 1");
    list.add("object 2");

### List 的 size
可以通过调用 size() 方法来获取 list 中元素的数量。下面是一个例子：

    List list = new ArrayList();
    list.add("object 1");
    list.add("object 2");

    int size = list.size();

### 泛型 Lists
默认，可以往 list 里存储任何对象，但自从 Java 5 以后，Java 泛型可以限制往 list 里插入的对象的种类。下面是一个例子：

    List<MyObject> list = new ArrayList<MyObject>();

现在，这个 list 中只可以插入 MyObject 的实例。现在，访问 list 中的元素不需要做强制转换了。下面是代码：

    MyObject myObject = list.get(0);

    for (MyObject anObject : list) {
        // 对 anObject 做一些事
    }

Java 泛型教程中有更多的 Java 泛型信息。

### 迭代 List
有几种不同的方法可以迭代一个 Java List。在这儿我会覆盖三种通用的机制。
第一种方法是使用 Iterator 。下面的例子是用 Iterator() 迭代 List 。

    List list = new ArrayList();
    // 往 list 中添加元素

    Iterator iterator = list.iterator();
    while (iterator.hasNext()) {
        Object next = iterator.next();
    }

可以通过调用 List 接口的 iterator() 方法来获取 Iterator 。
一旦获取到 Iterator 后，可以不断地调用 hasNext() 方法直到返回 false 。可以在 while 循环中调用 hasNext() 。
可以在 while 循环内部调用 Iterator 的 next() 方法来获取 Iterator 下一个指向的元素。
如果在 List 中指定了类型，在循环内部就不需要进行强制类型转换了。下面是一个例子：

    List<String> list = new ArrayList<String>();

    Iterator<String> iterator = list.iterator();
    while (iterator.hasNext()) {
        String obj = iterator.next();
    }

另一种方法是使用在 Java 5 中新增的 for-each 循环来迭代 List 。下面的例子是使用 for-each 循环来迭代 List ：

    List list = new ArrayList();
    // 往 list 中添加元素
    for (Object obj : list) {

    }

List 中的元素每迭代一次 for 循环就被执行一次。在 for 循环内部，每个元素都被轮流绑定到 obj 变量上。
如果 List 是一个泛型 List 的话可以在 for 循环中改变变量的类型（把原来的 Object 类型改变为相应的泛型类型）。下面是泛型 List 的迭代例子：

    List<String> list = new ArrayList();
    // 往 list 中添加元素

    for (String obj : list) {

    }
注意，List 是带有 String 类型的。所以，可以把循环内部的变量类型设置为 String 类型。
最后一种迭代 List 的方法是使用标准的 for 循环：

    List list = new ArrayList();
    // 往 list 中添加元素

    for(int i = 0; i < list.size(); i++) {
        Object = list.get(i);
    }

for 循环创建了一个 int 变量并把该变量初始化为 0 。只要变量 i 比 list 的 size 小，就会一直循环。每次循环变量 i 都会加 1 。
在例子中，通过把增长的变量 i 作为参数传递给 get() 方法来访问 list 中的每个元素。

### JavaDoc 中的更多细节
还可以对 List 做很多操作，但得通过查阅 Java 文档来了解细节。本文集中于最常见的两种操作：添加移除元素和迭代元素。







