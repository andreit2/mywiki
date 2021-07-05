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
```
FROM alpine:3.12
RUN apk update && apk upgrade
RUN wget https://releases.hashicorp.com/terraform/0.12.28/terraform_0.12.28_linux_amd64.zip 
RUN unzip terraform_0.12.28_linux_amd64.zip 
RUN rm terraform_0.12.28_linux_amd64.zip 
RUN mv terraform /usr/local/bin/
RUN wget https://github.com/terraform-linters/tflint/releases/download/v0.16.2/tflint_linux_amd64.zip 
RUN unzip tflint_linux_amd64.zip 
RUN rm tflint_linux_amd64.zip
RUN mv tflint /usr/local/bin/
RUN apk add curl
CMD ["/bin/sh"]
```
```
erfile
FROM alpine:3.12
ARG tf_ver=0.12.28
ARG tflint_ver=0.16.2
RUN apk update && apk upgrade
RUN wget https://releases.hashicorp.com/terraform/${tf_ver}/terraform_${tf_ver}_linux_amd64.zip \
    && unzip terraform_${tf_ver}_linux_amd64.zip && rm terraform_${tf_ver}_linux_amd64.zip \
    && mv terraform /usr/local/bin/
RUN wget https://github.com/terraform-linters/tflint/releases/download/v${tflint_ver}/tflint_linux_amd64.zip \
    && unzip tflint_linux_amd64.zip && rm tflint_linux_amd64.zip \
    && mv tflint /usr/local/bin/
RUN apk add --no-cache curl
CMD ["/bin/sh"]
```
