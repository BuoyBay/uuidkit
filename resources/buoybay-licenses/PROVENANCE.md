# Source investigation and scope

UUIDKit is new Buoy code. No implementation text, source files or assets from
the following repositories were copied. Their UUID features motivated the scope:

| Source | Inspected revision | UUID source |
| --- | --- | --- |
| [declaresub/uuid](https://github.com/declaresub/uuid) | `aee5860d4ef98096d4ce282ea3265d0dcf9fab03` | `files/UUID.xml`, `project/UUID.rbbas` |
| [declaresub/mojo](https://github.com/declaresub/mojo) | `6a4a741c3165b12db2ad217ccbf03e4000187dbe` | `mojo/UUID.xojo_code` |
| [declaresub/REALbasicStandardLibrary](https://github.com/declaresub/REALbasicStandardLibrary) | `d450286dd7807150ab27c45f283125bc197f8f16` | `REALbasicStandardLibrary/UUID.rbbas` |

No root license file or explicit license in the inspected UUID source was found.
The independent implementation avoids copying those sources. The Mojo class
uses platform `uuid_generate`/`uuid_compare`/`uuid_unparse` and Windows RPC calls,
and supports null values and operator conversion/comparison. The earlier UUID
repository also exposes v1/v4 generation. UUIDKit instead uses explicit methods,
portable text/network-byte conversion and Buoy's documented cryptographic entropy.

The format, variant/version bits and v4 generation procedure follow the public
specification [RFC 9562](https://www.rfc-editor.org/rfc/rfc9562.html), particularly
sections 4, 5.4, 5.9 and 5.10. Standard UUIDv1, UUIDv4 and UUIDv7 values are used
as interoperability fixtures, not as copied implementation code.

Buoy 0.72.0 installed documentation was searched for UUID support; no public UUID
API was found. Existing `Bytes.FromHex`/`ToHex` provide byte encoding and
`Crypto.RandomBytes` supplies documented secure randomness. This package adds
strict UUID layout, immutable value ownership and field interpretation around
those existing facilities rather than binding libuuid separately on each target.

Unimplemented upstream features: UUIDv1 generation, implicit string conversion,
comparison operators, platform GUID structures and libuuid-specific behavior.
No broader Mojo or REALbasicStandardLibrary compatibility is claimed.
