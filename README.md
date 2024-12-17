# Sample of mdBook doctests using external crates

There's a [PR pending at the mdBook project](https://github.com/rust-lang/mdBook/pull/2503) 
which supports doctests using external crates.  
mdBook currently supports this only for legacy Rust.

The current repo demonstrates how to use the proposed version of mdBook.

You can get the proposed version at: https://github.com/bobhy/mdBook/tree/extern_crate

To install it:
```shell
$ cargo install --git=https://github.com/bobhy/mdBook --branch=extern_crate_dist mdbook
$ mdbook -V
mdbook v0.4.43-extern-crate
```
(note updated version string so we can keep problem reports straight)

It seems to be working for me, and I'm prepared to help you use it, too.
Also, if you can help expedite review of the PR over at mdBook, please
put in a good word and see if we can't get it released!
