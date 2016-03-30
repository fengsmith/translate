Java 中的 Set 接口（java.util.Set）也可以被泛型化。换句话说，可以为 Set 的实例指定一种类型，只有这种类型的实例才可以往 Set 插入和读取。下面是一个例子：

    Set<String> set = new HashSet<String>;
现在，Set 的目标只能是 String 的实例，意思是，set 中只能添加 String 实例。如果你想把其他类型的实例添加到 set 中，编译器是不允许的。
泛型检查只存在编译期，在运行期可以调整代码把非 String 类型的实例添加到 String List 中。尽管可以这样做，但这并不是个好主意。

### 往泛型 Set 中添加元素
用 add() 方法往 Set 中添加元素，就像往其他集合类中添加元素一样，下面是代码：

    Set<String> set = new HashSet<String>();
    String string1 = "a string";
    set.add(string1);

这样做有什么意义呢？如果你尝试往 set 中添加非 String 类型的实例，编译器是不允许的。这个额外的类型检查是不是很 nice ，对吧。

### 迭代泛型 Set
可以使用 iterator 来迭代泛型 Set ，下面是代码：

    Set<String> set = new HashSet<String>();
    Iterator<String> iterator = set.iterator();
    while (iterator.hasNext()) {
        String aString = iterator.next();
    }

注意，调用 iterator.next() 方法后返回的对象是不需要做强制类型转换的。因为 Set 是泛型化的（有一个类型），编译器知道 iterator 包含的是 String 实例。所以调用 iterator.next() 方法后返回的对象是不需要做强制类型转换的，即使对象是经过调用 iterator 的 iterator.next() 方法得到的。
也可以像这样使用 for-each 循环：

    Set<String> set = new HashSet<String>();
    for (String aString : set) {
        System.out.println(aString);
    }

注意，aString 变量是定义到 for-each 循环的圆括号内部的。在for-each 遍历 List 的过程中，当前的元素（当前的字符串）被赋值给了 aString 变量。
