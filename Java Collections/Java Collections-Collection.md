Collection 接口（java.util.Collection）是 Java 集合类的根接口之一。
尽管并不会直接实例化一个 Collection 的实例，但会实例化一个 Collection 的子类的实例，并且通常把这些子类型都统一地作为 Collection 来对待。在本文将会看到怎样来把这些子类型都统一地作为 Collection 来对待。
下面是本文将要涉及的一组主题：

1、Collection 的子类型
2、添加和移除元素
3、检查 Collection 中是否包含某个元素
4、Collection 的 size
5、迭代 Collection

### Collection 的子类型
下面的接口（集合类型）继承自 Collection 接口：
- List
- Set
- SortedSet
- NavigableSet
- Queue
- Deque
Java 中没有提供直接实现了 Collection 接口的类，要用集合类的话必须使用上面列出的接口的子类型。Collection 接口定义了一组方法（行为），继承自 Collection 接口的子接口都共享了这一组方法。
正因为 Collection 接口的子接口都共享了一组方法，所以在使用集合的时候才可以忽略掉掉特定的集合类型，只把它们当做一个 Collection 来处理。这是标准的继承性，并没有什么神奇，但这仍然是一个经久不衰的特性。
在本文的后续部分会描述 Collection 接口的最常用的通用操作。

下面是在集合上操作的一个方法：

    public class MyCollectionUtil {
        public static void doSomething(Collection collection) {
            Iterator iterator = collection.iterator();
            while (iterator.hasNext()) {
                Object object = iterator.next();
                // 对 object 做一些事
            }

        }
    }

下面有两种方式来调用 doSomething() 方法，每种方式传递了不同的 Collection 子类型作为了参数。

    Set set = new HashSet();
    List list = new ArrayList();

    MyCollectionUtil.doSomething(set);
    MyCollectionUtil.doSomething(list);

### 添加和移除元素
所有的集合类型都有着标准的添加和移除元素的方法。可以像这样来添加和移除单个元素：

    String anElement = "an element";
    Collection collection = new HashSet();

    boolean didCollectionChange = collection.add(anElement);
    boolean wasElementRemoved = collection.remove(anElement);

add() 方法添加给定的元素到集合中，调用 add() 方法后集合发生了改变则返回 true 。Set 的实例有可能不会发生改变。如果 Set 已经包含了某个元素，元素是不能被重复添加的。但是，在一个 List 上调用 add() 方法添加一个元素并且这个元素已经在 List 中，最终这个元素会在 List 中存在两次。
如果一个元素在集合中存在，调用 remove() 方法成功删除该元素后会返回 true 。如果一个元素不在集合中，调用 remove() 方法删除该元素后会返回 false 。

可以一次性删除或添加集合中的所有对象。下面是一些例子：

    Set aSet = ... //
    List aList = ... //
    Collection collection = new HashSet();
    collection.addAll(aSet);
    collection.addAll(aList);
    collection.removeAll(aList);
    collection.retainAll(aSet);

传入一个集合作为 allAll() 方法的参数，addAll() 方法会把参数集合中的所有元素都添加到集合中。参数集合对象本身并不会被添加到集合中，而是参数集合中保存的对象会被添加到集合中。
如果调用 add() 方法，则参数集合对象会被添加到集合中而不是参数集合对象中的元素。

addAll() 方法的具体行为依赖于集合的子类型。一些集合的子类型允许同样的元素被添加多次，另一些集合的子类型则不允许。

removeAll() 方法会把参数集合中的所有元素都移除。但如果在目标集合中找不到参数集合中的元素，这些元素将会被忽略。

retainAll() 方法与 removeAll() 方法正好相反。retainAll() 方法并不会把参数集合中的所有元素都删除而是把参数集合中的所有元素都保留，把目标集合中有但在参数集合中没有的元素全部删除。
需要注意的是，只有在目标集合中已经存在的元素才会被保留，如果目标集合中不存在参数集合中的元素，那么不会自动地把那些不存在的元素添加到目标集合中，这些不存在的元素会被忽略。

下面我们用伪代码来看一个例子：

    Collection colA = [A,B,C]
    Collection colB = [1,2,3]

    Collection target = [];
    target.addAll(colA); // 现在 target 包含 [A,B,C]
    target.addAll(colB); // 现在 target 包含 [A,B,C,1,2,3]

    target.retainAll(colB); // 现在 target 包含 [1,2,3]
    target.removeAll(colB); // 现在 target 为空

### 检查集合中是否包含某个元素
Collection 接口有两个方法可以检查一个集合中包含一个或多个特定元素。这两个方法是 contains() 方法和 containsAll 方法。下面是例子说明：

    Collection collection = new HashSet();
    boolean containsElement = collection.contains("an element");

    Collection elements = new HashSet();
    boolean containsAll = collection.containsAll(elements);

如果 Collection 中有某个元素的话 contains() 方法返回 true，没有的话返回 false 。
如果目标集合中包含了参数集合中的所有的元素的话 containsAll() 方法会返回 true，否则的话返回 false 。

### 集合的 size
可以使用 size() 方法来检查集合的大小。“size” 的意思是集合中元素的数量。下面是一个例子：

    int numberOfElements = collection.size();

### 迭代集合
可以迭代集合中的所有元素。可以通过集合的 Iterator 来遍历集合中的所有元素。下面是代码：

    Collection collection = new HashSet();
    // ... 给集合中添加元素
    Iterator iterator = collection.iterator();
    while (iterator.hasNext()) {
        Object object = iterator.next();
        // 对 object 做一些事
    }

也可以用新的 for-each 循环：

    Collection collection = new HashSet();
    // ... 给集合中添加元素
    for (Object object : collection) {
        // 对 object 做一些事
    }
















