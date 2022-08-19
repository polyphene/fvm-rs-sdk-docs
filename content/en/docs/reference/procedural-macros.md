---
title: "Procedural Macros"
description: ""
lead: ""
date: 2022-08-04T09:31:05+02:00
lastmod: 2022-08-04T09:31:05+02:00
draft: false
images: []
menu:
docs:
parent: "reference"
weight: 300
toc: true
---

## `fvm_state`

To import in your actor everything needed by the procedural macro it is recommended to use the whole `state` module:

```rust
use fvm_rs_sdk::state::*;
```

There are two things to know while using this procedural macro:

- The procedural macro does not work on structure with lifetime or generic parameters to prevent problems around Serialization
  and Deserialization.
- When using the macro on a structure, fields that are not public will not be stored in the state.

## `fvm_actor`

The procedural macro to annotate your actor's interface can be found in the `actor` module:

```rust
use fvm_rs_sdk::actor::fvm_actor;
```

This macro will parse the annotated implementation and generate a proper `invoke()` function that will become the
entry point of your actor.

### Limitations

- The implementation with `#[fvm_actor]` have to be the implementation of the structure with `#[fvm_state]`.
- Only one implementation can be written with `#[fvm_actor]` as it will generate compilation conflicts otherwise (multiple
  `invoke()` functions declared).
- Implementation with generics or lifetime are not supported.

## `fvm_export`

The procedural macro to annotate your actor's entry point in the implementation representing your actor's interface. It
can be accessed in the `actor` module:

```rust
use fvm_rs_sdk::actor::fvm_export;
```

### Limitations

- When specifying an export it has to be used with a valid binding method attribute to specify its internal dispatch value (e.g.: `#[fvm_export(method_num=1)]`).
  Currently the only supported binding method is `method_num`.
- A method annotated with `#[fvm_export]` has to be public.
- Methods with generic types or lifetimes as arguments or return are not supported.
- Only a "few" types are supported. The list can be found [here](https://github.com/polyphene/fvm-rs-sdk-private/blob/feature/invoke-glue-code/macro-support/src/export/convert.rs#L158-L285).

## `fvm_payload`

`#[fvm_payload]` is used to annotate custom structures that will be used either as parameters or return
value for exposed methods. To use the macro it is advised to import the whole `payload` module:

```rust
use fvm_rs_sdk::payload::*;
```

There are two things to know while using this procedural macro:

- The procedural macro does not work on structure with lifetime or generic parameters to prevent problems around Serialization
  and Deserialization.
