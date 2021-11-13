# Docker cheat sheet

```
docker images

## run
```
docker run --name [NAME] [IMAGE:TAG]
```

-it option

## commit
``` 
docker commit[OPTIONS] container [REPOSITORY[:TAG]]
```

ex) docker commit web-server web-server-commit


## build
commit function backup or store current container as image
build function creates images based on script

# Reference
