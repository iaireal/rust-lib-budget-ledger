# rust-lib-budget-ledger

A Rust library for the bookkeeping rules of [iaireal](https://github.com/iaireal), private
personal budgeting for Brazilians. The crate is named `budget-ledger`.

## Status

The library is at its very beginning. Today it has a single placeholder function, `add`,
which exists so the other iaireal repositories have something to depend on while the
project's structure is built. None of the bookkeeping described below is implemented yet.

## What it is for

iaireal combines two methods, and this library is where their rules will live:

- **Double-entry bookkeeping.** Every real a person owns or owes is tracked. A transaction
  has two or more legs, and the legs always sum to zero: money never appears or
  disappears, it only moves between accounts.
- **Envelope budgeting.** Every real of income is assigned to a category for the month.
  What is left over in a category, or overspent, carries over to the next month.

The library holds only these rules. It does not store data, talk to a database or know
about the web. Programs that do those things, such as the iaireal Lambda functions, call
the library, so the rules are written and tested in one place.

## Using it

The library is not published on crates.io. Depend on it through its git URL in
`Cargo.toml`:

```toml
[dependencies]
budget-ledger = { git = "https://github.com/iaireal/rust-lib-budget-ledger", version = "0.1.0" }
```

In Rust code the crate is called `budget_ledger`, with an underscore:

```rust
let sum = budget_ledger::add(2, 3);
assert_eq!(sum, 5);
```

[lambda-budget-ledger-add](https://github.com/iaireal/lambda-budget-ledger-add) is a
complete example of a program that uses the library.

## Development

Requires [Rust](https://rustup.rs) 1.85 or later (the package uses the 2024 edition).

```bash
cargo test                                   # run the tests
cargo fmt                                    # format the code
cargo clippy --all-targets -- -D warnings    # run the linter
```

| Path | Contents |
| ---- | -------- |
| `src/lib.rs` | The library and its tests |
| `Cargo.toml` | The Rust package and its dependencies |
