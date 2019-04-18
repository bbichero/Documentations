Tests
------

Create a test function:
add `#[test]` attribute before the `fn` line
```
#[test]
fn it_works() {
	assert_eq!(2 + 2, 4);
}
```

Excute command `cargo test` to run all tests in projects.
