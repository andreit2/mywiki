# Install docker on Centos
```
sudo yum remove docker docker-client docker-client-latest docker-common docker-latest docker-latest-logrotate docker-logrotate docker-engine
sudo yum install -y yum-utils
sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
sudo yum install docker-ce docker-ce-cli containerd.io
sudo systemctl start docker
```
```
docker stats
```
Add user to the docker group
```
sudo usermod -aG docker $USER
```
```
docker logs <id container>
docker logs -f <id container>
docker inspect <id container>
docker exec -it <id container> bash
docker stop <id container>
docker rm $(docker ps -aq)
docker build -f Dockerfile2 -t andreit/test:0.1 .
docker tag nginx:stable-alpine nginx:rbm-dkr-07
docker login --username andreit2
docker push andreit2/otus:tagname
```
