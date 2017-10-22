META_AUTHOR := mgeo.de
DOCKER_NAME=fotoshower
DOCKER_IMAGE=dockermgeo/fotos_dockerconeu17:latest
PULBIC_PORT=8081
HTML_TITLE="Blubber"
LIST_SERVICES="fotoshower_visualizer fotoshower_fotoshowi fotoshower_dockerui"
VAR_1=$1


make ci:
	make build
	make service_update

build:
	docker build -t ${DOCKER_IMAGE} -f Dockerfile.nginx .

hub:
	docker push ${DOCKER_IMAGE}

run:
	docker run -ti --rm -e HTML_TITLE=${HTML_TITLE} -p ${PULBIC_PORT}:80 --name ${DOCKER_NAME} ${DOCKER_IMAGE}

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
	docker service update --force --update-parallelism 2 --update-delay 20s --detach=false ${DOCKER_NAME}

service_create:
	docker service create \
	 --publish=${PULBIC_PORT}:80 \
	 --mode=global \
	 --name=${DOCKER_NAME} \
	 --update-delay 10s \
	 --env HTML_TITLE="${HTML_TITLE}" \
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
	--publish=8099:9000 \
	--constraint=node.role==manager \
	--env=/docker.sock \
	--mount=type=bind,src=/var/run/docker.sock,dst=/var/run/docker.sock \
	abh1nav/dockerui:latest 

service_destroy:
	docker service rm ${LIST_SERVICES}

stack_deploy: network_create
	 docker stack deploy -c docker-compose.yml ${DOCKER_NAME}

stack_redeploy: stack_destory
	 docker stack deploy -c docker-compose.yml ${DOCKER_NAME}

stack_destroy:
	docker stack rm -c docker-compose.yml ${DOCKER_NAME}
	docker network rm proxy

pull:
	docker pull ${DOCKER_IMAGE}

ls:
	docker service ls

logs:
	docker service logs $((echo ${VAR_1}))

ps:
	docker service ps ${VAR_1}

rm:
	docker service rm ${VAR_1}
