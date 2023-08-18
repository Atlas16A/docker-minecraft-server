---
title: Docker and Basics
---

!!! info

    This guide is intended for users who have little to no experience with Docker, Docker Compose, and Minecraft Servers.

!!! note

    This setup guide is currently only for users setting up on a local PC such as a laptop or desktop.

## Downloading [Docker](https://www.docker.com/)

1. Use the link above to navigate to Docker's website.
2. Download Docker desktop for your OS
3. Docker has a very well put together guide for installing Docker Desktop, Follow their [guide](https://docs.docker.com/desktop/) and come back here when your done.

## Docker Compose

Now that you have Docker desktop installed you already have Docker Compose!

Docker Compose is a tool that allows you to define and manage multi-container applications. It uses a YAML file to define the services, networks, and volumes required for your application, making it easier to orchestrate complex setups.

What this all means in short is you will more easily create, edit, and manage your server. It is highly recommended you use Docker Compose going forward, however the respective command prompt input will be given as well.

!!! note "Visual Studio Code"

    While not neccesary, [Visual Studio Code](https://code.visualstudio.com/) is a great editor for yaml files. We recommend using it going forward, however it is not neccesary and all this can be done inside a normal text editor such as notepad.

## Using [Docker Compose](https://docs.docker.com/compose/)

1.  Create a folder. It can be anywhere you want, this will contain everything we do.
2.  Create a file in your folder called `docker-compose.yml`
3.  In the file you just created add the code from the code block below. (Read the explanations below it so you understand what each part is.)
4.  Save the file and head over to a Command Prompt/Terminal

    !!! note

        In VS Code you can do ctrl+shift+` to open a new terminal

5.  In your command line type `docker compose up -d` and hit enter

    !!! info

        To apply changes made to the compose file, just run `docker compose up -d` again.

        Follow the logs of the container using `docker compose logs -f`, check on the status with `docker compose ps`, and stop the container `using docker compose stop`.

6.  You should now see your container in Docker desktop (Or whatever tool you use to manage docker)

7.  Congrats youve made your first docker contained Minecraft server! Continue to Server Management to customize the server to your liking.

!!! note "Command Prompt Equivalent"

    `docker run -d -it -p 25565:25565 -e EULA=TRUE itzg/minecraft-server`

```yaml
version: "3.8"

services:
  mc:
    image: itzg/minecraft-server
    tty: true
    stdin_open: true
    ports:
      - "25565:25565"
    environment:
      EULA: "TRUE"
    volumes:
      - ./data:/data
```

| Tag                            | Explanation                                                                                                                                                                                                                                                              |
| ------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `version: "3.8"`               | This specifies the version of the Docker Compose file format being used. In this case, it's version 3.8. Different versions might support varying features and syntax.                                                                                                   |
| `services:`                    | This section defines the individual services (containers) that compose your application.                                                                                                                                                                                 |
| `mc:`                          | This is the name of the service. You can name it anything however you'll need to use that name in various commands.                                                                                                                                                      |
| `image: itzg/minecraft-server` | This line specifies the Docker image to be used for the container. The image named "itzg/minecraft-server" will be pulled from a Docker registry (like Docker Hub) and used to create the container. This image likely contains a pre-configured Minecraft server setup. |
| `tty: true`                    | This specifies that a pseudo-TTY (terminal) should be allocated for the container. This is often used for interactive applications.                                                                                                                                      |
| `stdin_open: true`             | This allows the standard input (stdin) to be kept open, which is also useful for interactive applications that require input.                                                                                                                                            |
| `ports:`                       | This section maps ports from the host machine to the container.                                                                                                                                                                                                          |
| `"25565:25565"`                | This line maps port 25565 from the host to port 25565 in the container. Minecraft servers typically use this port for communication.                                                                                                                                     |
| `environment`                  | This section allows you to set environment variables within the container. The majority of your settings will be in this field.                                                                                                                                          |
| `EULA: "TRUE"`                 | Mojang requires servers to accept the End User License Agreement (EULA) in order to run as the docker image is not the end user this must be set to true by you the user, and setting this environment variable to "TRUE" acknowledges that acceptance.                  |
| `volumes`                      | This section defines volume mappings between the host and the container. Volumes are used to persist data outside the container and share it between the container and the host.                                                                                         |
| `./data:/data`                 | This line maps the local directory named data (relative to the location of the Docker Compose file) to the /data path inside the container. This can be used to store Minecraft world data or any other data that needs to be persisted.                                 |
