# WatchTower ECR
A docker image based on [containrrr/watchtower](https://github.com/containrrr/watchtower/) for use with AWS ECR.
Project Repository [vincegh/watchtower-ecr](https://github.com/taufiqpsumarna/watchtower-ecr) Forked from [conveos/watchtower-ecr](https://github.com/conveos/watchtower-ecr)

[![Docker Pulls](https://img.shields.io/docker/pulls/vincegh/watchtower-ecr.svg?style=flat-square)](https://hub.docker.com/r/vincegh/watchtower-ecr/)
[![Docker Stars](https://img.shields.io/docker/stars/vincegh/watchtower-ecr.svg?style=flat-square)](https://hub.docker.com/r/vincegh/watchtower-ecr/)

This repository is update to date with the latest version of docker 29 and with AWS ECR.

Especially if you have this error: 
```
Error response from daemon: client version 1.25 is too old. Minimum supported API version is 1.44, please upgrade your client to a newer version
```

Add a star if you like my project!

## Usage

### Build Docker Image (optional)
Installation based on [Amazon ECR Credential Helper installation from source](https://github.com/awslabs/amazon-ecr-credential-helper?tab=readme-ov-file#from-source) and [containrrr/watchtower](https://github.com/containrrr/watchtower/) docker image

### Docker Run

Run the container with the following command:
```bash
docker run -d \
  --name watchtower \
  -v /var/run/docker.sock:/var/run/docker.sock \
  -e "AWS_ACCESS_KEY_ID=<AWS_ACCESS_KEY_ID>" \
  -e "AWS_SECRET_ACCESS_KEY=<AWS_SECRET_ACCESS_KEY>" \
  -e "AWS_REGION=<AWS_REGION>"
  vincegh/watchtower-ecr:latest --interval 300 --cleanup
```

### Docker Compose
If you prefer, you can use the [docker-compose.yml file](./docker-compose.yml) then update your .env file

```bash
cp .env.example .env
nano .env
docker-compose up -d
```

Both the single `docker run` and `docker-compose` can have the default ```config.json``` overridden to use a different authentication method for ECR. 
Refer to https://github.com/awslabs/amazon-ecr-credential-helper#aws-credentials for more info about it.

What you need to add is a new volume that map an existing ```config.json``` over the default one in [docker-compose.yml file](./docker-compose.yml)
```yaml
...
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
      - /path/to/docker-config.json:/config.json #overide default config.json
...
```