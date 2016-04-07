java.util.Map 接口代表了键和值之间映射关系的集合。Map 接口不是 Collection 接口的子类型，所以 Map 和之前介绍的其他集合类型有些不同。

下面是本文要讲的主题：

1、Map 的实现类
2、添加和访问元素
3、泛型 Map
4、JavaDoc 中的更多细节

### Map 的实现类
由于 Map 是一个接口，所以在使用的时候需要实例化一个具体的实现类。
在 Java 集合 API 中，可以在下面的实现类中选择：

- java.util.HashMap
- java.util.Hashtable
- java.util.EnumMap
- java.util.IdentityHashMap
- java.util.LinkedHashMap
- java.util.Properties
- java.util.TreeMap
- java.util.WeakHashMap

在我的开发实践中，最常用的 Map 实现类是 HashMap 和 TreeMap 。
每种 Map 的实现类在迭代、插入和访问方面的时间（大 O 记法）稍有不同。
HashMap 是键和值映射的集合。HashMap 不保证内部元素的存储顺序。
TreeMap 也是键和值映射的集合。但 TreeMap 保证迭代时 key 或 value 的顺序-keys 或 values 的排序顺序。查阅 JavaDoc 来获取更多详情。
下面是创建 Map 实例的几个例子：
   
   Map mapA = new HashMap();
   Map mapB = new TreeMap();
   
### 添加和访问元素
可以调用 put() 方法往 Map 中添加元素。下面是几个例子：
   
   Map mapA = new HashMap();
   mapA.put("key1", "element 1");
   mapA.put("key2", "element 2");
   mapA.put("key3", "element 3");
   
调用了三次 put() 方法，每次调用都会把一个 key 和 value 关联起来。然后就可以通过 key 来访问到 value 。可以像这样用 get() 方法来访问 value 。
    
    String 
   
   
   
   
   
   