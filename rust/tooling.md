![](https://fasterthanli.me/content/articles/why-is-my-rust-build-so-slow/assets/rust-build-pipeline.9df86fe8c41f18cc.svg)

> `cargo` invokes `rustc` once per crate
> 
> `rustc` decides how many "codegen units" to do in parallel, writes them as `.o` files, then archives them in an `.rlib`
> 
> `cargo` does one final `rustc` invocation with all the required `.rlib`, which ends up calling the linker to make a binary
> 
> From https://fasterthanli.me/articles/why-is-my-rust-build-so-slow

More on `.a` archives in `cheat-sheets/c`.
