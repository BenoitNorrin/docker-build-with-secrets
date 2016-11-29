# Docker build image with secrets

Project example.

## Step 1 : build the builder
See : `Dockerfile.build`

```sh
docker build --build-arg SVN_USER=<user> --build-arg SVN_PASSWORD=<password> --build-arg PROJECT_VERSION=tags/1.0.0/ -t project-builder -f Dockerfile.build .
```
## Step 2 : run the builder to build the final image
See : `Dockerfile.release`

```sh
docker run --rm --privileged -v /var/run/docker.sock:/var/run/docker.sock -ti project-builder
```

## Step 3 : run your image 
```sh
docker run -it -p 80:80 -d project
```


## With docker-compose

Edit `docker-compose-builder.yml` and complete with yours secrets

```sh
docker-compose -f docker-compose-builder.yml up --build
docker-compose -f docker-compose-release.yml up -d
```

