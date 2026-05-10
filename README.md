# lava

A community-maintained multi-tool for the [Magma computational algebra system](https://magma.maths.usyd.edu.au/), written in Rust.

## Features

- **`format`** — opinionated source code formatter. Re-implements and extends the upstream [topiary](https://github.com/tweag/topiary) CLI for Magma.
- **`highlight`** — syntax-highlighted terminal (ANSI) and HTML output.
- **`parse`** — pretty-print a Magma source tree (planned for v0.2)

## Install

### Pre-built binaries (recommended)

Run the installer script, which auto-detects your platform and downloads the latest release:

```bash
curl --proto '=https' --tlsv1.2 -LsSf https://github.com/havarddj/lava/releases/latest/download/lava-cli-installer.sh | sh
```

The binary is installed to `~/.cargo/bin` by default.

### From source

Requires Rust 1.85+ (2024 edition):

```bash
git clone https://github.com/havarddj/lava.git
cd lava
cargo install --path crates/lava
```

The `lava` binary is placed in `~/.cargo/bin` by default.


## Usage

```bash
# Format to stdout
lava format file.m

# Format in-place
lava format -w file.m

# Check formatting (CI-friendly)
lava format --check file.m

# Highlight to terminal (ANSI colours)
lava highlight file.m

# Highlight to HTML
lava highlight --html file.m > out.html
```

## Workspace layout

```
.
├── Cargo.toml                 # Virtual workspace
├── crates/
│   ├── lava/                  # CLI binary (lava-cli)
│   └── lava-core/             # Formatting library
└── ...
```

- **`lava-core`** — Query resolution, error types, and the synchronous `format_str` API backed by [topiary-core](https://github.com/tweag/topiary) and [tree-sitter-magma](https://github.com/edgarcosta/tree-sitter-magma).
- **`lava-cli`** — `clap`-driven CLI with subcommands, recursive directory walking, atomic file writes, and diff output for `--check`.

## License

MIT
