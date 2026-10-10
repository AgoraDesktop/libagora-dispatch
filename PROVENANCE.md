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
| Source changes by Agora | Swift overlay and build integration removed; artifact renamed — see *Agora changes* |

## What was copied

The whole upstream tree at the pinned revision — `src/`, `dispatch/`, `private/`, `os/`, `cmake/`,
`config/`, `resolver/`, `tools/`, `man/`, `tests/`, the Xcode project files, `CMakeLists.txt`,
`INSTALL.md`, `TESTING.md`, `PATCHES`, `LICENSE` — placed at this repository's root.

Dropped: only VCS and CI metadata — `.git/`, `.github/`, `.gitignore`, `.mailmap`, and the empty
`.gitmodules`. Agora supplies its own `.gitignore`.

Upstream's `README.md` is kept as `UPSTREAM-README.md` so this repository can carry its own
`README.md`.

## Agora changes

### Swift overlay and build integration removed

Agora does not support Swift, so the Swift overlay and its build integration have been removed:

- **deleted the Swift overlay** — `src/swift/` (the `*.swift` sources, `DispatchStubs.m`,
  `Dispatch.apinotes`, the overlay shims under `src/swift/shims/`, and its `CMakeLists.txt`);
- **deleted** `cmake/modules/SwiftSupport.cmake`;
- **removed** the `ENABLE_SWIFT` option, `enable_language(Swift)`, every `if(ENABLE_SWIFT)` block, the
  `lib/swift`-prefixed install destinations (now ordinary `${CMAKE_INSTALL_LIBDIR}`, `include/dispatch`
  and `include/os`), and the `COMPILE_LANGUAGE:Swift` compile options — across `CMakeLists.txt`,
  `src/CMakeLists.txt`, `dispatch/CMakeLists.txt`, `man/CMakeLists.txt`,
  `src/BlocksRuntime/CMakeLists.txt`, `tests/CMakeLists.txt`, `cmake/config.h.in` and
  `cmake/modules/dispatchConfig.cmake.in`.

The C and C++ sources are otherwise untouched. The `*_SWIFT_*` availability attributes in the headers
(`DISPATCH_SWIFT_UNAVAILABLE`, `OS_SWIFT_UNAVAILABLE`, `DISPATCH_REFINED_FOR_SWIFT`, …) are **kept**:
they are C preprocessor macros that a Swift importer would consume, and they compile to nothing for a
C/C++ build. Nothing in the remaining C/C++ path requires a Swift compiler.

### Artifact naming

The library is built as **`libagora-dispatch`** — `libagora-dispatch.a` when built static,
`libagora-dispatch.so` when shared (`libagora-dispatch.dylib` on Darwin):

```cmake
set_target_properties(dispatch PROPERTIES OUTPUT_NAME agora-dispatch)
```

The CMake target keeps upstream's name, `dispatch`, so `target_link_libraries(... dispatch)` is
unchanged. The `link` autolink directives in `dispatch/generic/module.modulemap` were updated from
`link "dispatch"` to `link "agora-dispatch"` to match. The `BlocksRuntime` library keeps its upstream
name.

## Licence and attribution

Upstream code is Apache-2.0 with the Runtime Library Exception. `LICENSE` is retained verbatim and
the per-file upstream headers are untouched. Agora's own additions to this repository fall under the
project licence (see the top-level project README).

## Keeping in sync

Updates re-extract from a newer upstream revision and record it in the table above. Because the tree
sits at the repository root, `git diff` against a fresh upstream checkout shows local divergence
directly.
