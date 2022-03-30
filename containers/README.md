# Containers

## Podman

Podman is a tool for running linux containers.

### Installation

#### Ubuntu 18.04

```sh
echo "deb https://download.opensuse.org/repositories/devel:/kubic:/libcontainers:/stable/xUbuntu_18.04/ /" | sudo tee /etc/apt/sources.list.d/devel:kubic:libcontainers:stable.list
curl -L "https://download.opensuse.org/repositories/devel:/kubic:/libcontainers:/stable/xUbuntu_18.04/Release.key" | sudo apt-key add -
sudo apt-get update
sudo apt-get -y upgrade
sudo apt-get -y install podman
```

#### Ubuntu 20.04

```sh
echo "deb https://download.opensuse.org/repositories/devel:/kubic:/libcontainers:/stable/xUbuntu_20.04/ /" | sudo tee /etc/apt/sources.list.d/devel:kubic:libcontainers:stable.list
curl -L "https://download.opensuse.org/repositories/devel:/kubic:/libcontainers:/stable/xUbuntu_20.04/Release.key" | sudo apt-key add -
sudo apt-get update
sudo apt-get -y upgrade
sudo apt-get -y install podman
```

**Ref:** [Podman Installation](https://podman.io/getting-started/installation)

### Basic commands

```sh
# Verify installation
podman info

# Check list of images
podman images

# Check list of containers
podman ps

# Check list of all containers including stopped
podman ps -a

# Run a simple container and check the output
podman run --name test-container -d busybox:latest echo "Hello World"

# Check the output
podman logs test-container

# Cleanup
podman rm test-container

# Run a container in interactive mode
podman run --name test-container -it busybox:latest sh

# Cleanup
podman rm test-container
```

**Notes:**

- `podman logs <container_name_or_id>` is used to check logs

### Daemon Configuration

```sh
# Create a dir
mkdir -p $HOME/data/mongodb

# Run daemon mongodb container
podman run -d --name mongo \
  -e MONGO_INITDB_ROOT_USERNAME=myadmin \
  -e MONGO_INITDB_ROOT_PASSWORD=mysecret \
  -v $HOME/data/mongodb:/data/db \
  -p 27020:27017 \
  mongo

# Stop a container
podman stop mongo

# Start a container
podman start mongo

# Connect to localhost:27020 in vs-code's mongodb extension (https://marketplace.visualstudio.com/items?itemName=ms-vscode.mongodb)


# Cleanup
podman stop mongo && podman rm mongo
```

**Notes**:

- `MONGO_INITDB_ROOT_USERNAME` and `MONGO_INITDB_ROOT_PASSWORD` are environment variables.
- `-v $HOME/data/mongodb:/data/db` mounts the directory `$HOME/data/mongodb` to the container as `/data/db`.
- `-p 27020:27017` binds the port `27020` to the container port `27017`.
- `-d` runs the container in detached mode.
- `--name mongo` sets the name of the container.

### Dockerfile

Lets write a simple Dockerfile for go application

```Dockerfile
FROM scratch

COPY ./sample-rest /opt/sample-rest

EXPOSE 8080

CMD ["/opt/sample-rest"]
```

Let's build a container image and run it

```sh
# Build the image
podman build -t sample-rest .

# Check the image
podman images

# Run the image
podman run -d --name sample -p 8080:8080 localhost/sample-rest

# Open browser and navigate to http://localhost:8080/api/hello

# Cleanup
podman stop sample && podman rm sample
```

**Notes:**

- `podman build -t sample-rest .` builds the image from the Dockerfile.

### Exercises

- Build a docker image for your app and run it.\
  Ex. Java, NGINX, Python, etc.

## VSCode Remote Containers

### Prequisites

- Podman
- Install [ms-vscode-remote.remote-containers](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers) extension
