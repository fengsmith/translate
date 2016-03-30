在 Java 中也可以泛型化方法，下面是一个例子：

    public static <T> T addAndReturn(T element, Collection<T> collection) {
        collection.add(element);
        return element;
    }
    
这个方法定义了一个类型 T ，T 是 element 参数的    
