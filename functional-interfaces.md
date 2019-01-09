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

# BiFunction

Takes 2 arguments and retrurn 1 value.

## Code Example

```public static void main(String[] args) {

		List<Person> persons = new ArrayList<>();

		Person p26 = new Person("Gourav", 26);
		Person p20 = new Person("Sourav", 15);

		persons.add(p26);
		persons.add(p20);

		System.out.println("Testing Predicate..................................");
		Predicate<Person> personPredicate = (person) -> person.getAge() > 18;
		System.out.println(personPredicate.test(p26));

		System.out.println("Testing Function...................................");
		Function<Person, String> personFunction = (person) -> personPredicate.test(person) ? "Adult" : "Kid";
		System.out.println(personFunction.apply(p26));
		System.out.println(personFunction.apply(p20));

		System.out.println("Testing Supplier...................................");
		Supplier<Double> randomIntSupplier = () -> Math.floor(Math.random() * 10);
		System.out.println(randomIntSupplier.get());

		System.out.println("Testing Consumer...................................");
		Consumer<List<Person>> ageConsumer = (personsList) -> {
			personsList.forEach((person) -> {
				if (person.getAge() >= 18) {
					System.out.println("Adult");
				} else {
					throw new RuntimeException("Not an adult");
				}
			});
		};
		try {
		ageConsumer.accept(persons);
		}catch(Exception e) {
			System.out.println(e);
		}
		
		System.out.println("Testing BiFunction...................................");
		BiFunction<Person, Person, Integer> greaterAgeBifunction = (p1, p2) -> p1.getAge() >= p2.getAge() ? p1.getAge() :p2.getAge();
		System.out.println(greaterAgeBifunction.apply(p26, p20));
	}```



