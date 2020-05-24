# Changing Go version

We try to use the latest-greatest Go version in our projects, but in order to provide reproducible builds,
Go version is pinned and changing it is always a manual process.

As a thumb rule, patch versions can be used as soon as they are released,
minor versions should be thoroughly tested before reaching production systems.

General steps to change Go version:

1. Edit `Makefile` (if there is one in the project) and change `GO_VERSION` to the desired version. (`make build` verifies that Go is at least at that version or higher)
1. Edit `.circleci/config.yaml` (if there is one in the project) and change the following to the desired version:
    - `GO_VERSION` environment variable
    - `banzaicloud/golang:<version>` build image
    - `circleci/golang:<version>` build image
1. Edit `.github/workflows/*.yml` workflow files (if there is any in the project) and change `go-version` to the desired version. (In case of libraries this could be a list of versions: add the version to the list, check if removing old versions is necessary.)
1. Edit `Dockerfile` (and every other `Dockerfile.*` files) and change `FROM golang:<version>` to the desired version.
1. Edit `go.mod` and change the `go` directive to the desired version (Only in case of applications!)
