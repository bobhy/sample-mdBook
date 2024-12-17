# A Sample of Doc Tests with External Crates

`serde` is not part of the Rust standard library, though, considering its importance and ubiquity within the ecosystem, it arguably could have been.
So, Rust code must `use serde;` as an external crate to take advantage of its capabilities.

Here's a code sample for `serde` in an mdBook page, decorated with assertions to make it interesting as a doctest.

```rust,editable
use serde::{Serialize, Deserialize};

#[derive(Serialize, Deserialize, Debug, PartialEq)]
struct Point {
    x: i32,
    y: i32,
}

fn main() {
    let point = Point { x: 1, y: 2 };

    // Convert the Point to a JSON string.
    let serialized = serde_json::to_string(&point).unwrap();

    // Prints serialized = {"x":1,"y":2}
    println!("serialized = {}", serialized);

    assert_eq!(serialized, r#"{"x":1,"y":2}"#);
    
    // Convert the JSON string back to a Point.
    let deserialized: Point = serde_json::from_str(&serialized).unwrap();

    // Prints deserialized = Point { x: 1, y: 2 }
    println!("deserialized = {:?}", deserialized);

    assert_eq!(deserialized, Point { x:1, y:2 } );
}
```

If you have cloned this repository, try `mdbook test` to see for yourself.

Refer to [A live run](./live_run.md) to see my record of it running for posterity.
