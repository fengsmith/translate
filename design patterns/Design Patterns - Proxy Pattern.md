原文链接：[http://www.tutorialspoint.com/design_pattern/proxy_pattern.htm](http://www.tutorialspoint.com/design_pattern/proxy_pattern.htm)
在代理模式中，一个类（代理）代理了另外一个类（被代理）的功能。代理模式属于结构型模式的一种。
在代理模式中，我们会创建一个对象（代理对象），这个对象有一个原始对象（被代理对象），这个代理对象会与外界打交道，而被代理对象不会直接与外界产生联系。

### 实现
我们将会创建一个 Image 接口和它的实现类。ProxyImage 是一个代理类，它的目的是延迟加载 RealImage 对象，减少 RealImage 对象在内存中的占用时长。

ProxyPatternDemo 是我们的 demo 类，ProxyPatternDemo 将会使用 ProxyImage 在需要 RealImage 的时候去硬盘上加载图片并显示。

### 第一步
创建一个接口。

Image.java

    public interface Image {
        void display();
    }
### 第二步
创建 Image 接口的实现类。

RealImage.java
   
   public class RealImage implements Image {
       private String fileName;
       
       public RealImage(String fileName) {
           this.fileName = fileName;
           loadFromDisk(fileName);
       }
       
       @Override
       public void display() {
           System.out.println("Displaying " + fileName);
       }
       
       private void loadFromDisk(String fileName) {
           System.out.println("Loading " + fileName);
       }
   }
   
ProxyImage.java
   
   public class ProxyImage implements Image {
       private String fileName;
       private RealImage;
       
       public ProxyImage(String fileName) {
           this.fileName = fileName;
       }
       
       @Override
       public void display() {
           if (realImage == null) {
               realImage = new RealImage(fileName);
           }
           realImage.display();
       }
   }
   
### 第三步
使用 ProxyImage 在需要 RealImage 的时候去获取 RealImage 。 
  
ProxyPatternDemo.java
    
    public class ProxyPatternDemo {
        public static void main(String[] args) {
            Image image = new ProxyImage("test_10mb.jpg");
            // 将会从硬盘中加载图片
            image.display();
            
            System.out.println("");
            
            // 不会再次从硬盘中加载图片
            image.display();
        }
    }
           
### 第四步
验证输出。

    Loading test_10mb.jpg
    Displaying test_10mb.jpg
    
    Displaying test_10mb.jpg
  
