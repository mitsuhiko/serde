# Serde &emsp; [![Build Status]][travis] [![Latest Version]][crates.io]

[Build Status]: https://api.travis-ci.org/serde-rs/serde.svg?branch=master
[travis]: https://travis-ci.org/serde-rs/serde
[Latest Version]: https://img.shields.io/crates/v/serde.svg
[crates.io]: https://crates.io/crates/serde

**Serde is a framework for *ser*ializing and *de*serializing Rust data structures efficiently and generically.**

---

You may be looking for:

- [An overview of Serde](https://serde.rs/)
- [Data formats supported by Serde](https://serde.rs/#data-formats)
- [Setting up `#[derive(Serialize, Deserialize)]`](https://serde.rs/codegen.html)
- [Examples](https://serde.rs/examples.html)
- [API documentation](https://docs.serde.rs/serde/)
- [Release notes](https://github.com/serde-rs/serde/releases)

## Serde in action

<details>
<summary>
Click to show Cargo.toml.
<a href="http://play.integer32.com/?gist=9003c5b88c1f4989941925d7190c6eec" target="_blank">Run this code in the playground.</a>
</summary>

```toml
[dependencies]

# The core APIs, including the Serialize and Deserialize traits. Always
# required when using Serde.
serde = "1.0"

# Support for #[derive(Serialize, Deserialize)]. Required if you want Serde
# to work for structs and enums defined in your crate.
serde_derive = "1.0"

# Each data format lives in its own crate; the sample code below uses JSON
# but you may be using a different one.
serde_json = "1.0"
```

</details>
<p></p>

```rust
#[macro_use]
extern crate serde_derive;

extern crate serde;
extern crate serde_json;

#[derive(Serialize, Deserialize, Debug)]
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

    // Convert the JSON string back to a Point.
    let deserialized: Point = serde_json::from_str(&serialized).unwrap();

    // Prints deserialized = Point { x: 1, y: 2 }
    println!("deserialized = {:?}", deserialized);
}
```

## Getting help

Serde developers live in the #serde channel on
[`irc.mozilla.org`](https://wiki.mozilla.org/IRC). The #rust channel is also a
good resource with generally faster response time but less specific knowledge
about Serde. If IRC is not your thing or you don't get a good response, we are
happy to respond to [GitHub issues](https://github.com/serde-rs/serde/issues/new)
as well.

## no-std
Serde has a feature named std enabled by default.
In order to to use Serde in a no_std context the std feature has to be disabled.
To do that add the following to your Cargo.toml:

```
[dependencies]
serde = { version = "1.0.27", default-features = false }
```

Also, note that this implies that there is no memory allocator enabled by
default. Therefore, if you have access to heap memory and want to use modules
from the standard library such as String, Vec or similar you need to explicitly
define which memory allocator to use. There are a number of different memory
allocators available for that, for example
[alloc](https://doc.rust-lang.org/nightly/alloc/index.html) that the standard
library in Rust is using.

## License

Serde is licensed under either of

 * Apache License, Version 2.0, ([LICENSE-APACHE](LICENSE-APACHE) or
   http://www.apache.org/licenses/LICENSE-2.0)
 * MIT license ([LICENSE-MIT](LICENSE-MIT) or
   http://opensource.org/licenses/MIT)

at your option.

### Contribution

Unless you explicitly state otherwise, any contribution intentionally submitted
for inclusion in Serde by you, as defined in the Apache-2.0 license, shall be
dual licensed as above, without any additional terms or conditions.
