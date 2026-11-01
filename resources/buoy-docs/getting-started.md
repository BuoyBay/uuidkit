---
title: "UUIDKit getting started"
summary: "Configure and use UUIDKit with explicit input and ownership rules."
category: "Guides"
order: 10
keywords: ["uuid", "identifier", "bytes", "crypto"]
related: ["index.md", "api.md", "typed-api.md"]
---

# UUIDKit getting started

Install uuidkit in packages and make the bundled crypto archive available alongside it or in your toolchain package search path. The example parses a known UUID, round-trips its network-order bytes, then generates one random UUIDv4.

```buoy
Import uuidkit

Sub Main()
    Dim known As New UUIDValue("F81D4FAE-7DEC-11D0-A765-00A0C91E6BF6")
    Dim restored As UUIDValue = UUIDFromBytes(known.ToBytes())
    Print restored.Text
    Print "Round trip: " + String.From(known.Equals(restored))
    Dim generated As UUIDValue = NewUUIDv4()
    Print generated.Text
    Print "Variant: " + generated.Variant
End Sub
```

## Select representations explicitly

Use `UUIDFromCompact(text)` for exactly 32 hexadecimal digits without hyphens.
Both hex cases are accepted and output is canonical lowercase with hyphens.
The constructor still requires the 36-character form. Neither parser trims
whitespace or accepts braces, URNs or non-ASCII hex characters.

Text is canonical lowercase. ToBytes returns a fresh 16-byte network-order buffer; UUIDFromBytes requires exactly 16 bytes and retains no caller-owned buffer. Windows GUID in-memory little-endian fields must be converted into network order before using this API.

Use Equals for value equality, rather than relying on object identity. Compare orders canonical text ordinally, matching unsigned network-byte ordering. Equals accepts a Nil reference as false, while Compare rejects Nil.

## Generation and errors

Entropy-provider failures propagate. Malformed text and invalid/missing byte buffers throw InvalidArgumentException. Generated values have Version 4 and Variant RFC; generation does not promise collision-free output. UUIDv1/v3/v5/v6/v7/v8 generation is not implemented.

## Read next

- [Overview](index.md)
- [Getting started](getting-started.md)
- [API reference](api.md)
