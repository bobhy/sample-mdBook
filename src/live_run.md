# A live run

To verify you've got the right version of mdBook in path:

```shell
$ mdbook -V
mdbook v0.4.43-extern-crate
```

You run doc tests as usual:

```shell
$ pwd
/home/me/src/localdep/sample-mdBook
$ mdbook test
2024-12-17 02:00:40 [INFO] (mdbook::utils::extern_args): running cd "/home/me/src/localdep/sample-mdBook" && "cargo" "build" "--verbose" "--manifest-path" "/home/me/src/localdep/sample-mdBook/./Cargo.toml"
2024-12-17 02:00:40 [INFO] (mdbook::book): Testing chapter 'The golden sample': "sample.md"
2024-12-17 02:00:40 [INFO] (mdbook::book): Testing chapter 'Setup': "setup.md"
2024-12-17 02:00:41 [INFO] (mdbook::book): Testing chapter 'A live run': "live_run.md"
```

If all tests pass, it's pretty uneventful.

## Run doc tests (failing)

E.g, in the sample, change:

```rust,ignore
assert_eq!(deserialized, Point { x:1, y:2 } );
```

to

```rust,ignore
assert_eq!(deserialized, Point { x:1, y:42 } );
```

Now, it's a bit noisier:

```shell
$ mdbook test
2024-12-17 02:01:44 [INFO] (mdbook::utils::extern_args): running cd "/home/me/src/localdep/sample-mdBook" && "cargo" "build" "--verbose" "--manifest-path" "/home/me/src/localdep/sample-mdBook/./Cargo.toml"
2024-12-17 02:01:44 [INFO] (mdbook::book): Testing chapter 'The golden sample': "sample.md"
2024-12-17 02:01:45 [ERROR] (mdbook::book): rustdoc returned an error:
2024-12-17 02:01:45 [INFO] (mdbook::book): Testing chapter 'A live run': "live_run.md"
--- stdout

running 1 test
test sample.md - A_Sample_of_Doc_Tests_with_External_Crates (line 8) ... FAILED

failures:

---- sample.md - A_Sample_of_Doc_Tests_with_External_Crates (line 8) stdout ----
Test executable failed (exit status: 101).

stdout:
serialized = {"x":1,"y":2}
deserialized = Point { x: 1, y: 2 }

stderr:
thread 'main' panicked at sample.md:27:5:
assertion `left == right` failed
  left: Point { x: 1, y: 2 }
 right: Point { x: 1, y: 42 }
note: run with `RUST_BACKTRACE=1` environment variable to display a backtrace



failures:
    sample.md - A_Sample_of_Doc_Tests_with_External_Crates (line 8)

test result: FAILED. 0 passed; 1 failed; 0 ignored; 0 measured; 0 filtered out; finished in 0.09s


--- stderr

2024-12-17 02:01:45 [INFO] (mdbook::book): Testing chapter 'Setup': "setup.md"
2024-12-17 02:01:45 [ERROR] (mdbook::utils): Error: One or more tests failed
```
