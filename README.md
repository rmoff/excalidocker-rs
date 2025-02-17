# excalidocker-rs
![GitHub release (latest by date)](https://img.shields.io/github/v/release/etolbakov/excalidocker-rs)
![Docker Pulls](https://img.shields.io/docker/pulls/etolbakov/excalidocker?style=plastic)
[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
![Maintenance](https://img.shields.io/badge/maintenance-actively--developed-brightgreen.svg)

Rust-based utility to convert docker-compose.yaml files into [excalidraw](https://excalidraw.com/) files.
![excalidocker](./data/img/excalidocker-colour-edge.png)

Key features
=================
 - Transform your local docker-compose files into excalidraw with just a single `docker run` command. Showcase your infrastructure designs in a visually appealing and engaging format.
 - Convert external docker-compose files into excalidraw by simply providing a Github link. Easy to share and collaborate.
 - Available for installation on both Linux and MacOS platforms (amd64/arm64).
 - Design customization. Tailor your infrastructure diagrams to your specific needs by customizing font, background colours, styles, etc.

Table of contents
=================
<!--ts-->
   * [Motivation](#motivation)
   * [Usage](#usage)
      * [Docker image](#docker-image)
      * [Binaries](#binaries)
      * [Config file](#config-file)
      * [Demo](#demo)
   * [Installation](#installation)
   * [Contributing](#contributing)
   * [Roadmap](#roadmap)
<!--te-->

## Motivation
An idea of writing this utility originates from Robin Moffatt's [tweet](https://twitter.com/rmoff/status/1659214185220423685).
![motivation](./data/img/motivation.png)

## Usage
### Docker image
🐳 `excalidocker` is available as a [docker image](https://hub.docker.com/r/etolbakov/excalidocker/tags).
Convert docker-compose files without hassle. Use as a Github action for documentation, presentations, ADRs what have you.
The sky is the limit. Get the latest image from [docker hub](https://hub.docker.com/r/etolbakov/excalidocker): 
```sh
docker pull etolbakov/excalidocker:latest
```

Convert a local file:
 ```sh
docker run --rm \
-v "$(pwd)/data/compose/:/tmp/" \
-e INPUT_PATH=/tmp/docker-compose.yaml \
etolbakov/excalidocker:latest > produced-by-image.excalidraw
```

Convert an external file:
```sh
docker run --rm \
-v "$(pwd)/data/compose/:/tmp/" \
-e INPUT_PATH=https://github.com/apache/pinot/blob/master/docker/images/pinot/docker-compose.yml \
etolbakov/excalidocker:latest > produced-by-image-remote.excalidraw
```

A produced `excalidraw` file could be opened in [excalidraw](https://excalidraw.com/) and .... hopefully it won't be too scary 👻 😅.

<details>
  <summary>Convert a local file proving a config</summary>
  
  The command below shows how to pass the config file for additional customization

  ```sh
   docker run --rm \ 
   -v "$(pwd)/data/compose/:/tmp/" \
   -v "$(pwd)/excalidocker-config.yaml:/tmp/excalidocker-config.yaml" \
   -e INPUT_PATH=/tmp/docker-compose.yaml \
   -e CONFIG_PATH=/tmp/excalidocker-config.yaml \
   etolbakov/excalidocker:latest > produced-by-image-config-deps.excalidraw
  ```
</details>

More command examples are in the [Makefile](/Makefile).

### Binaries
📚 Download the latest artifact for your platform/architecture from [releases](https://github.com/etolbakov/excalidocker-rs/releases) and ungzip it.

To get the `help` menu use:
```sh
./excalidocker -h
```
The output should be similar to:
```sh
Utility to convert docker-compose into excalidraw

Usage: excalidocker [OPTIONS] --input-path <INPUT_PATH>

Options:
  -i, --input-path <INPUT_PATH>    file path to the docker-compose.yaml
  -s, --skip-dependencies          display connecting lines between services; if `true` then only service without the lines are rendered
  -o, --output-path <OUTPUT_PATH>  file path for the output excalidraw file. By default the file content is sent to console output
  -c, --config-path <CONFIG_PATH>  config file path for the excalidraw. [default: excalidocker-config.yaml]
  -h, --help                       Print help
  -V, --version                    Print version
```
Usage example:
```sh
./excalidocker --input-path /your/path/docker-compose.yaml --output-path /your/path/result.excalidraw
```

> **Warning**
>
> On the first launch the ungzipped artifact I saw the following pop up
> "Mac cannot be opened because it is from an unidentified developer"
> If you are fine with that you can `Control-click` the artifact, then choose `Open` from the shortcut menu.
> Click `Open`. The utility will be saved as an exception to your security settings,
> and you can open it in the future by double-clicking it just as you can any registered app.
>
> ![mac-warning](./data/img/mac-warning.png)

### Config file
🎨 `excalidocker` supports basic customization provided via file, for example [excalidocker-config.yaml](./excalidocker-config.yaml).
At the moment it's possible to customize:
 - font size and type
 - fill type (`hachure`, `cross-hatch`, `solid`) 
 - backgroud colours for services and ports
 - edge type (`sharp`, `round`)
 - enable/disable connections (has the same effect as `--skip-dependencies` cli option)

### Demo
🎥 This is a small demo to see the `excalidocker` in action

![excalidocker-demo](./data/img/excalidocker.gif)

## Installation
To build `excalidocker` locally, please follow these steps:

1. Install Rust and Cargo if you haven't already. Refer to the official Rust documentation for [installation instructions](https://www.rust-lang.org/tools/install):
2. Clone this repository:
```sh
git clone https://github.com/etolbakov/excalidocker-rs.git
```
3. Build the project using Cargo:
```sh
cd excalidocker-rs && cargo build --release
```
There is the `make r` command available in the [Makefile](/Makefile) along with other useful command shortcuts.

## Roadmap
These are the features that I would like to add at some point:
- 📊 visualize more data from a docker-compose file - volumes, network, etc
- 🦀 various code improvements/enhancements. Feel free to review/suggest if anything could be done better!
- 👨‍💻 etc

## Contributing

Contributions are welcome! If you encounter any issues, have suggestions for improvements or would like to [participate](https://github.com/etolbakov/excalidocker-rs/issues) please open an issue or submit a pull request.

## License

This project is licensed under the [MIT License](./LICENSE).
Feel free to customize the text based on your project's specific details, such as repository URLs, installation instructions, and contribution guidelines.
