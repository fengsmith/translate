java.util.SortedMap 接口是 java.util.Map 中的子类型。SortedMap 中存储的元素是有序的。
排序的顺序要么是元素的自然排序顺序（如果元素所属的类实现了 java.lang.Comparable 接口的话）要么是由构造 SortedMap 时指定的 Comparator 决定的。

迭代时，默认的顺序是升序排序的，即由小到大的移动。但是也可以用 TreeMap.descendingKeySet() 方法获取到的 keySet 降序迭代元素。
在 Java 集合 API 中只有 java.util.TreeMap 一个类实现了 SortMap 接口。在 java.util.concurrent 包中
也有一个 SortMap 的实现类，但在本教程中不会涉及到并发类。

下面是创建 SortedMap 的两个例子：

    SortedMap mapA = new TreeMap();

    Comparator comparator = new MyComparator();
    SortedMap mapB = new TreeMap();

### JavaDoc 中的更多细节
其实还可以在 TreeMap 上做更多的操作，有些操作并不是 SortedMap 接口中的部分，比如，获取降序的 keySet 等。可以通过查阅 JavaDoc 来了解更多的特殊特点。
