# Build Tools

This repository houses the authoritative versions of shared build
infrastructure files.

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
