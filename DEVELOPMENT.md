# Quickstart (GitHub, no local install)

1. Click **Code → Create codespace on main**.
2. In the terminal:
   cargo fmt --all
   cargo clippy --all -- -D warnings
   cargo test --all
3. If you touched the UI:
   cd ui
   npm ci
   npm test

# Local Development

This page contains instructions on how to run everything locally.

## Build from Source

Requirements:
- Rust 1.86+
- npm 10+
- `cargo-deny` (for license/advisory checks)

Build the agentgateway UI:

```bash
cd ui
npm install
npm run build
```

Build the agentgateway binary:

```bash
cd ..
export CARGO_NET_GIT_FETCH_WITH_CLI=true
make build
```

Run the agentgateway binary:

```bash
./target/release/agentgateway
```

Open your browser and navigate to `http://localhost:15000/ui` to see the agentgateway UI.

## Debugging

Enable verbose logging with the `RUST_LOG` environment variable:

```bash
RUST_LOG=agentgateway=debug,tower_http=trace ./target/release/agentgateway
```

For JWT/auth issues specifically:

```bash
RUST_LOG=agentgateway::http::jwt=trace ./target/release/agentgateway
```

## Pre-commit Checks

Run these before opening a PR:

```bash
cargo fmt --all
cargo clippy --all -- -D warnings
cargo deny check
cargo test --all
```

