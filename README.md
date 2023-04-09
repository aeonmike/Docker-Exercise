# Docker-Exercise

# Install Docker

# Create Dockerhub Account

# Create Github Account

# Login to Dockerhub account via Docker CLI


# Pull Images from docker

Here's an example Dockerfile that pulls an image from a private registry:


````
FROM private-registry.example.com/my-image:latest
```

In this example, private-registry.example.com is the hostname of the private registry, my-image is the name of the image, and latest is the tag.

If the private registry requires authentication, you can include the credentials in the FROM instruction:

```
FROM private-registry.example.com/my-image:latest
ARG REGISTRY_USER
ARG REGISTRY_PASSWORD
RUN echo "$REGISTRY_PASSWORD" | docker login --username "$REGISTRY_USER" --password-stdin private-registry.example.com
````

In this example, the ARG instructions define variables that can be passed to the docker build command using the --build-arg option. The RUN instruction logs in to the private registry using the provided credentials.

To build the image, you can run:

```
docker build --build-arg REGISTRY_USER=<username> --build-arg REGISTRY_PASSWORD=<password> -t my-image .
```

Replace <username> and <password> with your actual credentials. The -t option tags the image with the name my-image.
