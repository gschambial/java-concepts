# Optional
A container object which may or may not contain a non-null value. If a value is present, isPresent() will return true and get() will return the value.

Additional methods that depend on the presence or absence of a contained value are provided, such as orElse() (return a default value if value not present) and ifPresent() (execute a block of code if the value is present). 

## Advantages

- Null checks are not required.
- No more NullPointerException at run-time.
- We can develop a clean and neat APIs.
- No more Boilerplate code
