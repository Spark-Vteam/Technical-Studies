# Multi-stages in a docker container

This is a short study of how to have multiple stages within a Docker container.

## Multi-staging

Multi-staging is a relatively new way to optimize Docker images and maintain a small size. It is recommended to use when the application has a build-phase. Multi-stage builds in Docker is when multiple 'FROM' statements are used. Each 'FROM' statement uses a different base image, and begins a new stage of a build. 
Mulit-stage builds thus allows to selectively copy files or folders from one stage from another. This way only needed resources are in the final image.

### Naming build stages

The stages in multi-stage builds are not named by default, Each stage can be named by adding 'AS <NAME>' to the FROM instruction. 
The name is then reused in the COPY instruction, that then reassures that the COPY doesn't break if the instructions are reordered at a later point.

### Stop a specific build stage
Having multiple stages in Dockerfile allows to separately build each stage:

```
docker build --target <stage_name> -t <image_name>
```

Multi-stage builds are used in order to deploy production-ready apps. It works with just one Dockerfile, and allows to build smaller images as it is separated into various stages.

