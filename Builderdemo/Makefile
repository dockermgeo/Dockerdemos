META_AUTHOR := mgeo.de
TEAM_NAME="Blubber2"
DOCKER_IMAGE=dockeriscool/demoimage:latest
DOCKER_NAME=logocontainer
LIST_SERVICES="fotoshower_visualizer fotoshower_fotoshowi fotoshower_dockerui"

make ci:
	make build
	make service_update

build:
	docker build -f Dockerfile.alpine -t ${DOCKER_IMAGE} .

hub:
	docker push ${DOCKER_IMAGE}

run:
	docker run -ti --rm -e TEAM_NAME=${TEAM_NAME} --name ${DOCKER_NAME} ${DOCKER_IMAGE}

network_recreate:
	docker network rm proxy
	docker network create --driver overlay proxy

network_create:
	docker network create --driver overlay proxy

service_stop:
	docker service rm ${DOCKER_NAME}

service_reboot:
		docker service rm ${DOCKER_NAME}
		make service

service_update:
	docker service update --force --update-parallelism 2 --update-delay 10s --detach=false ${DOCKER_NAME}

service_create:
	docker service create \
	 --publish ${PULBIC_PORT}:80 \
	 --mode global \
	 --name ${DOCKER_NAME} \
	 --update-delay 10s \
	 --env TEAM_NAME="${TEAM_NAME}" \
	 --label com.meta.copyright.author="${META_AUTHOR}" \
	 ${DOCKER_IMAGE}

service_visualizer: 
	docker service create \
	  --name=viz \
	  --publish=8088:8080/tcp \
	  --constraint=node.role==manager \
	  --mount=type=bind,src=/var/run/docker.sock,dst=/var/run/docker.sock \
	  dockersamples/visualizer

service_dockerui:
        docker service create \
        --name=dockerui  \
	--env=/docker.sock \
        --publish=8099:9000 \
        --constraint=node.role==manager \
        --mount=type=bind,src=/var/run/docker.sock,dst=/var/run/docker.sock \
        abh1nav/dockerui:latest

stack_deploy: network_create
	 docker stack deploy -c docker-compose.yml ${DOCKER_NAME}

stack_redeploy: network_recreate
	 docker stack rm -c docker-compose.yml ${DOCKER_NAME}
	 docker stack deploy -c docker-compose.yml ${DOCKER_NAME}

service_destroy:
	docker service rm ${LIST_SERVICES}

stack_destroy:
	docker stack rm -c docker-compose.yml ${DOCKER_NAME}
	docker network rm proxy

pull:
	docker pull ${DOCKER_IMAGE}

ls:
	docker service ls

node:
	docker service nodes

ps:
	docker service ps ${1}
rm:
	docker service rm ${1}


