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

## gh-release

[`gh-release`](gh-release) reads the latest release on GitHub, checks out its
tag and runs a build command (defaults to `make archive`) with `GOOS` / `GOARCH`
combinations defined in the script. After that, it attaches the resulting
tarball to the release.

For authentication a [GitHub Personal Access Token](https://github.com/settings/applications)
is required. This can be provided via the `GITHUB_TOKEN` env variable or written to
`~/.github-token`.

To build a new release, you need to

1. Change to the repo you want to create a release from
2. Bump version in Makefile and commit the changes
3. Run `make tag` to tag and push the current revision
4. Create a [GitHub release](https://help.github.com/articles/creating-releases/)
   for the new tag
5. Run `gh-release [optional-build-command]`
