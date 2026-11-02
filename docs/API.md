# UUIDKit 0.1.0

Strict UUID conversion and cryptographically random UUIDv4 generation for Buoy.
`Import uuidkit` exposes `UUIDValue`, `UUIDFromBytes`, `UUIDFromCompact`, `NilUUID`, `MaxUUID` and
`NewUUIDv4`. The package uses Buoy's bundled `crypto` package for secure entropy;
it does not use `Random`, timestamps or a MAC address to generate identifiers.
Install a toolchain with `crypto-1.0.0.buipkg` available, or provide that package
in the consumer's package search path. This dependency is supplied by Buoy rather
than downloaded by this package's BPM manifest.

## API

| API | Behavior |
| --- | --- |
| `New UUIDValue(text)` | Accept exactly 36 ASCII characters in the `8-4-4-4-12` hex/hyphen layout; accepts mixed hex case and canonicalizes to lowercase |
| `Text` | Read-only canonical text |
| `ToBytes()` | Fresh 16-byte buffer in RFC network order |
| `UUIDFromBytes(data)` | Require exactly 16 bytes and retain no caller-owned buffer |
| `UUIDFromCompact(text)` | Accept exactly 32 ASCII hex digits without hyphens, in either case; return a canonical UUIDValue |
| `Version` | Raw version nibble, `0..15` |
| `Variant` | `NCS`, `RFC`, `Microsoft` or `Future`, according to the leading bits of byte 8 |
| `IsNil`, `IsMax` | Identify the all-zero/all-one special UUIDs |
| `Equals(other)` | Value equality; a Nil object reference compares false |
| `Compare(other)` | Ordinal canonical-text ordering, equivalent to unsigned network-byte order; Nil throws |
| `NilUUID()`, `MaxUUID()` | New immutable special values |
| `NewUUIDv4()` | 16 bytes from `Crypto.RandomBytes`, with version and variant bits set |

Malformed text, missing bytes, incorrect byte counts and Nil ordering arguments
throw `InvalidArgumentException`. Entropy-provider failures propagate. Values are
immutable and byte buffers are copied on both input and output boundaries.

The parser validates syntax without imposing a UUID version policy. It accepts
all 128-bit patterns, including legacy/reserved variants and nil/max identifiers.
Callers requiring RFC-variant UUIDv4 must additionally check `Variant = "RFC"`
and `Version = 4`; nil/max special values have raw nibbles rather than conventional
generated versions. The constructor rejects URNs, braces, compact hex and surrounding
whitespace. Use `UUIDFromCompact` explicitly for compact hex; that parser rejects
hyphens, URNs, braces, whitespace and non-ASCII digits. Windows GUID in-memory little-endian field layouts are not
accepted as a special representation: convert those fields to network order first.

This is an independent implementation informed by declaresub's UUID-related
projects and [RFC 9562](https://www.rfc-editor.org/rfc/rfc9562.html). It does not
generate UUIDv1/v3/v5/v6/v7/v8, implement implicit conversions/operator overloads,
or promise collision-free output. See [provenance and parity](../PROVENANCE.md).

## Use and verify

The [console example](../examples/declaresub/uuid/main.bui) prints a parsed value and a fresh UUIDv4. Seal this source directory with `/usr/bin/buoy pkg seal`
on the development host; the `buoy` wrapper is for compilation.
