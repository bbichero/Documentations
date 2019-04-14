Traits
------

`trait` are like `interfaces` in other languages
It's use for differents types that share the same behavior, call the same method for all the types.
Trait definitions are a way to group method signatures together.

We need to define, `trait`, `struct` and `impl`
```Rust
pub trait Summary {
    fn summarize(&self) -> String;
}
```
See the full example [here](https://gitlab.com/bbichero/rust-learning/traits/src/main.rs)

To display trait, you need to implement a method that return a `String` in it and call it.

`trait` can also implement default return 
