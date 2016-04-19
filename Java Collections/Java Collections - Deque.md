java.util.Deque 接口是 java.util.Queue 接口的子类型。Deque 代表了一个 Queue ，可以在 Queue 的两端插入和移除元素。Deque 是 "Double Ended Queue" 的缩写，发音是 "deck" ，就像是一副扑克牌一样。

下面是本文涉及到的一组主题：

- Deque 的实现
- 添加和访问元素
- 移除元素
- 泛型 Deques
- JavaDoc 中的更多细节

### Deque 的实现
Deque 是 Queue 和 Collection 的子类型，Deque 可以使用 Queue 和 Collection 中的所有方法。
由于 Deque 是一个接口，在使用的时候必须要实例化一个具体的类。在 Java Collections API 中有几个 Deque 的实现类，在使用的时候可以从下面的两个实现类中选择一个：

- java.util.ArrayDeque
- java.util.LinkedDeque

LinkedList 是一个标准的 deque/queue 的实现类。
ArrayDeque 在底层是用数组实现的，所有的元素都保存在数组中。如果，元素的数量超出了数组的容量，就会重新分配一个数组，所有的元素会复制到这个新的数组中。换句话说，ArrayDeque 是按需增长的，虽然 ArrayDeque 的内部实现是数组，但也可以按需增长。

在 java.util.concurrent 包下也有 Deque 的实现类，但本教程中不会涉及到并发的相关类。

下面是怎样创建 Deque 的几个例子：

    Deque dequeA = new LinkedList();
    Deque dequeB = new ArrayDeque();
    
### 添加和访问元素
可以通过调用 add() 方法在 Deque 的尾部添加一个元素。也可以使用 addFirst() 和 addLast() 方法来添加元素，这两个方法分别在 Deque 的首部和尾部添加元素。
    
    Deque dequeA = new LinkedList();
    
    dequeA.add("element 1");
    dequeA.addFirst("element 2");
    dequeA.addLast("element 3");
    
添加到 Deque 内的元素的顺序依赖于 Deque 的实现。前面提到的 Deque 的两种实现类的元素存储顺序和插入顺序是一致的。

可以通过 element() 方法查看 queue 首部的元素而不需要移除该元素，也可以使用 getFirst() 方法和 getLast() 方法，这两个方法分别返回第一个元素和最后一个元素。下面是代码：

    Object firstElement = dequeA.element();
    Object firstElement1 = dequeA.getFirst();
    Object lastElement = dequeA.getLast();

稍后会讲怎样移除元素。
也可以迭代 deque 中的所有的元素，而不是一次处理一个元素。下面是代码：
    
    Deque dequeA = new LinkedList();
    
    dequeA.add("element 0");
    dequeA.add("element 1");
    dequeA.add("element 2");
    
    // 通过 Iterator 访问
    Iterator iterator = dequeA.iterator();
    while (iterator.hasNext()) {
        String element = (String) iterator.next();
    }
当通过 Iterator 或 for-each 循环迭代 deque 时迭代元素的顺序依赖于 queue 的实现。
    
### 移除元素
可以通过调用 remove() 方法、removeFirst() 方法、removeLast() 方法来移除元素。下面是几个例子：
    
    Object firstElement = dequeA.remove();
    Object firstElement1 = dequeA.removeFirst();
    Object lastElement = dequeA.removeLast();
    
### 泛型 Deque
默认，可以往 Deque 中添加任何元素，自从 Java 5 之后，Java 泛型可以限制插入到 Deque 中的元素的类型。下面是例子：
    
    Deque<MyObject> deque = new LinkedList<MyObject>();
现在 Deque 中只能插入 MyObject 类型的实例。现在迭代元素时不再需要对元素做强制类型转换了。下面是代码：
    
    MyObject myObject = deque.remove();
    
    for (MyObject anObject : deque) {
        // 对 anObject 做一些操作
    }
    
可以查阅 Java 泛型教程来了解泛型的更多细节。

### JavaDoc 中的更多细节
Deque 还有很多方法，可以通过查阅 JavaDoc 了解更多的细节。本文重点集中在两个最常用的操作上：添加/移除元素，迭代元素。
    