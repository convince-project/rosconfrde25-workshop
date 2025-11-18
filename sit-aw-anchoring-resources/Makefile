IMAGE_NAME:=mmorelli1/sitaw-env-rosconfr25
TAG:=0.1.0

CONTAINER:=sitaw-env-rosconfr25-0.1.0

ROS_WS_VOLUME:=$(shell pwd)/workspace/src
TQL_VOLUME:=$(shell pwd)/workspace/tql
DT_VOLUME:=$(shell pwd)/workspace/dt-simulator

HISTFILE:=$(shell pwd)/.bash_history

USERNAME:=user

UID:=$(shell id -u)
GID:=$(shell id -g)

default: all

all: start-docker

docker_exists=$(shell docker ps -a | grep -x $(CONTAINER))
docker_runs=$(shell docker ps | grep -x $(CONTAINER))

start-docker:
	xhost +local:root
ifeq ($(strip $(docker_exists)),)
	@echo "Create and start docker"
	docker run -it --rm -e UID=$(UID) -e GID=$(GID) --net=host --ipc=host --name $(CONTAINER) -v $(ROS_WS_VOLUME):/home/$(USERNAME)/sit-aw-anchoring/humble/src -v $(TQL_VOLUME):/tmp/tql -v $(DT_VOLUME):/tmp/dt -v $(HISTFILE):/home/$(USERNAME)/.bash_history -v /tmp/.X11-unix:/tmp/.X11-unix -v /dev/dri:/dev/dri -e DISPLAY=$(DISPLAY) $(IMAGE_NAME):$(TAG) /bin/bash
else ifeq ($(strip $(docker_runs)),)
	@echo "Restart docker"
	@docker start $(CONTAINER)
	@docker attach $(CONTAINER)
endif

stop-docker:
	docker stop $(CONTAINER)

clear-docker:
	docker rm $(CONTAINER)

join-docker:
	docker exec -u $(UID):$(GID) -it $(CONTAINER) /bin/bash

.PHONY: default all start-docker stop-docker join-docker
