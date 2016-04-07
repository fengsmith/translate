java.util.SortedSet 接口是 java.util.Set 接口的子类型。它的行为和一个正常的 Set 是一样的，但 SortedSet 的内部是有序的。意思是，迭代 SortedSet 时是按照一定的顺序返回的。

Set 中存储的元素所属的类如果实现了 java.lang.Comparable 接口的话，Set 中的元素的顺序就是自然顺序。或者是由构造 Set 时指定的 Comparator 来决定的。

默认，迭代元素是按升序排序的，即由小到大的移动。但也可以用 TreeSet.descendingIterator() 方法来降序迭代元素。

在 Java Collections API 中，只有 java.util.TreeSet 一个类实现了 SortedSet 接口。在 java.util.concurrent 包中也有一个类实现了该接口，但在本教程中不会涉及并发相关的类。

下面是怎样创建 SortedSet 的两个例子：

    SortedSet setA = new TreeSet();
    Comparator comparator = new MyComparator();
    SortedSet setB = new TreeSet(comparator);
    
### JavaDoc 中的更多细节
其实还可以在 TreeSet 上做更多的操作，有些操作并不是 SortedSet 接口中的部分，比如，获取 TreeSet 中的最大值元素和最小值元素，基于两个值然后把 TreeSet 截取成几个子 Set 等。可以通过查阅 JavaDoc 来了解更多的特殊特点。
