---
title: Installation
parent: Documentation
nav_order: 1
---

# Installation
Installation of Open SPM Registry. The server can be run either from source or from a docker image.
{: .fs-6 .fw-300 }

## Docker Image
The docker image is the easiest way to run the server. They can be built from source or pulled from dockerhub.
Its recommended to build the image from source especially if you want to adjust the configuration and keep it versioned on you docker server.
### Prebuilt Image
The prebuilt image is available on [dockerhub](https://hub.docker.com/r/wgr1984/openspmregistry).
```
docker pull wgr1984/openspmregistry:latest
```
### Build docker image
To build the docker image from source we need to clone the repository and build it.
```
> git clone git@github.com:wgr1984/openspmregistry.git
> cd openspmregistry
> make build-docker
```
This will build the docker image with the name `wgr1984/openspmregistry:latest`.

### Run docker image
To run the docker image we need to mount the files and the configuration.

`-v ./files:/app/files ` will mount the files directory to the container.

`-v ./config.local.yml:/app/config.local.yml` will mount the configuration file to the container.
-> [Configuration](#configuration)

same can be done with the certificates if needed.
```
> docker run -p 8080:8080 \
    -v ./files:/app/files \
    -v ./config.local.yml:/app/config.local.yml \
    -i -t wgr1984/openspmregistry:latest
```

## Source
To run the server from source we need to clone the repository and build it.
```
> git clone git@github.com:wgr1984/openspmregistry.git
> cd openspmregistry
> make build
```
### Configuration
Check the configuration by copying 'config.yml' to 'config.local.yml' and adjust it to your needs.
```
> cp config.yml config.local.yml
```
```yaml
# config.local.yml
server:
  hostname: 127.0.0.1
  port: 8080
  certs:
    cert: server.crt
    key: server.key
  repo:
    type: file
    path: ./files/
  publish:
    maxSize: 204800
  auth:
    enabled: false
```
e.g. to enable auth set `enabled: true`, set `type: basic` and add users to `users` array
```yaml
    type: basic
    users:
      - username: admin
        password: admin
```
then we can run it
### Run
```
./openspmregistry -tls=true -v
```

{: .highlight }
ℹ️ `-tls=true` is needed to enable `https`, if you want to use http set it to false (e.g. setup behind nginx proxy)
it will use `server.crt` and `server.key` as certificates.

