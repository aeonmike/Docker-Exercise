# Docker-Exercise

# Install Docker

# Create Dockerhub Account

# Create Github Account

Login to GitHub using the Linux CLI, follow these steps:

Open a terminal window on your Linux machine.

Install Git if it is not already installed by running the following command:

```
sudo apt-get install git
```

Once Git is installed, navigate to the directory where you want to store your GitHub repository by using the cd command.

Run the following command to configure your Git username and email address:

```
git config --global user.name "Your Name"
git config --global user.email "your_email@example.com"
```

Replace "Your Name" with your name, and "your_email@example.com" with your email address.

Generate a new personal access token (PAT) on GitHub by following these steps:

Log in to your GitHub account.
Click on your profile picture in the top-right corner of the screen and select "Settings" from the dropdown menu.
Click on "Developer settings" in the left sidebar.
Click on "Personal access tokens".
Click on "Generate new token".
Enter a name for your token and select the appropriate scopes for your needs.
Click on "Generate token".

In your terminal window, run the following command:

```
git config --global credential.helper store
```

This command tells Git to store your credentials in plaintext on disk.

Run the following command to open the Git credentials file in a text editor:

```
nano ~/.git-credentials
```

Add the following line to the file, replacing "your_username" with your GitHub username and "your_token" with the PAT you generated in step 5:

```
https://your_username:your_token@github.com
```

Save the file and exit the text editor.

That's it! You are now logged in to GitHub using the Linux CLI, and you can use Git to push and pull changes to and from your GitHub repositories.

# Login to Dockerhub account via Docker CLI

To log in to your Docker Hub account via the Docker CLI, follow these steps:

Open a terminal window on your machine.

Run the following command:

```
docker login
```

This will prompt you for your Docker Hub username and password.

```
Enter your Docker Hub username and press Enter.
```

```
Enter your Docker Hub password and press Enter.
```

If you have two-factor authentication (2FA) enabled on your Docker Hub account, you will be prompted to enter a one-time verification code. You can obtain the code from your 2FA app or device.

If your credentials are correct, you will see a message that says "Login Succeeded".

That's it! You are now logged in to your Docker Hub account via the Docker CLI, and you can use Docker to push and pull images to and from Docker Hub.



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
