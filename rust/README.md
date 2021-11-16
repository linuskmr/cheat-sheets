## Rust Cheat Sheet

See also https://www.programming-idioms.org/cheatsheet/Rust

```rust
// Line comment
/* Block comment*/
/// Doc comment
//! Doc comment for module
```

## Inline if else with return value

```rust
let sign = if value >= 0 { '+' } else { '-' };
```

## Inline foreach loop

```rust
for cty in ["Amsterdam", "Berlin", "New York"].iter() {
  println!("{}", city);
}
```

## Shadowing variables

```rust
let answer = "42";
let answer: i32 = number.parse();
// Instead of
let answer = "42";
let answer_int = number.parser();
```

## Tuple with one element (like in Python):

```rust
let tuple = (42, );
```

## Destructuring a tuple

```rust
let (a, b, c) = (42, 19, 51);
assert_eq!(a, 42);
assert_eq!(b, 19);
assert_eq!(c, 51);

// Destructuring in function
fn format_coordinates([x, y]: [f32; 2]) -> String {
    format!("{}|{}", x, y)
}
```

[^destructuring-in-function]
[^destructuring-in-function]: https://adventures.michaelfbryan.com/posts/daily/slice-patterns/#irrefutable-pattern-matching

## Destructuring a struct

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

## Fill array/vector


```rust
// Array with known size at compile time filled with 42x zeros:
let a = [0u; 42];

// Vector filled with 42x zeros. 
let v = vec![0u; 42];
```

## Get the size of a type/variable

```rust
// For a static sized type at compile time
let u32_size = std::mem::size_of::<u32>();
assert_eq!(a_size, 4);

// For a variable at runtime
let v = vec![0; 10];
let v_size = std::mem::size_of_val(&v);
assert_eq!(v_size, 24);
```

## Read a string from stdin and parse it to a number

```rust
let mut input = String::new();
std::io::stdin()::read_line(&mut input)?;
let input_number: i32 = input.trim().parse()?;
```

## Return a value from a loop

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

## Shorthand struct initialization

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

## Struct update syntax

Copies all missing fileds from another struct

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

## Execute a funtion for every element in an iterator and also execute another function, if it is not the last element

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

## Capture values in match

```rust
enum Message {
  Hello {id: i32},
}

match msg {
  Message::Hello { id: id_value @ 3..7 } => println!("In range 3..7: {}", id_value),
  Message::Hello { id } => println!("Other: {}", id),
}
```

## Use implementation of trait by disambiguate with `as`

```rust
trait Animal {
    fn name() -> &'static str;
}

struct Cat {}

impl Animal for Cat {
    fn name() -> &'static str {
        "Cat is Animal"
    }
}

impl Cat {
    fn name() -> &'static str {
        "Cat"
    }
}

fn main() {
    assert_eq!(Cat::name(), "Cat"); // Method of impl Cat
    assert_eq!(<Cat as Animal>::name(), "Cat is Animal"); // Method of impl Animal for Cat
}
```

[^disambiguate-as]
[^disambiguate-as]: https://doc.rust-lang.org/book/ch19-03-advanced-traits.html

## Default generic type parameters in traits

```rust
trait Add<Rhs=Self> {
    type Output;

    fn add(self, rhs: Rhs) -> Self::Output;
}
```

[^default-generic-type-parameter]
[^default-generic-type-parameter]: https://doc.rust-lang.org/book/ch19-03-advanced-traits.html

## Supertraits

Specify that a trait will only work for types that also implement another trait (the supertrait)

```rust
use std::fmt;

trait OutlinePrint: fmt::Display {
    fn outline_print(&self) {
        let output = self.to_string();
        let len = output.len();
        println!("{}", "*".repeat(len + 4));
        println!("*{}*", " ".repeat(len + 2));
        println!("* {} *", output);
        println!("*{}*", " ".repeat(len + 2));
        println!("{}", "*".repeat(len + 4));
    }
}
```

[^supertrait]
[^supertrait]:  https://doc.rust-lang.org/book/ch19-03-advanced-traits.html

## Ophan Rule

You can implement a trait on a type a long as either the trait or the type are local to our crate.

```rust
trait Number {
    /// Get the value of the number as i32.
    fn value(&self) -> i32;

    /// Doubles the number.
    fn double(&self) -> i32 {
        self.value() * 2
    }
}

// Can implement Number for i32, because the trait `Number` is local to this crate.
impl Number for i32 {
    fn value(&self) -> i32 {
        *self
    }
}

fn main() {
    assert_eq!(10.double(), 20);
}
```

## Generic type alias

```rust
type ResultStringError<T> = Result<T, String>;
```

## Drop behavior of temporary variables

"The code in Listing 20-20 that uses `let job = receiver.lock().unwrap().recv().unwrap();` works because with let, any temporary values used in the expression on the right hand side of the equals sign are immediately dropped when the let statement ends. However, `while let` (and `if let` and `match`) does not drop temporary values until the end of the associated block. In Listing 20-21, the lock remains held for the duration of the call to `job()`, meaning other workers cannot receive jobs."[^drop-temp-val]

[^drop-temp-val]: https://doc.rust-lang.org/book/ch20-02-multithreaded.html

```rust
impl Worker {
    fn new(id: usize, receiver: Arc<Mutex<mpsc::Receiver<Job>>>) -> Worker {
        let thread = thread::spawn(move || {
            while let Ok(job) = receiver.lock().unwrap().recv() {
                println!("Worker {} got a job; executing.", id);

                job();
            }
        });

        Worker { id, thread }
    }
}
```

[^drop-temp-val]

## Function references and closures

- All closures implement [`FnOnce`](https://doc.rust-lang.org/std/ops/trait.FnOnce.html). Called with `self`, `&self` or `&mut self`.
- Functions that can be called with `&mut self` (or `&self`) implement [`FnMut`](https://doc.rust-lang.org/std/ops/trait.FnMut.html).
- Functions that can be called with `&self` implement [`Fn`](https://doc.rust-lang.org/std/ops/trait.Fn.html).

[^fn-fnmut-fnonce]
[^fn-fnmut-fnonce]: https://stackoverflow.com/a/30232500

Function references are of type `fn()`, but closures are of type `Fn()`. You can use a function reference `fn()` everywhere where a closure `Fn()` is allowed.

```rust
let v = vec![1, 2, 3];
let vs: Vec<String> = v.iter().map(ToString::to_string).collect();
```

## Submodule `mod.rs`

> Instead of `foo/mod.rs` you can now (in Rust 2018) can name the file simply `foo.rs` and put the other files related to the submodule in `foo/`[^submodule-mod-rs].

[^submodule-mod-rs]: https://doc.rust-lang.org/edition-guide/rust-2018/path-changes.html#no-more-modrs

## Slice Patterns

> This part is from https://adventures.michaelfbryan.com/posts/daily/slice-patterns

### Handling Plurality

```rust
match words {
  [] => (), // Zero elements
  [word] => (), // One element
  _ => (), // Multiple elements
}
```
[^handling-plurality]
[^handling-plurality]: https://adventures.michaelfbryan.com/posts/daily/slice-patterns/#handling-plurality

### Matching start

```rust
match text {
  ['H', 'e', 'l', 'l', 'o'] => (), // test starts with Hello
  _ => (),
}
```

[^matching-start]
[^matching-start]: https://adventures.michaelfbryan.com/posts/daily/slice-patterns/#matching-the-start-of-a-slice

### Palindrom check

```rust
fn is_palindrome(items: &[char]) -> bool {
    match items {
        [first, middle @ .., last] => first == last && is_palindrome(middle),
        [] | [_] => true,
    }
}
```

[^palindrome-check]
[^palindrome-check]: https://adventures.michaelfbryan.com/posts/daily/slice-patterns/#checking-for-palindromes

### Argparser with slice patterns

```rust
loop {
    match args {
        ["-h" | "--help", ..] => {
            eprintln!("Usage: main [--input <filename>] [--count <count>] <args>...");
            std::process::exit(1);
        }
        ["-i" | "--input", filename, rest @ ..] => {
            input = filename.to_string();
            args = rest;
        }
        ["-c" | "--count", c, rest @ ..] => {
            count = c.parse().unwrap();
            args = rest;
        }
        [..] => break,
    }
}
```

[^argparser-slice-patterns]
[^argparser-slice-patterns]: https://adventures.michaelfbryan.com/posts/daily/slice-patterns/#irrefutable-pattern-matching

## impl in parameters and return

`impl` in function parameters is like a generic type, so `fn foo<T: Debug>(obj: T)` is equivalent to `fn foo(obj: impl Debug)`.

But `impl` as return type specifies an unboxed abstract return type, so the caller can only access method of the trait,
not the concrete returned object.

This is useful for [returning unboxed closures](https://doc.rust-lang.org/reference/types/impl-trait.html#abstract-return-types).

> With impl Trait, unlike with a generic type parameter, the function chooses the return type, and the caller cannot choose the return type[^impl-return].
[^impl-return]: https://doc.rust-lang.org/reference/types/impl-trait.html#differences-between-generics-and-impl-trait-in-return-position

## Into

`Into` may be used for functions that need an owned value and don't care about if the original is an owned or borrowed value.

```rust
#[derive(Debug)]
struct Person {
    name: String,
}

impl Person {
    fn new(name: impl Into<String>) -> Self {
        // name.into() converts name into an owned string.
        // This also works if name is a &str.
        Self { name: name.into() }
    }
}

fn main() {
    let p: Person = Person::new("Rust");
    println!("{:?}", p);
}
```

[^into]
[^into]: https://github.com/pretzelhammer/rust-blog/blob/master/posts/tour-of-rusts-standard-library-traits.md#conversion-traits
