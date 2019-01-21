# Other important topics

## StringJoiner

http://www.javaguides.net/2018/07/java-8-stringjoiner-class.html

## Default Methods

### Advantages:

#### Backward Campatibility
In a typical design based on abstractions, where an interface has one or multiple implementations, if one or more methods are added to the interface, all the implementations will be forced to implement them too. Otherwise, the design will just break down so default interface methods are an efficient way to deal with this issue. They allow us to add new methods to an interface that are automatically available in the implementations. Thus, there’s no need to modify the implementing classes. In this way, backward compatibility is neatly preserved without having to refactor the implementers.

### Multiple Inheritance 

Consider you have 2 interfaces both having same default method. When a class implements both of these interfaces, compiler will complain as it doesn't know which one to use.

Solution:
- Class must override the default method so that none of the parent methods are used.
- Another, way is to use both the implementations:

```
@Override
public String turnAlarmOn() {
    return Vehicle.super.turnAlarmOn() + " " + Alarm.super.turnAlarmOn();
}
```
