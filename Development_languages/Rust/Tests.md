Tests
------

### Creation
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

You can ignore a test run with `ignore` attribute:
```
#[ignore]
```

### Execution
Excute command `cargo test` to run all tests in projects.
Tests are run in parallele but you can specify number or thread used.
```
cargo test -- --test-threads=${THREAD_NB}
```

Output printed values for passed tests:
```
cargo test -- --nocapture
```

You can run a specific test with the function name passed to cargo:
```
cargo test ${FUNCTION_NAME}
```

You can also specify a function part name:
```
cargo test ${FUNCTION_PART_NAME}
```

To run only the ignored test:
```
cargo test -- --ignored
```

### Integrations tests
In Rust, integration tests are entirely external to your library. They use your library in the same way any other code would,    
which means they can only call functions that are part of your library’s public API.    
Their purpose is to test whether many parts of your library work together correctly.    
Units of code that work correctly on their own could have problems when integrated, so test coverage of the integrated code is important as well.    
To create integration tests, you first need a tests directory

To run a specific integration test:
```
cargo test --test ${INTEGRATION_TEST_NAME}
```

### Unitary tests
The purpose of unit tests is to test each unit of code in isolation from the rest of the code to quickly pinpoint where code is and isn’t working as expected.    
You’ll put unit tests in the src directory in each file with the code that they’re testing.    
The convention is to create a module named tests in each file to contain the test functions and to annotate the module with cfg(test).
