原文链接：[http://www.tutorialspoint.com/design_pattern/decorator_pattern.htm](http://www.tutorialspoint.com/design_pattern/decorator_pattern.htm)
Decorator Pattern（装饰器模式） 允许用户对已经存在的对象添加新的功能而不修改它的结构。Decorator Pattern 属于结构型模式的一种。Decorator Pattern 对现有的类充当了一个包装器的角色。

Decorator Pattern 创建了一个 decorator 类，这个类包装了原始的类，提供了和原始类的方法签名都完全一样的方法，并对这些方法提供了额外的功能。

下面的例子展示了 decorator pattern 的使用，我们在不修改 shape 类的前提下，将使用一些颜色来装饰 shape 。
 
### 实现
我们将创建一个 Shape 接口和实现了 Shape 接口的几个具体实现类。然后，我们将会创建一个抽象的装饰类 ShapeDecorator ，ShapeDecorator 实现了 Shape 接口并且还有一个 Shape 类型的成员变量。

RedShapeDecorator 实现了 ShapeDecorator 。

DecoratorPatternDemo 是我们的 demo 类，它会使用 RedShapeDecorator 来装饰 Shape 对象。
 
### 第一步
创建 Shape 接口。

Shape.java

    public interface Shape {
        void draw();
    }
    
### 第二步
创建几个实现了 Shape 接口的实现类。
    
Rectangle.java
    
    public class Rectangle implements Shape {
        @Override
        public void draw() {
            System.out.println("Shape:Rectangle");
        }
    }

Circle.java
    
    public class Circle implements Shape {
        @Override
        public void draw() {
            System.out.println("Shape:Circle");
        }
    }
    
### 第三步
创建一个实现了 Shape 接口的抽象装饰类。

ShapeDecorator.java
    
    public abstract class ShapeDecorator implements Shape {
        protected Shape decoratedShape;
        
        public ShapeDecorator(Shape decoratedShpae) {
            this.decoratedShpae = decoratedShape;
        }
        public void draw() {
            decoratedShape.draw();
        }
    }
    
### 第四步
创建一个继承于 ShapeDecorator 类的具体的装饰类。

RedShapeDecorator.java
    
    public class RedShapeDecorator extends ShapeDecorator {
        public RedShapeDecorator(shape decoratedShape) {
            super(decoratedShape);
        }
        
        @Override
        public void draw() {
            decoratedShape.draw();
            setRedBorder(decoratorShape);
        }
        private void setBorder(Shape decoratoredShape) {
            System.out.println("Border Color:Red");
        }
    }
    
### 第五步
使用 RedShapeDecorator 来装饰 Shape 对象。

DecoratorPatternDemo.java
    
    public class DecoratorPatternDemo {
        public static void main(String[] args) {
            Shape circle = new Circle();
            
            Shape redCircle = new RedShapeDecorator(new Circle());
            
            shape redRectangle = new RedRectangle(new Rectangle());
            System.out.println("Circle with normal border");
            circle.draw();
            
            System.out.println("\nCircle of red border");
            redCircle.draw();
            
            System.out.println("\nRectangle of red border");
            redRectangle.draw();
        }
    }
    
### 第六步

验证输出结果。
    
    Circle with normal border
    Shape:Circle
    
    Circle of red border
    Shape:Circle
    Border color:red
    
    Rectangle of red border
    Shape:Rectangle
    Border Color:Red
 

