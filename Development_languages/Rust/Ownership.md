Ownership
------

Rust central feature is ownership, the rules assiciated with are:
- Each value has a viable that's called it's `owner`
```Rust
let str1 = "super string";
```
The owner here is `str1`

- There can only be one owner at a time
That mean that only one variable name can be the owner of the memory place where "super string" string is located.

- When the owner goes out of the scope, the value will be droped
```Rust
{
	let str1 = "super string 1";
}
println!("str1 contain: {}", str1);
```
This program won't compile because the declaration line and `println!()` are not in the same scope.

Dangling references, is a pointer that references a location in memory that may have been given to someone else, by freeing some memory while preserving a pointer to that memory.
```Rust
fn main() {
    let reference_to_nothing = dangle();
}

fn dangle() -> &String {
    let s = String::from("hello");

    &s
}
```
The compilator whill prevent you from this type of error.
