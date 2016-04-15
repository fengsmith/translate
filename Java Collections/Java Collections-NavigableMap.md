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
descendingKeySet() 方法会返回一个 NavigableSet ，这个返回来的 NavigableSet 和原来的 NavigableSet 相比元素的顺序是相反的。
返回来的这个 NavigableSet 其实是个视图，这个视图是由原来的 NavigableSet 维护着的。所以，改变了这个返回来的 NavigableSet 后，原来的 NavigableSet 也相应的改变了。
然而，不应该直接从 key set 中移除元素，应该使用 Map.remove() 方法去移除元素。


下面是一个简单的例子：

    NavigableSet reverse = map.descendingKeySet();

descendingMap() 方法返回一个 NavigableMap ，这个 NavigableMap 是原始的 Map 的一个视图。这个视图中 map 的元素的顺序与原始 map 中的元素的顺序是相反的。返回来的 NavigableMap 是原始 map 的视图，对视图的任何改变都会影响到原始的 map 。
下面是一个简单的例子：

    NavigableMap descending = map.descendingMap();

### headMap()、tailMap() 和 subMap()

headMap() 方法返回了个原始 NavigableMap 的视图，这个视图中只包含了比给定元素小的元素。下面是一个例子：

    NavigableMap original = new TreeMap();
    original.add("1", "1");
    original.add("2", "2");
    original.add("3", "3");

    // 这个 headMap1 只包含”1“和”2“
    SortedMap headMap1 = original.headMap("3");
    // 这个 headMap2 包含”1“、”2“和”3“，headMap() 的第二个参数 inclusive 表示是否包含给定元素，inclusive=true ，表示包含给定元素。
    NavigableMap headMap2 = original.headMap("3", true);

tailMap() 方法的工作原理和 headMap() 方法是一样的，只不过 tailMap() 方法返回的所有的元素都要比给定的参数元素大。

subMap() 允许传入两个参数作为返回的视图集合的边界。匹配元素时第一个边界包含，第二个边界不包含。下面是例子：

    NavigableMap original = new TreeMap();
    original.add("1", "1");
    original.add("2", "2");
    original.add("3", "3");
    original.add("4", "4");
    original.add("5", "5");

    // submap1 会包含 ("2", "2") 和 ("3", "3")
    SortedMap submap1  = original.subMap("2", "4");

    // submap2 会包含 ("2", "2")、("3", "3")、("4", "4") 因为 fromInclusive=true，toInclusive=true
    NavigableSet subset = original.subSet("2", true, "4", true);

### ceilingKey()、floorKey()、higherKey()、和 lowerKey()

ceilingKey() 方法会从元素的 key 值大于或等于给定值的集合中选出最小的一个元素返回。下面是一个例子：

    NavigableMap original = new TreeMap();
    original.put("1", "1");
    original.put("2", "2");
    original.put("3", "3");


    // ceilingKey 是”2“
    Object ceilingKey = original.ceilingKey("2");

    // floor 是”2“
    Object floorKey = original.floorKey("2");

floorKey() 方法和 ceilingKey() 方法正好相反，floorKey() 方法会从比给定元素小或相等的元素中选出最大的 key 值元素返回。

higherKey() 方法会从元素的 key 值大于（不包含等于）给定值的集合中选出最小的 key 值元素返回。下面是一个例子：

    NavigableMap original = new TreeMap();
    original.put("1", "1");
    original.put("2", "2");
    original.put("3", "3");


    // higherKey 是”3“
    Object higherKey = original.higherKey("2");

    // lower 是”1“
    Object lowerKey = original.lowerKey("2");

lowerKey() 方法和 higherKey() 方法正好相反。

### ceilingEntry(), floorEntry(), higherEntry(), lowerEntry()

NavigableMap 也有可以根据给定的 key 来获取实体的方法，而不是 key 本身。这些方法的行为和 ceilingKey() 等方法的行为很相似，除了这些方法返回的是一个 Map.Entry 而不是 key 本身。
一个 Map.Entry 映射了一个 key 和一个 value 。
下面是一个简单的例子。可以查阅 JavaDoc 了解更多的细节。

    NavigableMap original = new TreeMap();
    original.put("1", "1");
    original.put("2", "2");
    original.put("3", "3");
     
    // higherEntry 是 ("3", "3") 
    Map.Entry higherEntry = original.higherEntry("2"); 
    
    // lowerEntry 是 ("1", "1")
    Map.Entry lowerEntry = original.lowerEntry("2");
    


### pollFirstEntry() 和 pollLastEntry()

pollFirstEntry() 会删除 NavigableMap 中的第一个元素并返回，如果 NavigableMap 为空的话则返回 null 。
pollLastEntry() 会删除 NavigableMap 中的最后一个元素并返回，如果 NavigableMap 为空的话则返回 null 。
第一个元素意思是对集合中元素的 key 进行排序，选出 key 最小的元素。最后一个元素意思是选出 key 最大的元素。
下面是两个例子：

    NavigableMap original = new TreeMap();
    original.put("1", "1");
    original.put("2", "2");
    original.put("3", "3");


    // 第一个是 ("1", "1")
    Map.Entry first = original.pollFirstEntry();

    // 最后一个是 ("3", "3")
    Map.Entry last = original.pollLastEntry();

### JavaDoc 中的更多细节

在 NavigableMap 接口中仍然还有一些有意思的方法在本文中没有覆盖到。比如，firstEntry() 方法和 lastEntry() 。可以查阅 JavaDoc 文档来查阅更多的方法。


























