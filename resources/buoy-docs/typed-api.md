---
title: "uuidkit typed API"
summary: "Source-derived public signatures, properties, parameters, defaults, and return values."
category: "Reference"
order: 21
types: ["UUIDValue"]
dependencies: []
symbols: ["UUIDValue"]
related: ["api.md", "getting-started.md", "index.md"]
---

# uuidkit typed API

Generated from the package source declarations. Platform guards are shown where present; inherited members are documented on the base type. See the [API contracts](api.md) for behavior and limitations.

## UUIDValue

`Public Class UUIDValue`

Immutable UUID value. Parsing validates syntax, not an application-specific version policy.

### Properties

| Name | Type | Read-Only | Shared | Default | Description |
| --- | --- | --- | --- | --- | --- |
| `Text` | `String` | Yes | No | — | — |
| `Version` | `Integer` | Yes | No | — | — |
| `Variant` | `String` | Yes | No | — | — |
| `IsNil` | `Boolean` | Yes | No | — | — |
| `IsMax` | `Boolean` | Yes | No | — | — |

### Constructor

`Public Sub Constructor(text As String)`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `text` | `String` | `ByVal` | Required |

Returns: no value.

### ToBytes

`Public Function ToBytes() As Bytes`

No parameters.

#### Returns

| Type |
| --- |
| `Bytes` |

### Equals

`Public Function Equals(other As UUIDValue) As Boolean`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `other` | `UUIDValue` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `Boolean` |

### Compare

`Public Function Compare(other As UUIDValue) As Integer`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `other` | `UUIDValue` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `Integer` |

## UUIDKit functions

### UUIDFromBytes

`Public Function UUIDFromBytes(data As Bytes) As UUIDValue`

Interpret exactly 16 bytes in RFC network order, not Windows GUID memory order.

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `data` | `Bytes` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `UUIDValue` |

### UUIDFromCompact

`Public Function UUIDFromCompact(text As String) As UUIDValue`

Parse exactly 32 ASCII hex digits without hyphens; retain the strict constructor contract.

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `text` | `String` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `UUIDValue` |

### NilUUID

`Public Function NilUUID() As UUIDValue`

No parameters.

#### Returns

| Type |
| --- |
| `UUIDValue` |

### MaxUUID

`Public Function MaxUUID() As UUIDValue`

No parameters.

#### Returns

| Type |
| --- |
| `UUIDValue` |

### NewUUIDv4

`Public Function NewUUIDv4() As UUIDValue`

Generate UUIDv4 using Buoy Crypto.RandomBytes; entropy failures propagate.

No parameters.

#### Returns

| Type |
| --- |
| `UUIDValue` |
