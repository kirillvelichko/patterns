## Decorator

Позволяет добавлять объектам новое поведение, помещая их в объекты-обёртки.

#### Базовый класс:
```java
public abstract class Sandwich {

    public abstract String getIngredients();
}

public class Bread extends Sandwich {

    public String getIngredients() {
        return "Bread";
    }
}
```

#### Декоратор:
```java
@RequiredArgsConstructor
public abstract class SandwichDecorator extends Sandwich {
    private final Sandwich sandwich;

    public String getIngredients() {
        return sandwich.getIngredients();
    }
}

public class Cheese extends SandwichDecorator {

    public Cheese(Sandwich sandwich) {
        super(sandwich);
    }

    public String getIngredients() {
        return super.getIngredients() + ", Cheese";
    }
}

public class Sausage extends SandwichDecorator {

    public Sausage(Sandwich sandwich) {
        super(sandwich);
    }

    public String getIngredients() {
        return super.getIngredients() + ", Sausage";
    }
}
```

#### Использование:
```java
public class Main {

    public static void main(String[] args) {
        var sandwich = new Sausage(new Cheese(new Bread()));
        System.out.println(sandwich.getIngredients());
    }
}
```