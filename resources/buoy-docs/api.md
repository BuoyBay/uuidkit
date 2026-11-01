---
title: "UUIDKit API"
summary: "Public types, functions, validation, and ownership rules for UUIDKit."
category: "Reference"
order: 20
keywords: ["uuid", "identifier", "bytes", "crypto"]
symbols: ["UUIDValue", "UUIDValue.Text", "UUIDValue.ToBytes", "UUIDValue.Version", "UUIDValue.Variant", "UUIDFromBytes", "UUIDFromCompact", "NilUUID", "MaxUUID", "NewUUIDv4"]
related: ["index.md", "getting-started.md", "typed-api.md"]
---

# UUIDKit API

| API | Contract |
| --- | --- |
| UUIDValue(text) | Strict 36-character ASCII UUID constructor; canonical lowercase output. |
| Text, ToBytes() | Read-only canonical text and a fresh 16-byte network-order buffer. |
| Version | Raw high nibble of byte 6, from 0 through 15. |
| Variant | NCS, RFC, Microsoft, or Future from byte 8's leading bits. |
| IsNil, IsMax | Identify the all-zero and all-one special values. |
| Equals(other), Compare(other) | Explicit equality and ordinal ordering; Nil handling differs deliberately. |
| UUIDFromBytes(data) | Exactly 16 bytes; input is copied into immutable canonical text. |
| UUIDFromCompact(text) | Exactly 32 ASCII hexadecimal digits in either case, without hyphens; returns a canonical UUIDValue. |
| NilUUID(), MaxUUID() | New immutable special values. |
| NewUUIDv4() | Cryptographic random bytes with v4 and RFC variant bits. |

## Ownership and error behavior

Changing an input or returned Bytes buffer cannot change an existing UUIDValue. Missing bytes, incorrect lengths, malformed syntax, and Nil comparison ordering arguments throw InvalidArgumentException. An entropy provider that fails or returns no valid 16-byte result causes generation to fail.

There are no implicit String conversions, comparison operator overloads, platform GUID structures, timestamp/MAC generators, or libuuid-specific APIs. UUID values are identifiers, not authentication tokens or a uniqueness proof.

## Read next

- [Overview](index.md)
- [Getting started](getting-started.md)
- [API reference](api.md)


[Full typed API: properties, parameters, defaults, and returns](typed-api.md)
