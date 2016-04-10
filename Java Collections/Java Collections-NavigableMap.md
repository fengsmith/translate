java.util.NavigableMap 接口是 java.util.SortedMap 接口的一个子接口。它的行为和 SortedMap 类似，除了具有 SortedMap 的排序机制外还有导航方法可以利用。
本文将仔细研究这些导航方法。

在 java.util 包下只有 java.util.TreeMap 类实现了 NavigableMap 接口。在 java.util.concurrent 包下也有个类实现了该接口，但同步类的用法不在本教程的范围内。

下面是本文要讲的一些主题：
- descendingKeySet() 和 descendingMap()
- headMap()、tailMap() 和 subMap()
- ceilingKey()、floorKey()、higherKey() 和 lowerKey()
- ceilingEntry()、floorEntry()、higherEntry() 和 lowerEntry()
- pollFirstEntry() 和 pollLastEntry()
- JavaDoc 中的更多细节

### descendingKeySet() 和 descendingMap()
最有意思的导航方法是 descendingKeySet() 方法和 descendingMap() 方法。
descendingSet() 方法会返回一个 NavigableSet ，这个返回来的 NavigableSet 和原来的 NavigableSet 相比元素的顺序是相反的。返回来的这个 NavigableSet 其实是个视图，这个视图是由原来的 NavigableSet 维护着的。所以，改变了这个返回来的 NavigableSet 后原来的 NavigableSet 也相应的改变了。然而，不应该直接从 key set 中移除元素，应该使用 Map.remove() 方法去移除元素。


下面是一个简单的例子：

    NavigableSet reverse = map.descendingKeySet();

descendingIterator() 方法可以以逆序的方式来迭代 NavigableSet 而不会改变原始 NavigableSet 的元素顺序。

    Iterator reverse = original.descendingIterator();

### headSet()、tailSet() 和 subSet()

headSet() 方法返回了个原始 NavigableSet 的视图，这个视图中只包含了比给定元素小的元素。下面是一个例子：

    NavigableSet original = new TreeSet();
    original.add("1");
    original.add("2");
    original.add("3");

    // 这个 headset 只包含”1“和”2“
    SortedSet headset = original.headSet("3");
    // 这个 headset 包含”1“、”2“和”3“，headSet() 的第二个参数 inclusive 表示是否包含给定元素，inclusive=true ，表示包含给定元素。
    NavigableSet headset = original.headSet("3", true);

tailSet() 方法的工作原理和 headSet() 方法是一样的，只不过 tailSet() 方法返回的所有的元素都要比给定的参数元素大。

subSet() 允许传入两个参数作为返回的视图集合的边界。匹配元素时第一个边界包含，第二个边界不包含。下面是例子：

    NavigableSet original = new TreeSet();
    original.add("1");
    original.add("2");
    original.add("3");
    original.add("4");
    original.add("5");

    // subset 会包含”2“和”3“
    SortedSet subset  = original.subSet("2", "4");

    // subset 会包含”2“, ”3“和”4“因为 fromInclusive=true，toInclusive=true
    NavigableSet subset = original.subSet("2", true, "4", true);

ceiling()、floor()、higher()、和 lower()

ceiling() 方法会从比给定元素大或相等的元素中选出最小的元素返回。下面是一个例子：

    NavigableSet original = new TreeSet();
    original.add("1");
    original.add("2");
    original.add("3");


    // ceiling 是”2“
    Object ceiling = original.ceiling("2");

    // floor 是”2“
    Object floor = original.floor("2");

floor() 方法和 ceiling() 方法正好相反，floor 方法会从比给定元素小或相等的元素中选出最大的元素返回。

higher() 方法会从比给定元素大(不包含相等)的元素中选出最小的元素返回。下面是一个例子：

    NavigableSet original = new TreeSet();
    original.add("1");
    original.add("2");
    original.add("3");


    // higher 是”3“
    Object higher = original.higher("2");

    // lower 是”1“
    Object lower = original.lower("2");

lower() 方法和 higher() 方法正好相反。

### pollFirst() 和 pollLast()
pollFirst() 会删除 NavigableSet 中的第一个元素并返回，如果 NavigableSet 为空的话则返回 null 。
pollLast() 会删除 NavigableSet 中的最后一个元素并返回，如果 NavigableSet 为空的话则返回 null 。
第一个元素意思是集合中根据排序排出的最小的元素。最后一个元素意思是集合张根据排序排出的的最大的元素。
下面是两个例子：

    NavigableSet original = new TreeSet();
    original.add("1");
    original.add("2");
    original.add("3");


    // 第一个是”1“
    Object first = original.pollFirst();

    // 最后一个是”3“
    Object last = original.pollLast();



























