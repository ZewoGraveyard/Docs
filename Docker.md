## Developing with Docker

Docker is a set of tools that allows you to package an application with all of its dependencies into a standardized unit.

### Install Docker

#### OS X

Download and install the **Docker Toolbox**.

- [Docker Toolbox](https://www.docker.com/products/docker-toolbox)

Open `Docker Quickstart Terminal`. It will run a bunch of scripts and in the end you'll have something like this.

```sh

                        ##         .
                  ## ## ##        ==
               ## ## ## ## ##    ===
           /"""""""""""""""""\___/ ===
      ~~~ {~~ ~~~~ ~~~ ~~~~ ~~~ ~ /  ===- ~~~
           \______ o           __/
             \    \         __/
              \____\_______/


docker is configured to use the default machine with IP 192.168.99.100
For help getting started, check out the docs at https://docs.docker.com
```

Notice the IP in the output (in our case `192.168.99.100`). This is very important for a future step. Now, check if everything is working by running.

```sh
docker run hello-world
```

If no errors occurs, we're good to go.

#### Linux

Get the latest docker package.

```sh
curl -fsSL https://get.docker.com/ | sh
```

Add your user to the `docker` group.

```sh
sudo usermod -aG docker <your user>
```

Log out, log back in and check if everything is working.

```sh
docker run hello-world
```

If no errors occurs, we're good to go.

### Create a Dockerfile

On the root of you app's project create a file called `Dockerfile`. `APP_NAME` should be the name of your app in your `Package.swift` file. In our case it's `hello`.

```
FROM zewo/swiftdocker:0.5.0

ENV APP_NAME=hello

WORKDIR /$APP_NAME/

ADD ./Package.swift /$APP_NAME/
ADD ./Sources /$APP_NAME/Sources

RUN swift build --configuration release

EXPOSE 8080

CMD .build/release/$APP_NAME
```

### Build a Docker image for your app

Build the Docker Image.

```sh
docker build -t <your username>/hello .
```

This command can take a while the first time, but next times it will run faster. This command downloads and installs all dependencies for the app and then builds the app itself in your container.

### Run it

Run your app inside your container.

```sh
docker run -p 8080:8080 <your username>/myapp
```

#### OS X

On OS X your container lives inside a virtual machine which was configured when you ran `Docker Quickstart Terminal`. This virtual machine can be accessed through the IP that was printed with the docker whale. In our case it was `192.168.99.100`.

Open your favorite browser and go to `<virtual machine ip>:8080/hello`. You should see `hello world` once again, but this time from your docker container. 😛

#### Linux

Open your favorite browser and go to `localhost:8080/hello`. You should see `hello world` once again, but this time from your docker container. 😝
