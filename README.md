# Parse UUIDs and generate cryptographically random UUIDv4 values

Strict UUID conversion and cryptographically random UUIDv4 generation.
`Import uuidkit` exposes `UUIDValue`, `UUIDFromBytes`, `UUIDFromCompact`, `NilUUID`, `MaxUUID` and
`NewUUIDv4`. The package uses Buoy's bundled `crypto` package for secure entropy;
it does not use `Random`, timestamps or a MAC address to generate identifiers.
Install a toolchain with `crypto-1.0.0.buipkg` available, or provide that package
in the consumer's package search path. This dependency is supplied by Buoy rather
than downloaded by this package's BPM manifest.

## Install

From a Buoy consumer project with BPM installed:

```sh
bpm add uuidkit --git https://github.com/BuoyBay/uuidkit.git --rev refs/heads/main
```basic

BPM records the resolved commit in its lockfile. Keep that lockfile with the
consumer project for reproducible installs.

## Example

```basic
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

## Build from source

With the native `build-packages` driver from [devtools](https://github.com/BuoyBay/devtools)
on your `PATH`, run from this checkout:

```sh
build-packages --root "$PWD" --compile-consumer uuidkit
```

The driver checks source targets and compiles an import consumer. See the
[API guide](docs/API.md) for behavior, limits and any host prerequisites.

## Local Buoy setup

On your own machine, install Buoy and run:

```sh
buoy ai init --both
```

## Contributing

[Contributing](CONTRIBUTING.md) · [License](LICENSE)
