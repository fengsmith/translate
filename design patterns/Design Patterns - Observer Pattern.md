观察者模式通常在对象之间存在一对多的关系下使用。例如，一个对象发生了变化需要通知依赖它的所有的对象。观察者模式属于行为模式的一种。

### 实现


观察者模式使用了三个 actor 类。Subject，Observer 和 Client 。Subject 是个对象，通过这个对象的附着（attach）和脱离（detach）方法，Observers 对象可以附着于 Subject 对象或者是脱离于 Subject 对象。
我们创建了一个抽象的类 Observer 和一个继承于 Observer 的具体的类 Subject 。

ObserverPatternDemo 是我们的 demo 类，ObserverPatternDemo 会使用 Subject 和 具体的对象来演示观察者模式。

### 第一步
创建 Subject 类。
Subject.java

    import java.util.ArrayList;
    import java.util.List;
    
    public class Subject {
        private List<Observer> observers = new ArrayList<Observer>();
        private int state;
        
        public int getState() {
            return state;
        }
        
        public void setState(int state) {
            this.state = state;
            notifyAllObservers();
        }
        
        public void attach(Observer observer) {
            observers.add(observer);
        }
        
        public void notifyAllObservers() {
            for (Observer observer : observers) {
                observer.update();
            }
        }
    } 
    
### 第二步
创建 Observer 类。
Observer.java
   
    public abstract class Observer {
        protected Subject subject;
        public abstract void update();
    }
    
### 第三步
创建具体的 observer 类。
BinaryObserver.java
    
    public class BinaryObserver extends Observer {
        public BinaryObserver(Subject subject) {
            this.subject = subject;
            this.subject.attach(this);
        }
        
        @Override
        public void update() {
            System.out.println("Binary String:" + Integer.toBinaryString(subject.getState()));
        }
    
    
    }
OctalObserver.java
    
    public class OctalObserver extends Observer {
        public OctalObserver(Subject subject) {
            this.subject = subject;
            this.subject.attach(this);
        }
        @Override
        public void update() {
            System.out.println("Octal String:" + Integer.toOctalString(subject.getState());
        }
    }
    
HexaObserver.java
    public class HexaObserver extends Observer {
        public HexaObserver(Subject subject) {
            this.subject = subject;
            this.subject.attach(this);
        }
        
        @Override
        public void update() {
            System.out.println("Hex String:" + Integer.toHexString(subject.getState()).toUpperCase());
        }
    
    }
    
### 第四步
使用 Subject 和具体的观察者对象。
ObserverPatternDemo.java
    
    public class ObserverPatternDemo {
        public static void main(String[] args) {
            Subject subject = new Subject();
            
            new HexaObserver(subject);
            new OctalObserver(subject);
            new BinaryObserver(subject);
            
            System.out.println("First state change:15");
            subject.setState(15);
            System.our.println("Second state change:10");
            subject.setState(10);
        }
    }
    
### 第五步
验证输出结果。
    
    First state change:15
    Hex String:F
    Octal String:17
    Binary String:1111
    Second state change:10
    Hex String:A
    Octal String:12
    Binary String:1010
    