UI Plugin Server
========

[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)

This repository serves as a base for developing plugins for the Rancher UI.

It contains a [Dockerfile](./package/Dockerfile) that packages the contents of the [`plugin/`](./plugin) directory into a Docker image that serves up the contents of the `plugin/` directory and an auto-generated `files.txt` via a simple [nginx](https://nginx.org) server.

> **Note:** The contents of the `plugin/` directory is expected to be an [npm package](https://docs.npmjs.com/about-packages-and-modules#about-packages), which means that it should contain a file that describes the plugin at `plugin/package.json`.

**This meets the expectations of a UI Plugin Server that can be integrated with Rancher's [UI Plugin Operator](https://github.com/rancher/ui-plugin-operator).** You can build this image by running the `make` command.

It also contains a [Helm chart](https://github.com/helm/helm) that can be used to deploy this image. 

A simple utility script located at [`scripts/patch`](./scripts/patch) that can be run by calling `make patch` allows a user to modify this Helm chart according to the plugin that you seek to build.

## Developing

### How do I create my own Rancher plugin?

To develop your own plugin, you will need to modify the Docker image and Helm chart in this repository.

Please read the [Getting Started guide](./docs/gettingstarted.md) for a more detailed explanation of how to do so!

For an example of how to create a repository that hosts multiple plugins and simply copies over the Helm chart from this repository with some changes on an install, see [`scripts/publish` in `rancher/ui-plugins-example`](https://github.com/rancher/ui-plugin-examples/blob/main/scripts/publish).

## Building

`make`

## Running

`helm upgrade --install --create-namespace -n cattle-ui-plugin-system <your-plugin> ./charts/ui-plugin-server`

## License
Copyright (c) 2022 [Rancher Labs, Inc.](http://rancher.com)

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

[http://www.apache.org/licenses/LICENSE-2.0](http://www.apache.org/licenses/LICENSE-2.0)

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
