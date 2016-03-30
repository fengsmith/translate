##Java Generics Tutorials
从 Java 5开始 Java 语言就支持泛型了。泛型增加了一种方式在对象上提前操作通用目的的类和方法来定义具体的类型。听起来有些抽象，现在让我们看几个集合泛型的例子。
注意：不仅集合类中可以使用 Java 泛型，其他类也可以，使用集合类来展示泛型的一些基础是最简单的一种方式。

Java Generics Example
List 接口代表了一组 Object 实例，也就是说我们可以往 List 里放任何对象。
下面是一个例子：

    List list = new ArrayList();
    list.add(new Integer(2));
    list.add("a String");
    
由于在 List 里可以放任何对象，从 List 中获取到的对象必须强制类型转换。
例如：

    Integer integer = (Integer) list.get(0);
    String string = (String) list.get(1);
    
在实践中通常一个集合里面只存放一种对象。例如，在一个集合中可能只存放 String 或其他类型的一种对象，而不会像在前面的例子中那样在一个集合中混合存储各种类型的对象。
使用 Java 泛型，可以设置集合中能存储的对象的种类。另外，从集合中获取到的对象不需要做类型转换。下面是使用 Java 泛型的一个例子：
    
    List<String> strings = new ArrayList<String>();
    strings.add("a String");
    String aString = strings.get(0);

很 nice，对吧！

Java 7 类型接口
在 Java 7 中更新了 Java 泛型，从 Java 7 起，编译器可以根据集合被赋值的变量的类型来推导出需要实例化的集合的类型。下面是一个 Java 7 泛型的例子：
    
    List<String> strings = new ArrayList<>();

注意，ArrayList 的泛型是怎样被省略的。只需要一对 <> 即可。有时称 <> 为 diamond 操作符，当只写一个 <> 操作符作为泛型时，Java 编译器会假定被实例化的类和其被赋值给的变量具有同样的类型。
具体到上面例子，泛型的类型就是 String ，因为 List 变量的类型为 String ，而被实例化的对象的类型和变量的类型是相同的。
    
Java 泛型 for 循环
Java 5 引入了新的 for 循环（也称之为 “for-each”），for-each 循环很适合泛型集合。
下面是一个例子：
    
    List<String> strings = new ArrayList<String>();
    // ... add String instances to the strings list...
    for (String aString : strings) {
        System.out.println(aString);
    }
for-each 循环遍历了保存在 strings list 中的所有 String 实例。每次遍历都会把下一个 String 实例赋值给 aString 变量。for-each 循环比 while 循环要简短，while 循环需要通过集合的 Iterator 和循环调用 Iterator.next() 来获取下一个实例。
泛型循环（“for-each”）会在 Java Generic for loop 中详细介绍。

###集合类型之外的其他类型的 Java 泛型
当然了，除了 Java 集合可以使用 Java 泛型外，其他类也可以使用 Java 泛型。也可以实现自己的泛型类。在 Generic Classes，Generic methods 和 Using class objects as type literals 几篇文章中会详细介绍怎样自定义泛型类。
