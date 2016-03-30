可以实现自己的泛型类。泛型并不限于 Java API 中预定义的那些类。下面是一个简单的例子：

    public class GenericFactory<T> {
        Class theClass = null;
        public GenericFactory(Class theClass) {
            this.theClass = theClass;
        } 
        public T createInstance()
        throws IllegalAccessException, InstantiationException {
            return (T) this.theClass.newInstance();
        }
    
    }
    
<T> 是一个类型，可以给大家一个提示，在实例化的时候可以指定一个类型。下面是一个例子：
    
    GenericFactory<MyClass> factory = new GenericFactory<MyClass>(MyClass.class);
    MyClass myClassInstance = factory.createInstance();
        
注意，factory.createInstance() 方法返回的对象是不需要强制类型转换的。编译器可以根据创建的 GenericFactory 的泛型类型来推导出 factory.createInstance() 方法返回的对象类型，因为在 <> 里面定义了类型。
GenericFactory 的每个实例都可以泛型化为不同的类型。下面是两个例子：

    GenericFactory<MyClass> factory = new GenericFactory<MyClass>(MyClass.class);
    MyClass myClassInstance = factory.createInstance();
    
    GenericFactory<SomeObject>  someObjectFactory = new GenericFactory<SomeObject>(SomeObject.class);
    SomeObject someObjectInstance = someObjectFactory.createInstance();
    
        