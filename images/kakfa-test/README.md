# Docker

docker build -t kafka-test-image .
docker run --rm --name kafka-test-container -i -t kafka-test-image

docker exec -it kafka-test-container bash

// docker rm kafka-test-container