## Prototype

Реализация клонирования делегируется самим объектам.

#### Классическая реализация
```java
public class Shape {
    private int width;
    private int height;

    public Shape() {
    }

    public Shape(Shape shape) {
        this.width = shape.width;
        this.height = shape.height;
    }
    
    public Shape clone() {
        return new Shape(this);
    }
}
```

#### Реализация с использованием native метода JVM
```java
public class Shape implements Cloneable {
    private int width;
    private int height;

    @Override
    public Shape clone() {
        Shape shape;
        try {
            shape = (Shape) super.clone();
        } catch (CloneNotSupportedException e) {
            throw new RuntimeException(e);
        }
        return shape;
    }
}
```