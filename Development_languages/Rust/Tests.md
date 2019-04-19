Tests
------

Excute command `cargo test` to run all tests in projects.

List of `assert!` test macros:
- `assert!`, boolean check (can take multiple arguments)
- `assert_eq!`, take 2 arguments and verify if there are equal
- `assert_ne!`, take 2 arguments and verify if there are not equal    
(used when the test MUST NOT return the value sent)

Create a test function:
add `#[test]` attribute before the `fn` line
```
#[test]
fn it_works() {
	assert_eq!(2 + 2, 4);
}
```
You can add `#[should_panic]` after `#[test]` attribute to check    
if the code succefully panic.
Because `should_panic` is inaccurate, we can me more specific by    
using `expected` parameter to specify a string.    
```
#[test]
#[should_panic(expected = "String display when panic")]
```
