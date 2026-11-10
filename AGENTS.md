# nishiki-sources

Pinned third-party files that nishiki's oracle reads.  
Read [README.md](README.md) for what the repository holds and how it is laid out.

## Rules

1. **Filled by script only.**
   - Files and `manifest.toml` change only through `bun run oracle/sources.ts fill <this checkout>`, run from nishiki.
   - No file is edited, renamed or written by hand.
2. **Append only.**
   - A file, once added, is never rewritten: its path names its commit, so its bytes never change.
   - A file leaves only when nishiki no longer pins it, and only with the operator's approval.
   - A pull request merges with a merge commit, never a squash or a rebase.  
     nishiki pins a fill commit by its SHA, which must stay on `main`.
3. **Every file has a row.**  
   `manifest.toml` lists each file with its source, licence, size and SHA-256.  
   `bun run oracle/sources.ts check <this checkout>` fails on a missing file, a changed file or a file with no row.
4. **Redistribution must be allowed.**
   - The repository is public, so it redistributes every file.
   - A file enters only under a licence found at its source that permits redistribution.
   - Its licence texts, and an Apache-2.0 repository's `NOTICE`, are mirrored beside it.
   - A file whose own notice reserves all rights stays out, whatever its repository's licence.  
     nishiki lists such files in `keptOut` in `oracle/sources.ts`.
5. **Nothing is relicensed.**  
   The repository has no licence of its own; each file keeps the one its row names.
6. **One guide file.**  
   `AGENTS.md` is the only guide file; add no `CLAUDE.md`.
7. **Commits.**  
   Conventional Commits, such as `feat: mirror the inputs nishiki added for Haskell`.  
   No AI attribution in commits.
