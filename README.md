# Build Tools

This repository houses the authoritative versions of shared build
infrastructure files.

## Common Makefile for Go projects

[`Makefile.COMMON`](Makefile.COMMON) provides common Makefile infrastructure
for several Prometheus components. This includes make tasks for downloading Go,
setting up a self-contained build environment, fetching Go dependencies,
building binaries, running tests, and doing release management. This file is
intended to be included from a project's Makefile, which needs to define the
following variables, at a minimum:

* VERSION - The current version of the project in question. 
* TARGET  - The desired name of the built binary.

Some of the variables defined in this Makefile are defined conditionally (using
'?'), which allows the project's main Makefile to override any of these
settings, if needed. The including Makefile may define any number of extra
targets that are specific to that project.
