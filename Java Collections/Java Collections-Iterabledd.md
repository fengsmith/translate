Iterable 接口（java.util.Iterable）是 Java 集合类中的根接口之一。Collection 接口继承于 Iterable，所有 Collection 的所有子类型都实现了 Iterable 接口。
可以使用新的 for 循环来迭代实现了 Iterable 接口的类。下面是一个例子：

    List list = new ArrayList();
    
    for (Oject o : list) {
      // do sth o;
    }
    
Iterable 接口只有一个方法：

    public interface Iterable<T> {
        public Iterator<T> iterator();
    }  
    
在 Java 泛型教程中的实现 Iterable 接口一文中介绍了如何实现 Iterable 接口，实现了 Iterable 接口以后就可以用新的 for 循环来迭代。