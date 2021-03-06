# lgpl-docs

LGPL-licensed docs for Gtk-rs crates.

## Structure

The docs for each library come from two files:

 * `docs.rs` is maintained manually, its entries take precedence over the
   `vendor.rs` file. PRs should normally target this file.

 * `vendor.rs` is generated by [gir] via simple transformation of the upstream
   docs found in [GIR definitions]. It serves as a fallback, the docs in it are
   tailored for C not Rust. This file should not be hand-edited.

You can generate it as follows:

```
cd gir
cargo run --release -- -c ../your-repo/Gir.toml -d ../gir-files/ -o ../your-repo/ -m doc
```

Cairo, which lacks GIR definitions, doesn't have a `vendor.rs` file.

[GIR definitions]: https://github.com/gtk-rs/gir-files
[gir]: https://github.com/gtk-rs/gir

## Format

The format of the files is Markdown with extra metadata in HTML-like comments,
which ties each entry to a specific Rust item. For example, this rustdoc
snippet:

```rust
impl Button {
    /// Creates a new `Button` widget. To add a child widget to the button,
    /// use `Container::add`.
    ///
    /// # Returns
    ///
    /// The newly created `Button` widget.
    pub fn new() -> Button {
```

corresponds to this entry in `gtk/vendor.md`:

```
<!-- impl Button::fn new -->
Creates a new `Button` widget. To add a child widget to the button,
use `Container::add`.

# Returns

The newly created `Button` widget.
```

## License

LGPL
