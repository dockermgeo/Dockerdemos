
IMAGE=dockeriscool/demoimage:latest
TEAM_NAME="Blubber"


build:
	docker build -f Dockerfile.alpine -t ${IMAGE} .

run:
	docker run -ti -e TEAM_NAME=${TEAM_NAME} --rm ${IMAGE}
