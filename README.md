# libagora-dispatch

**libdispatch for Agora** — the Grand Central Dispatch runtime and the blocks runtime for Agora's
stack: queues, `dispatch_once`, sources, semaphores, and the `Block` runtime that Objective-C blocks
need.

`libagora-core` (Core Foundation) depends on it — `CFRunLoop` is wired into libdispatch's runloop,
and much of Core Foundation uses `dispatch_once`, queues and `dispatch_source`. Agora's Foundation,
window server and applications build on it in turn.

Agora is an installable desktop environment for Linux and BSD; see the project README in the parent
directory (`../README.md`).

## Provenance

Extracted from Apple's
[swift-corelibs-libdispatch](https://github.com/swiftlang/swift-corelibs-libdispatch) — the
cross-platform libdispatch used by Swift on Linux and Windows.

| | |
|---|---|
| Upstream | https://github.com/swiftlang/swift-corelibs-libdispatch |
| Revision | `swift-6.4.0-RELEASE` (`024805abec6daa9cdda569fd736b9c7686dfd735`, 2026-04-30) |
| Agora changes | Swift overlay and build integration removed; artifact renamed — see [`PROVENANCE.md`](PROVENANCE.md) |

The full record is in [`PROVENANCE.md`](PROVENANCE.md).

## Licence

Apache-2.0 with the Runtime Library Exception — permissive, and compatible with Agora's
permissive-only policy. See [`LICENSE`](LICENSE).

## Build

Build into `build/`:

```sh
cmake -S . -B build -DCMAKE_C_COMPILER=clang -DCMAKE_CXX_COMPILER=clang++
cmake --build build
```

Upstream's CMake build is kept (`project(dispatch LANGUAGES C CXX)`, building `dispatch` from
`src/`). Upstream's Swift overlay and its `ENABLE_SWIFT` build integration have been removed, and the
library is built as **`libagora-dispatch`** (`libagora-dispatch.a` when static, `libagora-dispatch.so`
when shared; see [`PROVENANCE.md`](PROVENANCE.md)). The build needs only a C and C++ compiler.

### Install

```sh
cmake --install build --prefix <prefix>
```

The build installs a CMake package, so a consumer uses `find_package(dispatch CONFIG)` with
`-DCMAKE_PREFIX_PATH=<prefix>` — including `libagora-core`.
