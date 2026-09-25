# JavaScript Client Generation

[![Kubling license](https://img.shields.io/badge/license-Apache%202.0-blue.svg?style=flat-square)](LICENSE)

> [!IMPORTANT]
> **This repository is archived and no longer maintained.**
>
> Generating JavaScript API clients for injection into Kubling is no longer the
> recommended integration mechanism. Configure the
> [official OpenAPI provider](https://github.com/kubling-community/kubling-providers/tree/main/providers/openapi)
> for OpenAPI-described APIs, or implement a
> [custom provider](https://github.com/kubling-community/kubling-providers)
> when source-specific behavior is required.
>
> This repository remains available for historical reference.

## Historical documentation

The instructions below describe legacy JavaScript client generation and are not the current Kubling integration path.

This repository contains a list of curated and tested, auto-generated API Clients, using [openapi-generator](https://github.com/OpenAPITools/openapi-generator).

It is important to note that `ApiClient` template was modified to use Kubling `httpCli`, the object injected in all JavaScript contexts.
Therefore, you can't use the built-in generator's template for JavaScript since it will not work.

## Node.js based libraries
Most famous JavaScript libraries were meant to be used within a Node.js context. Similar way Kubling engine injects objects in execution
contexts, Node.js has core, built-in libraries (called modules) you can simply import, like `http` and `fs`.

Since they are not available in our engine, most of those libraries can't be used directly and need some adaptation, like teh result of this
template, in which we removed references to the standard `superagent` in favor of the powerful Kubling's `httpCli`.

## Generate API Client sources
Generated sources are not included since, in most cases, the result is a hundred of source files, which does not
make any sense to include as the generation takes usually less than a `git clone`.

To generate a client, you must have `java` installed locally. Please have a look at [this doc](https://openapi-generator.tech/docs/installation#jar)<br>
In case you don't want to use the version added to this repo, please read in that same document how to install the generator locally.

Once everything is configured just run:<br>
```
java -jar openapi-generator-cli-7.6.0.jar generate -i [path/to/spec] -g javascript -o [path/to/client/dir] -t template/
```

Example:
```shell
java -jar openapi-generator-cli-7.6.0.jar generate -i azure/spec/storage.yaml -g javascript -o azure/generated/storage/ -t template/
```