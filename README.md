# rosbag-rs

[![Crate][crate-image]][crate-link]
[![Docs][docs-image]][docs-link]
![Apache2/MIT licensed][license-image]
![Rust Version][rustc-image]
[![Build Status][build-image]][build-link]
[![Dependency Status][deps-image]][deps-link]

A pure Rust crate for reading ROS bag files.

## Example
```rust
use rosbag::{ChunkRecord, MessageRecord, IndexRecord, RosBag};

let bag = RosBag::new(path)?;
// Iterate over records in the chunk section
for record in bag.chunk_records() {
    match record? {
        ChunkRecord::Chunk(chunk) => {
            // iterate over messages in the chunk
            for msg in chunk.messages() {
                match msg? {
                    MessageRecord::MessageData(msg_data) => {
                        // ..
                    }
                    MessageRecord::Connection(conn) => {
                        // ..
                    }
                }
            }
        },
        ChunkRecord::IndexData(index_data) => {
            // ..
        },
    }
}
// Iterate over records in the index section
for record in bag.index_records() {
    match record? {
        IndexRecord::IndexData(index_data) => {
            // ..
        }
        IndexRecord::Connection(conn) => {
            // ..
        }
        IndexRecord::ChunkInfo(chunk_info) => {
            // ..
        }
    }
}
```

## License

The crate is licensed under either of

 * Apache License, Version 2.0, ([LICENSE-APACHE](LICENSE-APACHE) or http://www.apache.org/licenses/LICENSE-2.0)
 * MIT license ([LICENSE-MIT](LICENSE-MIT) or http://opensource.org/licenses/MIT)

at your option.

### Contribution

Unless you explicitly state otherwise, any contribution intentionally submitted
for inclusion in the work by you, as defined in the Apache-2.0 license, shall be dual licensed as above, without any
additional terms or conditions.

[//]: # (badges)

[crate-image]: https://img.shields.io/crates/v/rosbag.svg
[crate-link]: https://crates.io/crates/rosbag
[docs-image]: https://docs.rs/rosbag/badge.svg
[docs-link]: https://docs.rs/rosbag
[rustc-image]: https://img.shields.io/badge/rustc-1.63+-blue.svg
[license-image]: https://img.shields.io/badge/license-Apache2.0/MIT-blue.svg
[build-image]: https://github.com/newpavlov/rosbag-rs/actions/workflows/rosbag.yml/badge.svg
[build-link]: https://github.com/newpavlov/rosbag-rs/actions/workflows/rosbag.yml
[deps-image]: https://deps.rs/repo/github/newpavlov/rosbag-rs/status.svg
[deps-link]: https://deps.rs/repo/github/newpavlov/rosbag-rs
