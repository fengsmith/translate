Java 泛型的通配是一个机制，它的目的在于

下面是本文要讲的一组主题：
### 简单的泛型集合赋值问题
假设有下面的类继承层次：

    public class A {}
    public class B extends A {}
    public class C extends A {}
    
B 和 C 都继承自 A 。

请看下面的两个 List 变量：
    
    List<A> listA = new ArrayList<A>();
    List<B> listB = new ArrayList<B>();
    
可以让 listA 指向 listB ？或者是让 listB 指向 listA ？换句话说，下面的赋值是否是合法的：
    
    listA = listB;
    listB = listA;

答案是这两种赋值都是不合法的。下面是不合法的原因：
在 listA 中可以可以插入 A 的实例或者是 A 的子类的实例（B 和 C 的实例）。如果这样做的话：

    List<B> listB = listA;

可以通过 listA 往 listA 中添加 A、B、C 的实例，而现在 listB 和 listA 指向了同一个对象，所以从 listB 中获取到的对象就有可能是 A、B、C 的实例。而这破坏了声明 listB 时的契约：listB 只能添加 B 的实例或者是 B 的子类的实例，而事实上 A 和 C 不是 B 同时也不是 B 的子类。所以
    List<B> listB = listA;
    
是不合法的，同理：
    
    List<A> listA = listB;
    
也是不合法的。
    
### 什么时候需要这样的赋值操作？
在之前想要创建可复用的方法，这些方法在某种特定类型的集合上操作这时候就需要这样的赋值操作。
假如有个方法需要处理 List 中的元素，例如打印出 List 中的所有的元素。下面是方法的简单实现：
    
    public void processElements(List<A> elements) {
        for (A o : elements) {
            System.out.println(o.getValue());
        }
    }
    
上面的方法中迭代了 A 中的元素，并调用了 getValue() 方法（假设 A 有 getValue() 方法）。
在前面我们已经知道了不能把 List<B> 或者是 List<C> 作为参数来调用上面的方法。
     
### 泛型通配
泛型通配符可以解决上面提到的这种问题。通配符有两个主要的需求：

- 从泛型集合中获取对象
- 往泛型集合中插入对象

有 3 种方法可以在集合上定义泛型通配符，下面是例子：
    
    List<?>   listUknow = new ArrayList<A>();
    List<? extends A> listUknow = new ArrayList<A>();
    List<? super A> listUkonw = new ArrayList<A>();

接下来会对上面提到的这 3 种泛型通配做进一步的解释。

### 任意通配
List<?> 这个 list 的类型是不清楚的。可以是 List<A>，List<B>，List<String> 等。


     

    
    
    
