# Containers

## Podman

Podman is a tool for running linux containers.

### Installation

#### Ubuntu 18.04

```bash
echo "deb https://download.opensuse.org/repositories/devel:/kubic:/libcontainers:/stable/xUbuntu_18.04/ /" | sudo tee /etc/apt/sources.list.d/devel:kubic:libcontainers:stable.list
curl -L "https://download.opensuse.org/repositories/devel:/kubic:/libcontainers:/stable/xUbuntu_18.04/Release.key" | sudo apt-key add -
sudo apt-get update
sudo apt-get -y upgrade
sudo apt-get -y install podman
```

#### Ubuntu 20.04

```bash
echo "deb https://download.opensuse.org/repositories/devel:/kubic:/libcontainers:/stable/xUbuntu_20.04/ /" | sudo tee /etc/apt/sources.list.d/devel:kubic:libcontainers:stable.list
curl -L "https://download.opensuse.org/repositories/devel:/kubic:/libcontainers:/stable/xUbuntu_20.04/Release.key" | sudo apt-key add -
sudo apt-get update
sudo apt-get -y upgrade
sudo apt-get -y install podman
```

**Ref:** [Podman Installation](https://podman.io/getting-started/installation)

### Basic commands

```bash
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

### Daemon Configuration and Volumes

```bash
```
