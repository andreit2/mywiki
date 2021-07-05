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
```
