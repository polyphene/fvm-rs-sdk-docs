---
title: "Considerations"
description: ""
lead: ""
date: 2022-08-04T09:31:05+02:00
lastmod: 2022-08-04T09:31:05+02:00
draft: false
images: []
menu:
docs:
parent: "reference"
weight: 100
toc: true
---

> You can find the initial grant proposal for the high level Rust SDK 1.0 [here](https://github.com/filecoin-project/devgrants/issues/562)

## External considerations

The goal for this SDK was to create a set of tools that would help actors developer to get on building
over the Filecoin network without having to think about overhead code used to comply to the network standard.

In that sense the SDK is meant to be:
- **Simple**: Entry-level Rust developer should be able to use the SDK to produce actors that can be
run in the FVM.
- **Adjustable**: More experienced developer, either in Rust or on IPFS & Filecoin knowledge, should
be able to fine-tune some part of the SDK to fit their needs (e.g.: codec for methods payloads).
- **Modular**: For some use cases only a small amount of utilities will be required while other projects
will need a fully assisted experience. Developer should be able to find utilities for all types of needs
emerging when dealing with actor developments.

## Internal considerations

As of now the FVM and its ecosystem are still evolving, which requires its tooling framework to evolve
at the same pace. This SDK was designed with those considerations in mind. All procedural macros and
modules have been designed to evolve easily with future needs of integration based on community feedbacks
(e.g. new binding style for methods).
