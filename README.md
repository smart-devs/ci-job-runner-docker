# CI job runner Docker

This Repo contains the build instructions for the ci docker job runner. it contains secrets to push and pull images from/to registries.

## Documentation

### How to use this image

This image can be used for following pipeline stages:

- docker container build
- docker container release 

### Environment vars

| Argument                              | Default Value                                             | Description |
| :---                                  | :---                                                      | :---         |
| DOCKER_HOST                           | tcp://localhost:2375                                      | Path to docker host or unix socket    |

### Build Arguments

All build arguments should be prefixed with DOCKER_BUILD_ARG. They can be set as pipeline Variable / Job variable. 

note: `DOCKER_BUILD_ARG_` prefix should prepend to all shown variables.

| Argument                              | Default Value                                             | Description |
| :---                                  | :---                                                      | :---         |
| FROM                                  | debian:stretch-slim                                       | Base image to build from    |
| CONTAINER_RUNTIME_REQUIREMENTS        | *empty                                                    | Packages for container during runtime  |
| CONTAINER_BUILD_REQUIREMENTS          | curl gnupg apt-transport-https software-properties-common | Packages for container required during build  |
| CONTAINER_EXTRA_RUNTIME_REQUIREMENTS  | *empty                                                    | extra runtime requirements to keep merge / rebase possible  |
| CONTAINER_EXTRA_BUILD_REQUIREMENTS    | *empty                                                    | extra build requirements to keep merge / rebase possible  |
| DOCKER_VERSION                        | 18.06.1~ce~3-0~debian                                     | Docker version to install  |
| DOCKER_AUTH_CONFIG                    | {}                                                        | Docker `config.json` as string. Value will be written to `~/.docker/config.json`  |

## Contributing

See [CONTRIBUTING.md](./docs/CONTRIBUTING.md).

## Changelog
