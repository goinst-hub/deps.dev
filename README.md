# deps.dev API

[deps.dev](https://deps.dev/) is a service developed and hosted by Google to
help developers better understand the structure, construction, and security of
open source software packages.

The deps.dev API can be accessed in two ways: as JSON over HTTP, as well as via
[gRPC](https://grpc.io/). This repository contains the service definition for
the gRPC API, along with example applications for both APIs.

## Using the HTTP API

The HTTP API can be accessed using any HTTP client. To quickly get started, you
can use the `curl` command-line tool. Example:

```console
curl 'https://api.deps.dev/v3alpha/systems/npm/packages/%40colors%2Fcolors'
```

Note that the `@` and `/` in the package name have been percent-encoded.

For complete documentation on the HTTP API, please visit
[docs.deps.dev](https://docs.deps.dev/).

## Using the gRPC API

The gRPC API can be accessed using any gRPC client. The service definition,
which describes the methods of the API along with their request and response
messages, can be found in [api/v3alpha/api.proto](./api/v3alpha/api.proto)

To quickly get started exploring the API, you can use the
[`grpcurl`](https://github.com/fullstorydev/grpcurl) command-line tool.
Example:

```console
grpcurl \
  -d '{"package_key":{"system":"NPM","name":"@colors/colors"}}' \
  api.deps.dev:443 \
  deps_dev.v3alpha.Insights/GetPackage
```

## Example applications

Example applications written in Go can be found in the `examples` directory:

- [`artifact_query`](./examples/go/artifact_query) shows how to query the
  deps.dev HTTP API by file content hash.
- [`dependencies_dot`](./examples/go/dependencies_dot) fetches a resolved
  dependency graph from the deps.dev HTTP API and renders it in the DOT
  language used by Graphviz.
- [`package_lock_licenses`](./examples/go/package_lock_licenses) reads
  dependencies from an npm package-lock.json file and fetches their licenses
  from the deps.dev gRPC API.

## Third party tools and integrations

Note that these are community built tools and unsupported by the core deps.dev maintainers.

- [`edoardottt/depsdev`](https://github.com/edoardottt/depsdev) CLI client (and Golang module) for deps.dev API.

## Data

deps.dev aggregates data from a number of sources:

- Package data (including package and version names, descriptions, dependency requirements, etc)
  - [Crates.io](https://crates.io/)
  - [Go Module Mirror, Index, and Checksum Database](https://index.golang.org/)
  - [Maven Central Repository](https://repo.maven.apache.org/maven2/)
  - [Google's Maven Repository](https://maven.google.com/)
  - [Jenkins' Maven Repository](https://repo.jenkins-ci.org/releases/)
  - [npm Registry](https://registry.npmjs.org/)
  - [NuGet](https://www.nuget.org/)
  - [PyPI](https://pypi.org/)
- Project data (including project names, descriptions, forks and stars, etc)
  - [GitHub](https://github.com/)
  - [GitLab](https://gitlab.com/)
  - [Bitbucket](https://bitbucket.org/)
- Security advisories
  - [OSV.dev](https://osv.dev/)
- Associated data
  - [OpenSSF Scorecard](https://github.com/ossf/scorecard)
  - [OSS-Fuzz](https://google.github.io/oss-fuzz/)

For details on using the data from these sources, please consult their
documentation.

As well as aggregating data, deps.dev generates additional data, including
resolved dependencies, advisory statistics, associations between entities, etc.
This generated data is available under a
[CC-BY 4.0](https://creativecommons.org/licenses/by/4.0/) license.

## Terms

Use of the deps.dev API is subject to the
[Google API Terms of Service](https://developers.google.com/terms).

## Contact us

If you have questions about the API, or want to report a problem, please create
an issue or contact us at depsdev@google.com.
