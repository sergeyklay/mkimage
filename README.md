# `mkimage`

Docker images to use in multi-stage builds.

Avaliable PHP versions:

* PHP 7.0
* PHP 7.1
* PHP 7.2

Note: Phalcon support for PHP 7.2 is experemental. Do not use it at production.

## Usage

### Ubunti 16.04

#### Getting Artifacts

```sh
# Use PHP_VERSION=7.0, PHP_VERSION=7.1 or PHP_VERSION=7.2
docker create --name extract klay/mkimage:ubuntu-16.04-php-${PHP_VERSION}
docker cp extract:/artifacts ./artifacts
docker rm -f extract
```

#### Dockerfile

```Dockerfile
# ...

ENV PHP_VERSION=7.0

COPY artifacts .

RUN cp -R /artifacts/etc/php/$PHP_VERSION/mods-available /etc/php/$PHP_VERSION/mods-available \
    && cp -R /artifacts/usr/lib/php/`php-config --phpapi` /usr/lib/php/`php-config --phpapi` \
    && FILES=/artifacts/etc/php/$PHP_VERSION/mods-available/* && for f in $FILES; \
        do \
            phpenmod -v $PHP_VERSION -s ALL `basename $f | cut -d '.' -f 1`; \
        done \
    && php -m \
    && rm -rf /artifacts

# ...
```

#### Artifacts

##### PHP 7.0

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

##### PHP 7.1

```
/artifacts
|-- etc
|   `-- php
|       `-- 7.1
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
    |       `-- 20160303
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

##### PHP 7.2

```
/artifacts
|-- etc
|   `-- php
|       `-- 7.2
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
    |       `-- 20170718
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

## Build your own build-image

```sh
# Use PHP_VERSION=7.0, PHP_VERSION=7.1 or PHP_VERSION=7.2
make build PHP_VERSION=7.0
```

## Verify build-image

```sh
# Use PHP_VERSION=7.0, PHP_VERSION=7.1 or PHP_VERSION=7.2
docker inspect klay/mkimage:ubuntu-16.04-php-${PHP_VERSION} | grep build_id
```
