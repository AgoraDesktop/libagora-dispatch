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
| Agora changes | none yet — see [`PROVENANCE.md`](PROVENANCE.md) |

The full record is in [`PROVENANCE.md`](PROVENANCE.md).

## Licence

Apache-2.0 with the Runtime Library Exception — permissive, and compatible with Agora's
permissive-only policy. See [`LICENSE`](LICENSE).

## Build

Upstream's CMake build is kept (`project(dispatch LANGUAGES C CXX)`, building `dispatch` from
`src/`). It is not yet wired into Agora's standalone build. Upstream's Swift overlay (`src/swift/`,
gated by the `ENABLE_SWIFT` option) is off by default and is not used by Agora.
