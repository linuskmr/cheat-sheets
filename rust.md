## Rust Cheat Sheet

```rust
// Line comment
/* Block comment*/
/// Doc comment
//! Doc comment for module
```

Inline if else with return value

```rust
let sign = if value >= 0 { '+' } else { '-' };
```

Inline foreach loop:

```rust
for cty in ["Amsterdam", "Berlin", "New York"].iter() {
  println!("{}", city);
}
```

Shadowing variables:

```rust
let x = 42;
let x = "Hello World";
// Not allowed, because assignment with different type is not shadowing:
// x = true;
```

Tuple with one element (like in Python):

```rust
let tuple = (42, );
```

Destructing a tuple:

```rust
let (a, b, c) = (42, 19, 51);
assert_eq!(a, 42);
assert_eq!(b, 19);
assert_eq!(c, 51);
```

Destructing a struct:

```rust
struct Position {
  latitude: f64,
  longitude: f64,
}

let p = Position { latitude: 50.1, longitude: 10.8 };
let Point { latitude: p_lat, longitude: p_lng } = p;
assert_eq!(p_lat, 50.1);
assert_eq!(p_lng, 10.8);
```

Fill array/vector:


```rust
// Array with known size at compile time filled with 42x zeros:
let a = [0u; 42];

// Vector filled with 42x zeros. 
let v = vec![0u; 42];
```

Get the size of a type/variable:

```rust
// For a static sized type at compile time
let u32_size = std::mem::size_of::<u32>();
assert_eq!(a_size, 4);

// For a variable at runtime
let v = vec![0; 10];
let v_size = std::mem::size_of_val(&v);
assert_eq!(v_size, 24);
```

Read a string from stdin and parse it to a number:

```rust
let mut input = String::new();
std::io::stdin()::read_line(&mut input)?;
let input_number: i32 = input.trim().parse()?;
```

Return a value from a loop:

```rust
let mut counter = 0;
let result = {
  loop {
    counter += 1;
    if counter == 10 {
      break counter * 2;
    }
  }
};
assert_eq!(result, 20);
```

Shorthand struct initialization:

```rust
struct Person {
  name: String,
  age: u8,
  id: u32,
}

impl Person {
  fn new(name: String, age: u8) -> Self {
    Person { name, age, id: 42 }
  }
}
```

Struct update syntax, i.e. copy all missing fileds from another struct:

```rust
struct Person {
  name: String,
  age: u8,
  id: u32,
}

fn birthday(person: Person) -> Person {
  Person {age: person.age + 1, ...person}
}
```

Execute a funtion for every element in an iterator and also execute another function, if it is not the last element.

```rust
let v = vec![1, 2, 3, 4, 5, 6];
let mut iter = v.into_iter().peekable();

while let Some(element) = iter.next() {
    // Execute for every element
    print!("{}", element);
    // Only write a `,` if this is not the last element
    if iter.peek().is_some() {
        print!(", ");
    }
}
```

> Note: For simple cases you may better use [Iterator::intersperse](https://doc.rust-lang.org/std/iter/trait.Iterator.html#method.intersperse) or [Vec::join](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.join)
