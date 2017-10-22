NAME = klay/mkimage
TAG = ubuntu-16.04
PHP_VERSION = 7.0
FQIN = $(NAME):$(TAG)-php-$(PHP_VERSION)
SHELL = /bin/bash

build: pre-build docker-build post-build

pre-build:

post-build: clean

docker-build:
	docker build \
		-t $(FQIN) \
		--pull \
		--build-arg PHP_VERSION=$(PHP_VERSION) \
		. \
		-f Dockerfile.build

release: build push

push: do-push post-push

do-push:
	docker push $(FQIN)

post-push:

clean:

.PHONY: build pre-build post-build docker-build release push do-push post-push clean

# vim:ft=make:noet:ci:pi:sts=0:sw=4:ts=4:tw=78:fenc=utf-8:et
