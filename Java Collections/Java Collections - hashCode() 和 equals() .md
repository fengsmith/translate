hashCode() 方法和 equals() 方法在 Java Collections 中的对象上扮演了不同的角色。在 JavaDoc 中对这两个方法满足的契约约束有了很好的说明。在本文中我会告诉大家这两个方法在 Java collections 中的对象上扮演了什么样的角色。
 他们的用途，所以知道为什么他们是这样实现的是很重要的。
  
### equals()
在大多数的集合中都使用 equals() 方法来判断一个集合中是否包含某一个元素。例如：
  
  List list = new ArrayList();
  list.add("123");
  
  boolean contains123 = list.contains("123");
  
ArrayList 会迭代所有的元素并执行 "123".equals(element) 方法来判断 element 和参数对象 "123" 是否相等。这是 String.equals() 方法的实现，可以判断两个字符串的内容是否相等。
在移除元素的是否也会用到 equals() 方法。例如：

    List list = new ArrayList();
    list.add("123");
    
    boolean removed = list.remove("123");

ArrayList 会再次迭代所有的元素并执行 "123".equals(element) 方法来判断 element 和参数对象 "123" 是否相等。list 会删除最先找到的并且满足 element.equals("123") 为 true 条件的元素。
        
   
