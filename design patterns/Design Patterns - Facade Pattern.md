原文链接：[http://www.tutorialspoint.com/design_pattern/facade_pattern.htm](http://www.tutorialspoint.com/design_pattern/facade_pattern.htm)
Facade Pattern（门面模式/外观模式） 隐藏了系统的复杂性，为客户端访问系统提供了一个接口。Facade Pattern 属于结构型模式的一种，通过添加一个接口来隐藏现有系统的复杂性。
Facade Pattern 涉及到一个类，这个类像代理一样调用了现有系统的类的一些方法，从而为客户端提供了简化的方法来访问系统。

### 实现

我们将会创建一个 Shape 接口和 Shape 接口的具体实现类。下一步中会定义一个 facade 类 ShapeMaker。

ShapeMaker 使用具体的类来代理用户想要访问的类。FacadePatternDemo 是一个 demo 类，会用 ShapeMaker 类来展示结果。

### 第一步
创建一个接口。
Shape.java

    public interface Shape {
        void draw();
    }
### 第二步

创建 Shape 接口的具体实现类。

Rectangle.java

    public class Rectangle implements Shape {
        @Override
        public void draw() {
            System.out.println("Rectangle::draw()");
        }
    }

Square.java

    public class Square implements Shape {
        @Override
        public void draw() {
            System.our.println("Square::draw()");
        }
    }
Circle.java
    
    public class Circle implements Shape {
        @Override
        public void draw() {
            System.out.println("Circle::draw()");
        }
    }
    
### 第三步
创建一个 facade 类。
ShapeMaker.java
    public class ShapeMaker {
        private Shape circle;
        private shape rectangle;
        private shape square;
        
        public ShapeMaker() {
            circle = new Circle();
            rectangle = new Rectangle();
            square = new Square();
        }
        
        public void drawCircle() {
            circle.draw();
        }
        
        public void drawRectangle() {
            rectangle.draw();
        }
        
        public void drawSquare() {
            square.draw();
        }
    }    
### 第四步
    
使用 facade 绘制各种类型的形状。
FacadePatternDemo.java
    
    public class FacadePatternDemo {
        public void main(String[] args) {
            ShapeMaker shapeMaker = new ShapeMaker();
            
            shapeMaker.drawCircle();
            shapeMaker.drawRectangle();
            shapeMaker.drawSquare();
        }
    }
    
### 第五步
验证结果。
    
    Circle::draw()
    Rectangle::draw()
    Square::draw()
  