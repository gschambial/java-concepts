# Method References

Each time when you are using lambda expression to just referring a method, you can replace your lambda expression with method reference.

e.g;

## There are 4 ways:

### Static Method Reference

```
/*
 * Functional Interface where body is a reference to static method of some other
 * class
 */
interface PersonOperationsCheckStatic {

	boolean isPersonAdult(Person person);
}
```

```
/*
 * Class which contains method body we want to refer to
 *
 */
class PersonUtils {

	public static boolean isAdult(Person person) {
		return person.getAge() >= 18 ? true : false;
	}
}

```

```
/*
 * Using Lambda
 *
 */
 PersonOperationsCheckStatic staticMethodCheckWithLambda = (person) -> PersonUtils.isAdult(person);
```

```
/*
 * Using Method Reference
 *
 */
 PersonOperationsCheckStatic staticMethodCheckWithMethodReference = PersonUtils::isAdult;
```

### Instance Method Reference

```
/*
 * Functional Interface where body is a reference to instance method of some other
 * class
 */
interface PersonOperationsCheckInstance {

	boolean isPersonLegalToMarry(Person person);
}
```

```
/*
 * Class which contains method body we want to refer to
 *
 */
class PersonUtils {

	public boolean isLegalToMarry(Person person) {
		return person.getAge() >= 21 ? true : false;
	}
}

```

```
/*
 * Using Lambda
 *
 */
 PersonOperationsCheckInstance instanceMethodCheckWithLambda = (person) -> new PersonUtils()
				.isLegalToMarry(person);
```

```
/*
 * Using Method Reference
 *
 */
 PersonOperationsCheckInstance instanceMethodCheckWithMethodReference = new PersonUtils()::isLegalToMarry;
```

### Constructor Method Reference

```
/*
 * Functional Interface where body is reference to constructor of some class
 */
interface PersonOperations {

	Person get(String name, Integer age);
}
```

```
/*
 * Class which contains constructor we want to refer to
 *
 */
class Person {

	private String name;
	private Integer age;

	public Person(String name, Integer age) {
		super();
		this.name = name;
		this.age = age;
	}

	public String getName() {
		return name;
	}

	public void setName(String name) {
		this.name = name;
	}

	public Integer getAge() {
		return age;
	}

	public void setAge(Integer age) {
		this.age = age;
	}

	@Override
	public String toString() {
		return "Person [name=" + name + ", age=" + age + "]";
	}
}

```

```
/*
 * Using Lambda
 *
 */
 PersonOperations constructorCheckWithLambda = (name, age) -> new Person(name, age);
```

```
/*
 * Using Method Reference
 *
 */
 PersonOperations constructorCheckWithMethodReference = Person::new;
```


### Instance Method Reference by Class

  - If `Functional Interface` argument list is `(Person p1, Person p2, Integer i)` then ideally, It can refer to an `instance method` of a class.

  - But, if `Person` has a method as `(Person p2, Integer i)` then we can use `Person::method` style to refer to this method body. Compiler can automatically infer that first argument is the object used to invoke this method. 

```
/*
 * Functional Interface where body is a reference to instance method of some other
 * class
 */
interface PersonOperationsCheckArbitrary {

	boolean isFirstPersonLarger(Person p1, Person p2);
}
```

```
/*
 * Class which contains method body we want to refer to
 *
 */
class Person {

	private String name;
	private Integer age;

	public Person(String name, Integer age) {
		super();
		this.name = name;
		this.age = age;
	}

	public String getName() {
		return name;
	}

	public void setName(String name) {
		this.name = name;
	}

	public Integer getAge() {
		return age;
	}

	public void setAge(Integer age) {
		this.age = age;
	}

	@Override
	public String toString() {
		return "Person [name=" + name + ", age=" + age + "]";
	}
	
	public boolean isFirstLarger(Person p) {
		return this.getAge() >= p.getAge();
	}
}

```

```
/*
 * Using Lambda
 *
 */
 PersonOperationsCheckArbitraryDiffTypes instanceMethodInStaticStyleDiffParams = new Person().isFirstLargerInteger(p1, p2);
```

```
/*
 * Using Instance Method Reference by Class
 *
 */
 PersonOperationsCheckArbitraryDiffTypes instanceMethodInStaticStyleDiffParams = Person::isFirstLargerInteger;
`
