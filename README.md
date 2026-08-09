# titans-rs

Work in progress: a Rust implementation of the Titans ML paper ([arXiv:2501.00663](https://arxiv.org/pdf/2501.00663)).

## Paper

- Title: *Titans: Learning to Memorize at Test Time*
- Link: [https://arxiv.org/pdf/2501.00663](https://arxiv.org/pdf/2501.00663)

## Key Ideas from the Paper

- Introduces a neural long-term memory module that updates at test time.
- Treats attention as short-term memory and the neural memory as long-term memory.
- Uses surprise-driven memory updates (gradient-based) with momentum-like carryover.
- Uses adaptive forgetting/decay to manage memory capacity over long sequences.
- Proposes three architecture variants:
  - MAC: Memory As Context
  - MAG: Memory As Gate
  - MAL: Memory As Layer
- Includes persistent memory (learned task-level, input-independent memory tokens).
- Reports strong long-context behavior and scaling claims (including 2M+ context).

## What This Repository Is Implementing

This repository is an in-progress Rust implementation of the Titans design, with an emphasis on correctness, modularity, and reproducible experiments.

### Minimal Viable Prototype (build first)

1. Core sequence model scaffold in Rust (tensor ops + training loop).
2. Neural long-term memory module with:
   - Surprise-based update signal
   - Momentum-like surprise accumulator
   - Forget/decay gate
3. Retrieval path from long-term memory using query projections.
4. One integrated variant (recommended first: MAC) end-to-end.
5. Basic synthetic long-context tasks for sanity checks.

### Next Milestones (after MVP)

1. Add remaining integration variants (MAG, MAL).
2. Add persistent memory tokens and ablations.
3. Add chunked/parallel-friendly memory update path.
4. Reproduce small-scale benchmark slices:
   - Language modeling (small setup)
   - Needle-in-a-haystack style retrieval
   - Time-series or genomics toy benchmark
5. Profiling and optimization for longer context windows.

### Nice-to-Have Later

- Full benchmark parity with paper-scale runs.
- Distributed/multi-GPU training support.
- Additional memory module architectures and ablation tooling.

## Status

- Current status: early-stage work in progress.
- APIs, architecture details, and results are expected to evolve as implementation matures.

## Crate Metadata (crates.io)

The crate is configured as a Rust library package and includes:

- Package metadata (`description`, `license`, `repository`, `homepage`, `documentation`)
- Crate discoverability metadata (`keywords`, `categories`)
- Rust toolchain requirement (`rust-version`)
- Packaging include list for publish artifacts
- Readme/license wiring for crates.io and docs.rs

## Publish Checklist

Before first release:

1. Update `version` in `Cargo.toml` to your release version.
2. Run:
   - `cargo check`
   - `cargo test`
   - `cargo package`
3. Authenticate once with crates.io:
   - `cargo login`
4. Publish:
   - `cargo publish`

After publishing, users can install with:

```bash
cargo add titans-rs
```
