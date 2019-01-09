# java-concepts

## Lambda Expressions
  - Syntax
    - `() -> return 1+1;`
    - `(int a, int b) -> return a+b;`
    - `(int a, int b) -> { a += 10; b += 20; return a+b; }`
  - Pointers
    - Function interfaces having only one abstract method (As interfaces in Java8 can have default and static methods in addition to abstract methods)
  - Lambda vs Anonymous Interface Implementations
    - Anonymous Interface Implementations can have state (member variables)
    - Lambdas cannot have state (member variables)
  - Lambda Type Inference
      ```
      item.addListener(
        (oldState, newState) -> System.out.println("State changed")
      );
      ```
      Type of parameter for Lamba expression is inferenced from `addListener` method declaration.
  - Java lambda expression is treated as a function, so the compiler does not create a .class file
  - 
