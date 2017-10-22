# `mkimage`

Docker images to use in multi-stage builds.

## Usage

### PHP 7.0 + Ubunti 16.04

```sh
docker create --name extract klay/mkimage:ubuntu-16.04-php-7.0
docker cp extract:/artifacts ./artifacts
docker rm -f extract
```

Dockerfile:

```Dockerfile
COPY artifacts .
```

## Artifacts

```
/artifacts
|-- etc
|   `-- php
|       `-- 7.0
|           `-- mods-available
|               |-- aerospike.ini
|               |-- handlersocketi.ini
|               |-- phalcon.ini
|               |-- pinba.ini
|               |-- weakref.ini
|               `-- zephir_parser.ini
`-- usr
    |-- lib
    |   `-- php
    |       `-- 20151012
    |           |-- aerospike.so
    |           |-- handlersocketi.so
    |           |-- phalcon.so
    |           |-- pinba.so
    |           |-- weakref.so
    |           `-- zephir_parser.so
    `-- local
        |-- bin
        `-- lib
```
