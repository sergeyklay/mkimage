SHELL         ?= /bin/sh
ARGS           = $(filter-out $@,$(MAKECMDGOALS))
PHP_VERSION   ?= 7.0
BUILD_ID      ?= $(shell /bin/date "+%Y%m%d-%H%M%S")
IMAGE_NAME     = klay/mkimage
IMAGE_BASE_TAG = ubuntu-16.04

.SILENT: ;               # no need for @
.ONESHELL: ;             # recipes execute in same shell
.NOTPARALLEL: ;          # wait for this target to finish
.EXPORT_ALL_VARIABLES: ; # send all vars to shell
Makefile: ;              # skip prerequisite discovery

# Public targets

.PHONY: build
build: pre-build docker-build post-build

.PHONY: pre-build
pre-build: check

.PHONY: post-build
post-build: clean

.PHONY: check
check:
ifeq ($(PHP_VERSION),)
	$(error The PHP_VERSION variable not defined: $(PHP_VERSION))
endif

.PHONY: docker-build
docker-build:
	docker build \
		-t $(IMAGE_NAME):$(IMAGE_BASE_TAG)-php-$(PHP_VERSION) \
		--label build_id=$(BUILD_ID) \
		--pull \
		--build-arg PHP_VERSION=$(PHP_VERSION) \
		. \
		-f Dockerfile.build

.PHONY: release
release: build push

.PHONY: push
push: do-push post-push

.PHONY: do-push
do-push:
	docker push $(IMAGE_NAME):$(IMAGE_BASE_TAG)-php-$(PHP_VERSION)

.PHONY: post-push
post-push:

.PHONY: clean
clean:

.SECONDARY: clean

%:
	@:
# vim:ft=make:noet:ci:pi:sts=0:sw=4:ts=4:tw=78:fenc=utf-8:et
