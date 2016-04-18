java.util.Stack 值得单独讲解一下。在 List 接口一文中，提到过 Stack 是 List 种的一种实现。Stack 的典型使用并不是作为 List 来使用的。
 
Stack 是一种数据结构，可以往 Stack 顶添加元素，也只能从 Stack 顶移除元素。这也就是常说的”后进先出“原则。与之相反的是 Queue 用的是”先进先出原则“。

用 Stack 来处理一些类型的数据很方便，例如使用 SAX 或 StAX 。例如，我的 Java XML 教程中的例子[Java SAX Example](http://tutorials.jenkov.com/java-xml/sax-example.html)。

下面是 Stack 的使用例子：

    Stack stack = new Stack();
    
    stack.push("1");
    stack.push("2");
    stack.push("3");
    
    // 查看对象 "3" 而不需要移除
    Object objTop = stack.peek();
    
    Object obj3 = stack.pop(); // stack 顶部的元素是 "3"
    Object obj2 = stack.pop(); // stack 顶部的元素是 "2"
    Object obj1 = stack.pop(); // stack 顶部的元素是 "1"
    
push() 方法把一个对象 push 到 Stack 顶部。
peek() 方法返回 Stack 顶部的对象，但并不会移除该对象。
pop() 方法移除 Stack 顶部的对象并返回。
    
### 查找 Stack
用 search() 方法可以在 Stack 中查找一个对象并返回其索引。在查找的时候会循环调用 Stack 中元素的 equals() 方法与传入的参数进行比较是否相等，从而找到目标的元素。查找元素获取到的元素的索引是从 Stack 顶部开始计算的，索引从 1 开始，顶部的元素的索引是 1 。
    
下面是在 Stack 中查找元素的例子：
   
   Stack stack = new Stack();
   
   stack.push("1");
   stack.push("2");
   stack.push("3");
   
   int index = stack.search("3"); // index = 1
    