# Docker

## best practices

- use lightweight images (like Alpine)
- install only required software
- never install SSH (there are other ways to access docker container)
- create and use non-root user
- config small


## workflow
use jenking to build code 
scan docker container & fail build if scanner fails (clairctl)

## ressources

[try docker online](https://labs.play-with-docker.com/)
[docker container name](https://github.com/opencontainers/image-spec)
[security issue scanner with fancy HTML report](github.com/coreos/clair)
[docker bench security which suggest how to improve configuration](https://github.com/docker/docker-bench-security)
[more resources](https://techbeacon.com/security/10-top-open-source-tools-docker-security)
[OWSAP Best practices](https://github.com/OWASP/Container-Security-Verification-Standard)

https://github.com/opencontainers/image-spec

docker swarm vs kuberneters

## example

```docker
WORKDIR / 
ADD myscript.sh # copies local file into docker container 

CMD ["bin/bash", "echo", "hello world"]

EXPOSE 8080

# create non-root user; ensure this user does not exist in host system! user-ids are incremented;
RUN adduser -S ngix-user
# ensure docer uses the non-root user
USER ngix-user
```


```yml
services:
    service-a:
        image: my-image
        deploy:
            resources:
                limits: #restruct resources
                    memory: 64M
                    cpus: '0.2'
        secrets:
            - mongo_password
        volumes:
            - jenkins_home:/var/jenkins_home # from jenkins config
            - '/var/run/docker.sock:/var/run/docker.sock' # mounts docker sock to run docker within docker. the socker is used to control docker itself (clinet/server model). hence never activate in prod. hence weakest link is CI environment
        ports:
            - "80:8080"
        networks:
            - network-a

    service-b:
        image: other-image
        networks: # assing to different network. if not assigned; lands in default hub and can see all traffic!
            - network-b

secret:
    mongo_passwort:
        file: /opt/docker-secrets/secret.txt # defines the mongo_password secret; secret is placed in docker under /var/run/.... Hence only need to place secert on build server
```

```bash
docer network create --opts encrypted --drive overlay --attachable network-b # to encrypt all communication within network; needs docker swarm
```

sign images and ensure they were not modifed; only signed images are deployed
export DOCKER_CONTENT_TRUST=1
