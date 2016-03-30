Java 的 List(java.util.List) 接口可以被泛型化。换句话说，可以给定 List 一种类型，只有这种类型的实例才可以被插入在 List 中和从 List 中读取。下面是一个例子：

    List<String> list = new ArrayList<String>;
现在，list 的目标只能是 String 实例，意思是，list 中只能添加 String 实例。如果你想把其他类型的实例添加到 list 中，编译器是不允许的。
泛型检查只存在编译期，在运行期可以调整代码把非 String 类型的实例添加到 String List 中。尽管可以这样做，但这并不是个好主意。
### 访问泛型 List
可以像这样在泛型 List中获取和插入元素：
    
    List<String> list = new ArrayList<String>;
    String string1 = "a string";
    list.add(string1);
    String string2 = list.get(0);

注意，调用 list.get(0) 方法后获取到的对象是不需要做类型转换的，如果没有泛型的话，通常是需要做强制类型转换的。编译器能知道 list 只能存储 String 类型的实例，所以强制类型转换是不必要的。
### 迭代泛型 List
可以像下面一样使用 iterator 迭代 list：
    
    List<String> list = new ArrayList<String>();
    Iterator<String> iterator = list.iterator();
    while (iterator.hasNext()) {
        String aString = iterator.next();
    }
    
注意，调用 iterator.next() 方法后返回的对象是不需要做强制类型转换的。因为 List 是泛型化的（有一个类型），编译器知道 iterator 包含的是 String 实例。所以调用 iterator.next() 方法后返回的对象是不需要做强制类型转换的，即使对象是经过调用 iterator 的 iterator.next() 方法得到的。
也可以像这样使用 for-each 循环：
       
    List<String> list = new ArrayList<String>();
    for (String aString : list) {
        System.out.println(aString);
    }       
注意，aString 变量是定义到 for-each 循环的圆括号内部的。在for-each 遍历 List 的过程中，当前的元素（当前的字符串）被赋值给了 aString 变量。
    
    