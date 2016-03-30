Java 中的 Map 接口（java.util.Map）也可以被泛型化。换句话说，可以为 Map 的实例的键和值各自指定一种类型。下面是一个例子：

    Map<Integer, String> set = new HashMap<Integer, String>();
    
这个 Map 现在只接受 Integer 实例作为键 String 实例作为值。
泛型检查只存在编译期，在运行期可以调整代码把非 String 类型的实例添加到 String List 中。尽管可以这样做，但这并不是个好主意。

### 访问泛型 Map
在 Map 泛型中通过 put() 和 get() 方法来分别添加和获取元素，加了泛型之后和没加泛型的访问方式是一样的：
    
    Map<Integer, String> map = new HashMap<Integer, String>();
    Integer key1 = new Integer(123);
    String value1 = "value 1";
    map.put(key1, value1);
    String value1_1 = map.get(key1);
    
这样做有什么意义呢？在上面的例子中，如果你尝试往 map 中添加非 Integer，String 的类型对的实例，编译器是不允许的。这个额外的类型检查是不是很 nice ，对吧。
注意，通过 get() 方法获取到的实例不需要强制转换为 String 类型的实例。编译器知道 Map 的值是 String 类型的，强制转换是不必要的。
也可以像这样使用 Java 5 的自动装箱来方便的定义整型值：
    
    Map<Integer, String> map = new HashMap<Integer, String>();
    Integer key1 = 123;
    String value1 = "value 1";
    map.put(key1, value1);
    // or
    map.put(123, value1);
    String value1_1 = map.get(123);

### 迭代泛型 Map
Map 有两个集合可以迭代。key Set 和 value 集合。通常只迭代 key Set ，每个 key 值再通过 Map.get() 方法来访问 value。
下面是两个例子：

    Map<Integer, String> map = new HashMap<Integer, String>();
    // ... add key,value pairs to the Map
    // iterate keys
    Iterator<Integer> keyIterator = map.keySet().iterator();
    while (keyIterator.hasNext()) {
        Integer aKey = keyIterator.next();
        String aValue = map.get(aKey);
    }
    Iterator<String> valueIterator = map.values().iterator();
    while (valueIterator.hasNext()) {
        String aString = valueIterator.next();
    }

注意，通过 xxxIterator.next() 方法获取到的实例是不需要强制类型转换的。因为 Map 是泛型化的（有一种类型），编译器知道 keys 中包含的是 Integer 实例，values 中包含的是 String 实例。
所以，从 Map 中获取到的对象是不需要做类型强制转换的，即使实例是通过 xxxIterator.next() 方法获取到的。
也可以像下面这样使用 for-each 循环

    Map<Integer, String> map = new HashMap<Integer, String>();
    // ... add key,value pairs to the Map
    for (Integer aKey : map.keySet()) {
        String aValue = map.get(aKey);
        System.out.println("" + aKey + ":" + aValue);
    }    
    for (String aValue : map.values()) {
        System.out.println(aValue);
    }
注意，Integer 和 String 变量是定义在 for-each 循环的圆括号内部的，每次迭代（Map 的 key set 中的每个元素或者是 value 集合中的每个元素）循环变量包含了当前的值（当前的 Integer 或者是 String）。

    