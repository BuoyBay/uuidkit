---
title: "UUIDKit"
summary: "Convert strict immutable UUID values and generate cryptographically random UUIDv4 identifiers."
category: "Overview"
order: 0
keywords: ["uuid", "identifier", "bytes", "crypto"]
related: ["getting-started.md", "api.md", "typed-api.md"]
---

# UUIDKit

UUIDKit supplies strict canonical UUID text, RFC network-byte conversion, field inspection, special nil/max values, and secure UUIDv4 generation. UUID values are immutable, and buffers are copied when entering or leaving the API.

## Parsing and policy

Text must be exactly 36 ASCII characters in the 8-4-4-4-12 layout. Mixed hex case is accepted and canonicalized to lowercase. The parser validates representation, not an application's version policy: all 128-bit patterns and reserved/legacy variants are accepted.

If a caller requires generated RFC-variant v4, check Variant and Version explicitly. Nil/max UUIDs retain their raw bit interpretations. URNs, braces, compact hex, and surrounding whitespace deliberately reject.

## Dependency and provenance

NewUUIDv4 uses the Buoy crypto package's Crypto.RandomBytes, with version and variant bits set explicitly. Make crypto available in the compiler package search path. This independent implementation follows RFC UUID representation and was informed by declaresub's UUID-related projects; it does not copy their code or claim their implicit-conversion/operator APIs.

## Read next

- [Overview](index.md)
- [Getting started](getting-started.md)
- [API reference](api.md)
