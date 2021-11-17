# Docker cheat sheet


docker images

## images, ps


## run
```
$ docker run --name [NAME] [IMAGE:TAG]
```

example
``` 
$ docker run --name web-server -it ubuntu:20.04
```

-it option

## commit
``` 
docker commit [OPTIONS] container [REPOSITORY[:TAG]]
```

example
```
docker commit web-server web-server-commit
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

```
```

**FROM** : base image   
**RUN** : run command when docker container is created. Make new image (빌드가 실행될 때 실행됨, 이미지에 반영됨)
**WORKDIR** : maker directory and move to the directory and command is executed on the directory     
                if run "RUN echo "Hello, \<strong> Docker \</strong>" index.html" after the "WORKDIR PATH"   
                the PATH/index.html id created   
**COPY** : copy files from the host to a docker working directory   
**CMD** : run command (컨테이너가 실행될 때 실행됨, 컨테이너에 
```
FROM ubuntu:20.04
RUN apt update && apt install -y python3
WORKDIR /var/www/html 
COPY ["index.html", "."]
CMD ["python3", "-u", "-m", "http.server"]
```

# Reference
