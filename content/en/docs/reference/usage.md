---
title: "Usage"
description: ""
lead: ""
date: 2022-08-04T09:30:30+02:00
lastmod: 2022-08-04T09:30:30+02:00
draft: false
images: []
menu:
  docs:
    parent: "reference"
weight: 100
toc: true
---

## Limitations

As of now some references to `ref-fvm` are done through [cargo patches](https://doc.rust-lang.org/cargo/reference/overriding-dependencies.html)
to ease the development of the SDK. This reference makes the SDK harder to use and to test through integration in a
Filecoin Virtual Machine. However, the final version will be simply a line in your dependencies so please bear with us
until then!

## Pre-requirements

Before using the SDK, clone this repository on your local machine and make sure to initialize and update the `ref-fvm`
submodule.

```bash
git submodule init
git submodule update
```

## Build an actor using the SDK

To build an actor using the SDK you can follow the example of the `sdk_example_actor` crate in `./examples/sdk-example-actor`.
Once your actor's crate is ready just run:

```bash
cargo build
```

Using `wasm-builder` in your `build.rs` file will compile the crate in a wasm file that can be found at the path
`./examples/<crate-folder>/target/debug/wbuild/<crate-name>/<crate-name>.compact.wasm`.

## Test your actor

You can test your actor by either integrate it in the `fvm_integration_tests` crate in `ref-fvm` or by running your actor
on a local lotus network.

### Integration test framework

Create a new test in the `fvm_integration_tests` crate and use the path of the compiled wasm file to retrieve its binary content.
You will then be able to interact with it. An example of such tests can be found in `<ref-fvm-repository>/testing/integation/tests`.

### Lotus local network

1. Set up a Lotus devnet on the branch `experimental/fvm-m2`. Instructions can be found
   [in the documentation](https://lotus.filecoin.io/developers/local-network/).
2. Install the actor on the lotus devnet, `lotus chain install-actor <path-to-wasm-bytecode>`. This command should return
   the CID representing the bytecode of the actor.
3. Instantiate the actor, `lotus chain create-actor <code-cid> <encoded-params>`. This command should return the address
   at which the actor is instantiated.
4. Invoke any function from your actor, `lotus chain invoke <address> <method-num>`
