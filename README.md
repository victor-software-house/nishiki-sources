# nishiki-sources

Pinned test inputs for [nishiki](https://crates.io/crates/nishiki), a syntax highlighting engine in Rust.

nishiki checks its output against Shiki on third-party source files, each pinned to a commit.  
This repository keeps a copy of each file, so a deleted or rewritten upstream repository cannot break those checks.  
nishiki's scripts read the files from here and never from upstream.

## Licences

Each file stays under its own licence.  
Nothing here is relicensed, and this repository has no licence of its own.

- [`manifest.toml`](manifest.toml) gives each file's licence as an SPDX expression.  
  It also gives `licence_sources`: the files at the pinned commit that state the licence.
- Those licence texts, and each Apache-2.0 repository's `NOTICE` file, are mirrored beside the files they cover.
- A file whose own notice reserves all rights is left out, even when its repository has an open licence.

## Layout

Each file sits at its raw GitHub URL's path, without the host:

```text
<owner>/<repo>/<commit>/<path>
```

For example, `https://raw.githubusercontent.com/psf/requests/<commit>/src/requests/api.py` is at `psf/requests/<commit>/src/requests/api.py`.

`manifest.toml` has one row per file:

| Field | Holds |
|:--|:--|
| `path` | the file's path here |
| `source` | the raw URL it was fetched from |
| `commit` | the upstream commit |
| `purpose` | `input`, a file nishiki reads, or `licence text`, a licence or notice an input names |
| `licence` | an input's licence, as an SPDX expression |
| `licence_sources` | the upstream files that state an input's licence |
| `bytes`, `sha256` | the file's size and SHA-256 |

## Filling and checking

nishiki's `oracle/sources.ts` fills this repository and checks it.  
`fill` fetches each pinned file the mirror lacks, byte for byte, and never rewrites a file already here.  
`check` fails when a pinned file is missing, or when a file differs from its row or has no row.  
nishiki's CI checks out one commit of this repository, pinned in its workflow.
