# microservices
repo for otus devops course
# docker host creation

docker-machine create --driver google \
--google-project docker-181817 \
--google-zone europe-west1-b \
--google-machine-type f1-micro \
--google-machine-image $(gcloud compute images list --filter ubuntu-1604-lts --uri) \
docker-host

---
# open firewall port on GCE for app
gcloud compute firewall-rules create default-puma-server --allow tcp:9292 --source-tags=docker-machine --source-ranges=0.0.0.0/0 --description="puma server port rule"

# change docker-client env to work on remote host

use
docker login
before starting docker containers  on remote host

eval $(docker-machine env docker-host)

# building  container

docker build -t reddit:latest .

# running  container

docker run --name reddit -d --network=host reddit:latest

# push

docker tag reddit:latest <your-login>/otus-reddit:1.0
docker push <your-login>/otus-reddit:1.0
