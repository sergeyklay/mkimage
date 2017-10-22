NAME = klay/mkimage
TAG = ubuntu-16.04
SHELL = /bin/bash

build: pre-build docker-build post-build

pre-build:

post-build:

docker-build:
	docker build \
		-t $(NAME):$(TAG) \
		--pull \
		--build-arg PHP_VERSION=7.0 \
		. \
		-f Dockerfile.build