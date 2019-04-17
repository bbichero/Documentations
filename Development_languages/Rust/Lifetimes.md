Lifetimes
------

When a function return a reference on a variable, the rust compiler throw you an error about a missing lifetime parameter
Let's see a simple example:
```Rust
fn longuest(str1: &str, str2: &str) -> &str {
    if str1.len() > str2.len() {
        str1
    } else {
        str2
    }
}

fn main() {
    str1 = String::from("super string 1");
    str2 = "String 2";

    println!("the longest string is: {}", longest(str1.as_str(), str2));
}
```

The compilator throw us :
```
error[E0106]: missing lifetime specifier
 --> src/main.rs:1:40
  |
1 | fn longuest(str1: &str, str2: &str) -> &str {
  |                                        ^ expected lifetime parameter
  |
  = help: this function's return type contains a borrowed value, but the signature does not say whether it is borrowed from `str1` or `str2`
```

The names of lifetime parameters must start with an apostrophe (') and are usually all lowercase and very short, like generic types.
Like:
```
&i32        // a reference
&'a i32     // a reference with an explicit lifetime
&'a mut i32 // a mutable reference with an explicit lifetime
```

The compiler uses three rules to figure out what lifetimes references have when there aren't explicit annotations.
- Each parameter that is a reference gets its own lifetime parameter. (one lifetime parameters by reference parameter)
- If there is exactly  one input lifetime parameter, that lifetime is assigned to all ouput lifetime parameters
- If there are multiple input lifetime parameters, but one of them is `&slef` of `&mut self`, the lifetime of `self` is assigned to all ouput lifetime parameters.
