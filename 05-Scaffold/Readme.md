# Skaffold
* skaffold init
* skaffold init --compose-file docker-compose.yml
* skaffold init --compose-file docker-compose.yml -f skaffold-test.yml
* skaffold init -k .k8s/*.yml


Define build artifacts
```
skaffold init --compose-file docker-compose.yml \
        -a '{"builder": "Docker", "payload": { "path" : "Dockerfile"}, "image": "skaffold-example"}'
```

A local build will update dist and sync it to the container
```
    sync:
        manual:
        - src: "./dist"
          dest: "/usr/share/nginx/html"
    docker:
        dockerfile: "nginx.dev.dockerfile"
```

#### Build and deploy using Skaffold
* skaffold dev
* skaffold run

Real use-case: http://github.com/DanWahlin/Angular-Jumpstart

#### Other tools
* Draft: https://draft.sh
* Tilt: https://tilt.dev
* Garden: https://garden.io