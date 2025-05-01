# DSC_672_software_pres
# Yaseen Ghani
# Jenkins Tutortial

## Cloning from github
```
Git clone https://github.com/yaseen-ghani/DSC_672_jenkins_demo
```

## Build the Jenkins BlueOcean Docker Image (or pull and use the one I built)
```
docker build -t myjenkins-blueocean:2.492.3-1 .
```

## Create the network 'jenkins'
```
docker network create jenkins
```

### Creating the docker contrainer on Windows 
```
docker run --name jenkins-blueocean--restart=on-failure --detach `--network Jenkins --env DOCKER_HOST=tcp://docker:2376 `--env DOCKER_CERT_PATH=/certs/client --env DOCKER_TLS_VERIFY=1 `--volume jenkins-data:/var/jenkins_home `--volume jenkins-docker-certs:/certs/client:ro `--publish 8080:8080 --publish 50000:50000 myjenkins-blueocean:2.492.3-1
```

## Get the Password
```
docker exec jenkins-blueocean cat /var/jenkins_home/secrets/initialAdminPassword
```

## Connect to the Jenkins
```
https://localhost:8080/
```

## Installation Reference:
https://www.jenkins.io/doc/book/installing/docker/


## alpine/socat container to forward traffic from Jenkins to Docker Desktop on Host Machine

```
docker run -d --restart=always -p 127.0.0.1:2376:2375 --network Jenkins -v /var/run/docker.sock:/var/run/docker.sock alpine/socat tcp-listen:2375,fork,reuseaddr unix-connect:/var/run/docker.sock

docker ps

docker inspect <container_id> | grep IPAddress
```

## Jenkins docker agent
```
jenkins/agent:alpine-jdk17
```
