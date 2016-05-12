原文链接：[https://en.wikipedia.org/wiki/Facade_pattern](https://en.wikipedia.org/wiki/Facade_pattern)
Facade pattern（外观模式） 是一种软件设计模式，在 OOP 编程中经常会使用到。Facade pattern 这个名字是类比建筑学中的 facade 而来的。
一个 facade 就是一个对象，这个对象对一大块代码（例如一个类库）进行了封装，提供了一个简化的接口。facade 的优点：

- 由于 facade 为常用的任务提供了更方便的方法，所以让类库更容易使用、理解和测试；
- 同样地，由于 facade 为常用的任务提供了更方便的方法，所以让类库的可读性更好。
- 由于外部代码中的大部分代码是与 facade 在打交道而不是直接与类库打交道，所以减少了外部代码对类库内部的工作方式的依赖，同时使系统的开发更灵活。
- 把一个设计糟糕的 APIs 集合包裹在单个设计良好的接口中。

当系统非常复杂或者是由于系统有大量相互依赖的类或者是其他原因导致系统很难理解时就可以使用 Facade pattern 。这种模式隐藏了大型系统的复杂性，为客户端提供了一个相对简单的接口。Facade pattern 典型的涉及到了一个单一的包装器类，这个包装器中会有一组变量，客户端需要的功能会由这组变量中的一个或多个协同来完成，这些成员变量代理 facade 去访问系统，这样一来对客户端就隐藏了实现细节。

### 使用场景
用一个接口能代替一个潜在的对象，与这个潜在的对象相比，这个接口更简单、更容易使用，在这种情况下可以使用 facade pattern 。另外，如果一个包装器必须遵循某一个接口并且必须支持多态行为，这时候就可以使用 adapter 。一个 decorator 可以在运行时添加和修改一个接口的行为。

Pattern Intent（目的）
Adapter 把一个接口转化为另外一个接口，这个转化后的接口能满足客户端的期望。
Decorator 通过包裹原始的代码，为接口动态地添加职责。
Facade 提供一个简化的接口。

facade pattern 的典型使用场景：

- 通过一个简单的接口来访问一个复杂的系统；
- 子系统的抽象和实现是紧耦合的；
- 对不同层次的软件提供一个入口点；或者
- 一个系统非常复杂或者是很难理解。

### 结构

#### Facade

> facade 类对应用中的 1、2、3 这三个包进行了抽象。

#### Clients
> 那些使用 Facade Pattern 来访问包中提供的资源的对象。

### 例子
下面是一个抽象出来的例子，一个客户端（你）是怎样通过一个 facade（计算机）来访问一个复杂的系统（计算机的内部，比如说 CPU 和硬盘驱动器）。

    // 复杂的部分
    class CPU {
        public void freeze() { ... }
        public void jump(long position) { ... }
        public void execute() { ... }
    }
    class Memory {
        public void load(long position, byte[] data) { ... }
    }
    
    class HardDriver {
        public byte[] read(long lba, int size) { ... }
    } 
               
    // Facade
    class ComputerFacade {
        private CPU processor;
        private Memory ram;
        private HardDriver hd;
        
        public ComputerFacade() {
            this.processor = new CPU();
            this.ram = new Memory();
            this.hd = new HardDriver();
        }
        
        public void start() {
            processor.freeze();
            ram.load(BOOT_ADDRESS, hd.read(BOOT_SECTOR, SECTOR_SIZE));
            processor.jump(BOOT_ADDRESS);
            processor.execute();
        }
    }   
    
    // Client
    class You {
        public static void main(String[] args) {
            ComputerFacade computer = new ComputerFacade();
            computer.start();
        }
    }                        
     

