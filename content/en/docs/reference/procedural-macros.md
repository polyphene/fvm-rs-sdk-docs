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
weight: 200
toc: true
---

## _fvm_state_

To import in your actor everything needed by the procedural macro it is recommended to use the whole
`state` module:

```rust
use fvm_rs_sdk::state::*;
```

The macro should be used on a public structure. It will generate an implementation of the `StateObject`
for the state object, allowing for it to be saved and loaded while interacting with the actor.

A simple example of usage would be:
```rust
use fvm_rs_sdk::state::*;

#[fvm_state]
pub struct State {
  pub count: u64
}
```

Blockstore glue code is located in the SDK and can be found under the `state` module of the crate.


### Limitations

- The procedural macro does not work on structure with lifetime or generic parameters to prevent problems around Serialization
  and Deserialization.
- When using the macro on a structure, fields that are not public will not be stored in the state.

## _fvm_actor_

The procedural macro to annotate your actor's interface can be found in the `actor` module:

```rust
use fvm_rs_sdk::actor::fvm_actor;
```

This macro will parse the annotated implementation and generate a proper `invoke()` function that will become the
entry point of your actor. An `#[fvm_actor]` procedural macro should be combined with the usage of the
`#[fvm_export]` macro described in the next section.

A simple usage would be:
```rust
use fvm_rs_sdk::state::*;
use fvm_rs_sdk::actor::fvm_actor;

#[fvm_state]
pub struct State {
  pub count: u64
}

#[fvm_actor]
impl State {
  ...
}
```

### Limitations

- The implementation with `#[fvm_actor]` has to be the implementation of the structure annotated
with `#[fvm_state]`.
- Only one implementation can be annotated with `#[fvm_actor]` as it will otherwise generate
compilation conflicts (multiple `invoke()` functions declared).
- Currently, the only dispatch method handled is `method-num`, using integers to manage the internal
dispatch of the actor.
- Implementation with generics or lifetime are not supported.

## _fvm_export_

The procedural macro to annotate your actor's entry point in the implementation representing your actor's interface. It
can be accessed in the `actor` module:

```rust
use fvm_rs_sdk::actor::fvm_export;
```

This macro will help to generate the glue code inside the `invoke()` entry point by generating all
internal dispatch possibilities.

A simple usage would be:
```rust
use fvm_rs_sdk::state::*;
use fvm_rs_sdk::actor::{fvm_actor, fvm_export};

#[fvm_state]
pub struct State {
  pub count: u64
}

#[fvm_actor]
impl State {
  #[fvm_export(binding=1)]
  fn increment(&mut self) -> u64 {
    self.count += 1;
    self.count
  }
}
```

It has to be noted that we are differentiating pure, read-only and read-write functions by playing
around the reference that a method is associated with. As such:
- No reference: pure function
- `&self`: read-only function
- `&mut self`: read-write function

### Limitations

- When specifying an export it has to be used with the `binding` attribute to specify its internal
dispatch value (e.g.: `#[fvm_export(binding=1)]`).
- Methods with generic types or lifetimes as arguments or return are not supported.

## _fvm_payload_

This procedural macro should be used on custom structures and types that will be used either as
parameters or return types of method exported. It can be found in the `payload` module of the crate.
It is recommended to use the whole module when dealing with the macro:
```rust
use fvm_rs_sdk::payload::*;
```

It will generate necessary code for Serialization and Deserialization of the structures and types. As
serde is working recursively on types within structures, all inner types should also be tagged with
the macro.

A simple usage would be:
```rust
use fvm_rs_sdk::state::*;
use fvm_rs_sdk::actor::{fvm_actor, fvm_export};
use fvm_rs_sdk::payload::fvm_payload

#[fvm_state]
pub struct State {
  pub count: u64
}

#[fvm_payload]
pub struct Payload {
  pub amount: u64
}

#[fvm_actor]
impl State {
  #[fvm_export(binding=1)]
  fn increment(&mut self) -> u64 {
    self.count += 1;
    self.count
  }

  #[fvm_export(binding=2)]
  fn add(&mut self, payload: Payload) -> u64 {
    self.count += payload.amount;
    self.count
  }
}
```
