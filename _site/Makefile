# Set $ROOT to top-level directory of the repository
ROOT ?= $(shell dirname $(realpath $(firstword $(MAKEFILE_LIST))))

IMG_NAME=wedocoweb
IMG_HOME=/home

build-env:
	docker build -f ${ROOT}/Dockerfile \
	--platform=linux/amd64 \
	--progress=plain --rm -t ${IMG_NAME} .

build-env-no-cache:
	docker build -f ${ROOT}/Dockerfile \
	--platform=linux/amd64 \
	--no-cache \
	--progress=plain --rm -t ${IMG_NAME} .

COMMAND_RUN=docker run \
		--name ${IMG_NAME} \
		--platform=linux/amd64 \
		--detach=false \
		--network=host \
		--rm \
		-v ${ROOT}:${IMG_HOME}:rw \
		-w ${IMG_HOME} \
		${IMG_NAME} 

build-web:
	$(COMMAND_RUN) /bin/bash -c "make build_web"

serve-web:
	$(COMMAND_RUN) /bin/bash -c "make serve_web"

build_web:
	bundle exec jekyll build

serve_web:
	bundle exec jekyll serve