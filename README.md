# Vanity address searcher

A blazingly fast vanity address generator written with the Rust programming language.  Supporting Bitcoin (always included), Ethereum, and Solana (via optional features).

With btc-vanity, you can generate wallets that have custom addresses with prefixes, suffixes, substrings, or even regex patterns. It's designed for **speed**, **flexibility**, and **security**.

You can easily run the btc-vanity terminal application locally or use it as a library to create your vanity keypairs securely.

## Key Features

**Multi-Chain Support**:
*   **Bitcoin:** Always included.
*   **Ethereum:**  Enabled via the `ethereum` feature.
*   **Solana:** Enabled via the `solana` feature.

**Advanced Customization**: Match prefixes, suffixes, substrings, or regex-based patterns with optional case insensitivity. <br>
**Blazingly Fast Performance**: Fully utilize your hardware with customizable thread counts. <br>
**Batch File Support**: Bulk generate addresses using input files with desired patterns. <br>

## Installation

### CLI

Install the binary using `cargo`:

```bash
cargo install btc-vanity  # Installs Bitcoin support only (default)
cargo install btc-vanity --features ethereum  # Installs with Ethereum support
cargo install btc-vanity --features solana    # Installs with Solana support
cargo install btc-vanity --features all       # Installs with all features (Bitcoin, Ethereum, Solana)
```

**Important:**  You *must* use the `--features` flag to enable Ethereum and/or Solana support.  If you omit the flag, you'll only get Bitcoin functionality.

### Library

Include `btc-vanity` in your `Cargo.toml`:

```toml
[dependencies]
btc-vanity = "2.1.0"  # Bitcoin support only

# For Ethereum support:
# btc-vanity = { version = "2.1.0", features = ["ethereum"] }

# For Solana support:
# btc-vanity = { version = "2.1.0", features = ["solana"] }

# For all features:
# btc-vanity = { version = "2.1.0", features = ["all"] }
```

Crate on [crates.io](https://crates.io/crates/btc-vanity) <br>
Documentation on [docs.rs](https://docs.rs/btc-vanity/latest/btc_vanity/index.html)

## CLI Usage

### Basic CLI Syntax

The CLI tool provides several options to customize your address generation:

```shell
$ btc-vanity [OPTIONS] <PATTERN>
```

#### Blockchain Selection

*   `--btc`: Generates Bitcoin keypairs and addresses. (Always available)
*   `--eth`: Generates Ethereum keypairs and addresses. (**Requires the `ethereum` feature**)
*   `--sol`: Generates Solana keypairs and addresses. (**Requires the `solana` feature**)

#### General Options

*   `-i, --input-file <FILE>`: Reads patterns and flags from the specified file (one pattern per line).
*   `-o, --output-file <FILE>`: Saves generated wallet details to the specified file.
*   `-t, --threads <N>`: Sets the number of threads for address generation.
*   `-f, --force-flags`: Forces CLI flags to override flags in the input file.
*   `-d, --disable-fast`: Disables fast mode (allows longer patterns).

#### Matching Options

*   `-p, --prefix`: Matches the pattern as a prefix (default).
*   `-s, --suffix`: Matches the pattern as a suffix.
*   `-a, --anywhere`: Matches the pattern anywhere in the address.
*   `-r, --regex <REGEX>`: Matches addresses using a regular expression.
*   `-c, --case-sensitive`: Enables case-sensitive matching.

### Bitcoin CLI Examples

These examples *always* work, as Bitcoin support is always included.

Generate a Bitcoin address with prefix `1Emiv` (case-insensitive):

```shell
$ btc-vanity Emiv
```

Generate a Bitcoin address containing the substring `test` (case-sensitive):

```shell
$ btc-vanity -a -c test
```

Generate a Bitcoin address using a regex pattern `^1E.*T$`:

```shell
$ btc-vanity -r "^1E.*T$"
```

Generate multiple Bitcoin addresses and save to `wallets.txt`:

> [!NOTE]
> -f flag will override any pattern flags inside the `input-file.txt`.
> For example if there line `emiv -s --eth` will become `emiv -p --btc -c`.
> The resulting wallet will be printed in `wallets.txt`.

```shell
$ btc-vanity -f --btc -p -c -i input-file.txt -o wallets.txt
```
### Ethereum and Solana CLI Examples
**Important:** These commands *require* that you installed `btc-vanity` with the appropriate features (see Installation section above).
Generate an Ethereum address starting with 0xdead with 8 threads:
```shell
# Ensure you installed with: cargo install btc-vanity --features ethereum
$ btc-vanity --eth -t 8 dead
```

Generate a Solana address ending with 123:
```shell
# Ensure you installed with: cargo install btc-vanity --features solana
$ btc-vanity --sol -s 123
```

Remember, the security of your cryptocurrency holdings is paramount. Always prioritize the safety and security of your assets.
