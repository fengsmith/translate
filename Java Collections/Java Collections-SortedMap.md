java.util.SortedMap 接口是 java.util.Map 中的子类型。SortedMap 中存储的元素是有序的。
排序的顺序要么是元素的自然排序顺序（如果元素所属的类实现了 java.lang.Comparable 接口的话）要么是由构造 SortedMap 时指定的 Comparator 决定的。

迭代时，默认的顺序是升序排序的，即由小到大的移动。但是也可以用 TreeMap.descendingKeySet() 
