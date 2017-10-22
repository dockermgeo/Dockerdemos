
TEAM_NAME="Blubber"
DOCKER_IMAGE=dockeriscool/demoimage:latest
DOCKER_NAME=logocontainer


build:
	docker build -f Dockerfile.alpine -t ${DOCKER_IMAGE} .

run:
	docker run -ti -e TEAM_NAME=${TEAM_NAME} --rm ${DOCKER_IMAGE}
service_update:
	docker service update --force --update-parallelism 2 --update-delay 20s --detach=false ${DOCKER_NAME}

service_create:
	docker service create \
	 --name ${DOCKER_NAME} \
	 --replicas 3 \
	 --update-delay 10s \
	 --env TEAM_NAME="${TEAM_NAME}" \
	 ${DOCKER_IMAGE}

service_deploy:
	 docker stack deploy -c docker-compose.yml ${DOCKER_NAME}
