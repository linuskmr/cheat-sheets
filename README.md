# Cheat Sheets

Here are my own cheat sheets for various programming languages.

[Python](python)

[Rust](rust.md)

## Common

### Sentinal Values

Don't use `-1` for error codes, like `string.indexOf('x') == -1`. In [Rust](rust.md), use `Option`. In other languages, throw an Exception.

> From https://adventures.michaelfbryan.com/posts/rust-best-practices/bad-habits/#using-sentinel-values

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

> From https://adventures.michaelfbryan.com/posts/rust-best-practices/bad-habits/#initialize-after-construction

### Attention for readonly getters

E.g. in python retuning a list from a getter and not providing a setter doesn't ensure the list or the items don't change.

> From https://adventures.michaelfbryan.com/posts/rust-best-practices/bad-habits/#defensive-copies
