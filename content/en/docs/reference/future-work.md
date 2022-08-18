---
title: "Future Work"
description: ""
lead: ""
date: 2022-08-04T09:31:05+02:00
lastmod: 2022-08-04T09:31:05+02:00
draft: false
images: []
menu:
docs:
parent: "reference"
weight: 400
toc: true
---

> If you have any ideas for iterations that you can not find in the list down below please feel free
> to open an issue on the [repository](https://github.com/polyphene/fvm-rs-sdk).

## _fvm_actor_

- Developers should be able to develop their own invoke function without using `#[fvm_actor]` and still
feel as less overhead as possible. Different design should be studied (macros for code  generation of
serde/dispatch/etc., code injection at dedicated places in the generated invoke ...) and one implemented.

## _fvm_export_

- Support the ["Calling convention with hashed method name"](https://github.com/filecoin-project/FIPs/blob/master/FRCs/frc-0042.md) for exported methods.

## Examples

- The current fungible token example is not adequate for production usage and is mostly coming from
Helix team's work on their [Filecoin library](https://github.com/helix-onchain/filecoin). When the library
is live on crates.io we should switch to an example importing it and implementing it.

## Optimization

- This SDK should be tested and benchmark to try and find optimization to reduce Wasm bytecode size and
gas cost when running a method exposed.
