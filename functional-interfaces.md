### Functional Interfaces

- An Interface that contains exactly one abstract method is known as a functional interface.
- It can have any number of `default`, `static` methods but can contain only one abstract method. It can also declare methods of the object class.
- Functional Interface is also known as Single Abstract Method Interfaces or SAM Interfaces. It is a new feature in Java 8, which helps to achieve a functional programming approach.
- A functional interface can extend another interface only when it does not have any abstract method.
- The Java API has many one-method interfaces such as `Runnable`, `Callable`, `Comparator`, `ActionListener`, and others. They can be implemented and instantiated using anonymous class syntax.
  
## @FunctionalInterface Annotation

@FunctionalInterface annotation is used to ensure that the functional interface can’t have more than one abstract method. In case more than one abstract methods are present, the compiler flags an ‘Unexpected @FunctionalInterface annotation’ message. However, it is not mandatory to use this annotation.

## Predefined Functional Interfaces

# Predicate

Predicate interface contains exactly one abstract method test(T t). Note that it also contains a default, static methods.

# Function

Function interface contains exactly one abstract method apply(T t). Note that it also contains a default, static methods.
 
# Supplier

Supplier interface contains exactly one abstract method get(T t). It takes no argument and returns 1 value. Examples, `IntSupplier`, `DoubleSupplier`

# Consumer

Consumer interface contains exactly one abstract method accept(T arg0). It takes 1 argument and returns nothing.



