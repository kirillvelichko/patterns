## Factory Method

Метод с общим интерфейсом для создания объектов, реализующие классы могут изменять тип создаваемых объектов.

```mermaid
classDiagram
  class Department{
    <<abstract>>
    get() Employee
  }
  
  class ItDepartment{
    get() Programmer
  }
  
  class Employee{
    <<abstract>>
  }
  
  class Programmer{
  }
  
  Department <|-- ItDepartment
  Employee <|-- Programmer
```

```java
abstract class Department {
    public abstract Employee getEmployee();
}

class ItDepartment extends Department {
    @Override
    public Programmer getEmployee() {
        return new Programmer();
    }
}

abstract class Employee {
}

class Programmer extends Employee {
}
```