# Docker cheat sheet

## ubuntu install programs
apt update
apt install -y git

## docker images, ps
list images
```
docker images [OPTIONS] [REPOSITORY[:TAG]]
```
list containers
```
docker ps [OPTIONS]
```
## login & logout
```
docker login -u [ID] -p [PASSWORD]
docker logout
```

## pull
**digest** : immutable identifier
```
docker pull [OPTIONS] NAME[:TAG|@DIGEST]
```
 docker pull ubuntu:20.04
 docker pull ubuntu@sha256:82becede498899ec668628e7cb0ad87b6e1c371cb8a1e597d83a47fac21d6af3

## push
```
docker push [OPTIONS] NAME[:TAG]
```

example
```
docker push my-repository/python:1.0
```

## run
```
$ docker run [OPTIONS] IMAGE [COMMAND] [ARG...]
```

example
``` 
$ docker run --name web-server -it ubuntu:20.04
$ docker run -it --name my-ubuntu bash
```

-it option

## commit
``` 
docker commit [OPTIONS] container [REPOSITORY[:TAG]]
```

example
```
docker commit web-server web-server-commit

docker commit my-ubuntu my-repository:ubuntu-git
docker commit my-python my-repository/python3:1.0
```

## build
commit function backup or store current container as image
build function creates images based on script

```
docker build [OPTIONS] PATH | URL | -
```

example)
현재 경로 . 에 있는 docker 파일을 이용해 web-serber-build 이미지 생성
```
docker build -t web-server-build .
docker rm --force web-server
docker run -p 8888:8000 --name webserver web-server-build
```

**FROM** : base image   
**RUN** : run command when docker container is created. Make new image (빌드가 실행될 때 실행됨, 이미지에 반영됨)
**WORKDIR** : maker directory and move to the directory and command is executed on the directory     
                if run "RUN echo "Hello, \<strong> Docker \</strong>" index.html" after the "WORKDIR PATH"   
                the PATH/index.html id created   
**COPY** : copy files from the host to a docker working directory   
**CMD** : run command (컨테이너가 실행될 때 실행됨, 컨테이너에 반영됨). docker run 시에 디폴트로 수행되며 만약 docker run 뒤에 command가 입력되면 무시됨 

```
FROM ubuntu:20.04
RUN apt update && apt install -y python3
WORKDIR /var/www/html 
COPY ["index.html", "."]
CMD ["python3", "-u", "-m", "http.server"]
```

```
docker run -p 8888:8000 --name webserver web-server-build (CMD로 지정된 명령어 실행)
docker run -p 8888:8000 --name webserver web-server-build pwd (CMD 무시하고 pwd 실행, override)
```
## exec
```
docker exec -it mongodb bash
```

## compose


## github container registry
**first you have to get an personal access token**

login
```
export CR_PAT=[YOUR_TOKEN]
docker login ghcr.io -u [USERNAME] --password-stdin
```

make image like below format
```
image name format : ghcr.io/[OWNER]/[IMAGE_NAME]:[TAG]
```

example
```
docker commit my-container ghcr.io/my-git-repository-name/my-container:latest
docker push ghcr.io/my-git-repository-name/my-container:latest
```
# Reference
