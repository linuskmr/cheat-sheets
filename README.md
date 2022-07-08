# Cheat Sheets

Here are my own cheat sheets for various programming languages.

[Python](python)

[Rust](rust)

[C/C++](c)

[LaTeX](latex)

[Java](java)

[Web best practices tools](web)

[Javascript](js)

## Common

### Sentinal Values

Don't use `-1` for error codes, like `string.indexOf('x') == -1`. In [Rust](rust), use `Option`. In other languages, throw an Exception[^sentinal].

[^sentinal]: https://adventures.michaelfbryan.com/posts/rust-best-practices/bad-habits/#using-sentinel-values

### Don't initialize after construction

Bad:

```rust
let mut dict = Dictionary::new();
// read the file and populate some internal HashMap or Vec
dict.load_from_file("./words.txt")?;
```

Good:

```rust
Dictionary::from_file("./words.txt")?;
```

[^init-after-construction]

[^init-after-construction]: https://adventures.michaelfbryan.com/posts/rust-best-practices/bad-habits/#initialize-after-construction

### Attention for readonly getters

E.g. in python retuning a list from a getter and not providing a setter doesn't ensure the list or the items don't change[^readonly-getters].

[^readonly-getters]: https://adventures.michaelfbryan.com/posts/rust-best-practices/bad-habits/#defensive-copies
