DOCKER_NAME=python3-notebook

build:
	docker build -t ${DOCKER_NAME} .

run:
	docker run -it --name ${DOCKER_NAME} -p 8022:22 --rm -v /db/github/ansible_tutorial/container/src:/home/jovyan/node/src ${DOCKER_NAME}

start:
	docker start -i ${DOCKER_NAME}

rm:
	docker rm ${DOCKER_NAME}

update:rm build

