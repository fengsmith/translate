java.util.Queue 接口是 java.util.Collection 接口的子类型。Queue 就像 List 一样，Queue 代表了一组有序对象，但 Queue 的用途与 List 的用途有些不同。
只能在 Queue 的末尾插入元素，在 Queue 的开头删除元素。就像是在一个超市排队付款一样。
下面是本文要覆盖的一组主题：

- 1、Queue 的实现
- 2、添加和访问元素
- 3、移除元素
- 4、泛型 Queue
- 5、JavaDoc 中的细节

### Queue 的实现
Queue 是 Collection 的子类型，Queue 可以使用 Collection 的所有的方法。
由于 Queue 只是个接口，在使用 Queue 的时候必须实例化一个接口的具体实现类。
在 Java 集合 API 中，下面的类都实现了 Queue 接口，需要实例化 Queue 的时候可以在下面的类中选择：

LinkedList 是一个标准的 Queue 实现类。
PriorityQueue 内存储的元素是根据元素的自然顺序（如果元素所属的类实现了 Comparable 接口）或根据在构造 PriorityQueue 的时候指定的 Comparator 来存储元素的。

在 java.util.concurrent 包下也有 Queue 的实现类，但在本教程中不会涉及。

下面是创建 Queue 实例的一些例子：

    Queue queueA = new LinkedList();
    Queue queueB = new PriorityQueue();
    
### 添加和访问元素
可以调用 add() 方法来往 Queue 中添加元素。add() 方法也是继承自 Collection 的。下面是一些例子：

    Queue queueA = new LinkedLlist();
    
    queueA.add("element 1");
    queueA.add("element 2");
    queueA.add("element 3");
    
添加的元素在 Queue 中内部保存的顺序依赖于 Queue 的实现。从 Queue 中获取到的元素的顺序也是依赖于 Queue 的实现。可以通过查阅 JavaDoc 来获取更多的具体 Queue 实现类的信息。
    
可以在不移除 queue 中的元素的条件下来观察 queue 中最前面的元素。可以用 element() 来实现，下面是代码：

    Object firstElement = queueA.element();
    
可以使用 remove() 方法来删除 queue 中的第一个元素，remove() 方法将会在后面介绍。
    
也可以迭代 queue 中的所有元素而不用一次只处理一个元素。下面是代码：
    
   Queue queueA = new LinkedList();
   
   queueA.add("element 0");
   queueA.add("element 1");
   queueA.add("element 2");
    
   // 通过 iterator 访问
   Iterator iterator = queueA.iterator();
   while (iterator.hasNext()) {
       String element = iterator.next();
   } 
   
   // 通过 for-each 循环访问
   for(Object object : queueA) {
       String element = (String) object;
   }
   
通过 Iterator 或者是 for-each 循环（实际上也是用了 Iterator）来迭代 queue ，迭代返回的元素的顺序依赖于 queue 的实现。

### 移除元素
可以调用 remove() 方法来移除 queue 中的元素。remove() 方法移除了 queue 中最前面的元素。在大部分的 queue 实现中，head 和 tail 都是位于 queue 的相反的两端。
然而，也可以实现 head 和 tail 都位于 queue 的同一端的 Queue 接口。这种情况下 Queue 就成了 stack 。

下面是移除的一个例子：
   
   Object firstElement = queueA.remove();
   
### 泛型 Queue
默认，可以往 Queue 中放置任何对象，但自 Java 5 之后，可以限制插入 Queue 中元素的类型。下面是一个例子：
   
   Queue<MyObject> queue = new LinkedList<MyObject>();
   
现在，只能往这个 queue 中插入 MyObject 类型的对象。然后在迭代的时候就不需要对这些元素进行强制类型转换了。下面是代码：
    
    MyObject myObject = queue.remove();
    for (MyObject anObject : queue) {
        // 对 anObject 做一些操作
    }
  
  
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    