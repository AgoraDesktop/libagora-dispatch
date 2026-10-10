# Provenance

This repository is an extraction of libdispatch — Apple's Grand Central Dispatch — from the
swift-corelibs-libdispatch project. It supplies the dispatch runtime and the blocks runtime that
`libagora-core` and the rest of Agora's stack build on.

| | |
|---|---|
| Upstream repository | https://github.com/swiftlang/swift-corelibs-libdispatch |
| Upstream revision | `swift-6.4.0-RELEASE` |
| Upstream commit | `024805abec6daa9cdda569fd736b9c7686dfd735` |
| Upstream commit date | 2026-04-30 |
| Extraction | the upstream repository root, placed at this repository's root |
| Extraction date | 2026-10-10 |
| Source changes by Agora | none |

## What was copied

The whole upstream tree at the pinned revision — `src/`, `dispatch/`, `private/`, `os/`, `cmake/`,
`config/`, `resolver/`, `tools/`, `man/`, `tests/`, the Xcode project files, `CMakeLists.txt`,
`INSTALL.md`, `TESTING.md`, `PATCHES`, `LICENSE` — placed at this repository's root.

Dropped: only VCS and CI metadata — `.git/`, `.github/`, `.gitignore`, `.mailmap`, and the empty
`.gitmodules`. Agora supplies its own `.gitignore`.

Upstream's `README.md` is kept as `UPSTREAM-README.md` so this repository can carry its own
`README.md`.

## Licence and attribution

Upstream code is Apache-2.0 with the Runtime Library Exception. `LICENSE` is retained verbatim and
the per-file upstream headers are untouched. Agora's own additions to this repository fall under the
project licence (see the top-level project README).

## Keeping in sync

Updates re-extract from a newer upstream revision and record it in the table above. Because the tree
sits at the repository root, `git diff` against a fresh upstream checkout shows local divergence
directly.
