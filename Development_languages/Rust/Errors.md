Errors handling
------

Execute cargo with env variable `RUST_BACKTRACE=1` to display backtrace

Abort on panic => Edit `Cargo.toml` file:
```TOML
[profile.release]
panic = 'abort'
```

Display error message then quit:
```rust
panic!("Error message");
```

If function return a `Result<T, E>`, we must handle error with `match`:
```rust
let f = File::open("hello.txt");
let ret = match f {
    Ok(file) => file,
    Err(error) => {
        panic!("There was a problem opening the file: {:?}", error)
    },
};
```

use `unwrap_or_else` when dealing with errors, instead of match, code is cleaner:
```rust
let f = File::open("hello.txt");
let ret = File::open("hello.txt").unwrap_or_else(|error| {
    panic!("There was a problem opening the file: {:?}", error);
});
```

`unwrap` keyword will call `panic!` if `Result` return `Err`
```rust
let f = File::open("hello.txt").unwrap();
```
Return:
```
thread 'main' panicked at 'called `Result::unwrap()` on an `Err` value: Os { code: 2, kind: NotFound, message: "No such file or directory" }', src/libcore/result.rs:997:5
note: Run with `RUST_BACKTRACE=1` environment variable to display a backtrace.
```

`expect` keyword can replace `unwrap`, the different here is that it print first the message we send it:
```rust
let f = File::open("hello.txt").expect("Failed to open hello.txt");
```
Return:
```
thread 'main' panicked at 'Failed to open hello.txt: Os { code: 2, kind: NotFound, message: "No such file or directory" }', src/libcore/result.rs:997:5
note: Run with `RUST_BACKTRACE=1` environment variable to display a backtrace.
```

`?` operator, shortcut for propagation Errors
The `?` placed after a Result value is defined to work in almost the same way as the match expressions, but you can use it only in function that return a `Result`
```Rust
File::open("hello.txt")?.read_to_string(&mut s)?;
```

### Use case
- Use `panic!` for alerting person (or you) to the bug in the code (for invalid use of the function / method).
- Use Result when failure is expected
