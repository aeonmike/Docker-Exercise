# Docker-Exercise

# Install Docker

# Create Dockerhub Account

# Create Github Account

# Login to Dockerhub account via Docker CLI


# Pull Images from docker

Here's an example Dockerfile that pulls an image from a private registry:


```
FROM private-registry.example.com/my-image:latest
```

In this example, private-registry.example.com is the hostname of the private registry, my-image is the name of the image, and latest is the tag.

If the private registry requires authentication, you can include the credentials in the FROM instruction:

```
FROM private-registry.example.com/my-image:latest
ARG REGISTRY_USER
ARG REGISTRY_PASSWORD
RUN echo "$REGISTRY_PASSWORD" | docker login --username "$REGISTRY_USER" --password-stdin private-registry.example.com
```

In this example, the ARG instructions define variables that can be passed to the docker build command using the --build-arg option. The RUN instruction logs in to the private registry using the provided credentials.

To build the image, you can run:

```
docker build --build-arg REGISTRY_USER=<username> --build-arg REGISTRY_PASSWORD=<password> -t my-image .
```

Replace <username> and <password> with your actual credentials. The -t option tags the image with the name my-image.

# Create and image and upload to your Dockerhub registry

To create an Ubuntu image with Nginx HTML files using a Dockerfile and upload it to a private registry on Docker Hub, follow these steps:

Create a Dockerfile that defines your image. Here is an example:

```
FROM ubuntu:latest
RUN apt-get update && apt-get install -y nginx
COPY html /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
```

This Dockerfile uses Ubuntu as the base image, installs the Nginx web server, copies an html directory containing HTML files to the web server's default directory, and exposes port 80. It then sets the command that will be run when the container starts to start the Nginx server in the foreground.

Create a directory called html in the same directory as the Dockerfile, and place your HTML files inside it.

Build the Docker image using the Dockerfile:

```
docker build -t my-nginx-image .
```

This command builds the Docker image using the Dockerfile in the current directory, and tags the image as my-nginx-image.

Tag the image with the name of your Docker Hub private registry:

```
docker tag my-nginx-image my-dockerhub-username/my-nginx-image
```

Replace my-dockerhub-username with your Docker Hub username, and my-nginx-image with the name you want to give to the image in your private registry.

Log in to Docker Hub using the Docker CLI:

```
docker login --username=my-dockerhub-username --password=my-dockerhub-password
```

Replace my-dockerhub-username with your Docker Hub username, and my-dockerhub-password with your Docker Hub password.

Push the Docker image to your private registry on Docker Hub:

```
docker push my-dockerhub-username/my-nginx-image
```

This command uploads the Docker image to your private registry on Docker Hub.

That's it! Your Docker image is now uploaded to your private registry on Docker Hub, and you can use it to create containers or deploy it to your production environment.
