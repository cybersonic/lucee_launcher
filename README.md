# Lucee (Docker) Launcher Script

This repository contains a Bash script for running and managing a [Lucee Docker](https://github.com/lucee/lucee-dockerfiles) container with various customizable options. The script provides an easy way to set up a container with pre-configured environment variables, volumes, and more.
The main goal is being able to run [Lucee](https://www.lucee.org/) from whichever folder you are in, and being able to launch different versions of Lucee quickly and easily.

This script is a standard bash script that was written to run on macOS. It should run on linux but I havent tested it yet. 

## Features
- Run a Lucee Docker container with custom image and tag options.
- Attach volumes to the container.
- Set environment variables for the container.
- Automatically find available ports if the default is taken.
- Supports listing tags from Docker Hub, running containers in detached mode, stopping running containers, and viewing logs.
- Includes a dry-run mode to preview the Docker command before executing it.
## Dependencies
The script is designed to go on macOS primarily but I am sure it works in *nix environments. 
It also requires Docker to be installed and running

## Installation
The easiest way to install the script is to add the `lucee` file it to your local `~/bin` folder. You will then be able to call it from the command line wherever you need it. 

## Usage
### Basic Command
The script can be executed with the following command:

```sh
lucee [options] [action]
```

### Options
- **`-i, --image IMAGE`**: Set the Docker image (default: `lucee/lucee`).
- **`-t, --tag TAG`**: Set the Docker image tag (default: `5.4.7.1-SNAPSHOT`).
- **`-p, --port PORT`**: Set the host port for the container (default: `3000`).
- **`-v, --volume, -V PATTERN`**: Add volume patterns (repeatable). Format is `[host_path]:[container_path]`.
  - Example: `-v /path/on/host:/path/in/container`.
- **`-e, --env KEY=VALUE`**: Set environment variable for the container (repeatable).
  - Example: `-e MY_VAR=my_value`.
- **`-d, --detach`**: Run the container in detached mode.
- **`list`**: List available image tags from Docker Hub.
- **`logs`**: Show logs of the currently running container.
- **`stop`**: Stop the currently running container.
- **`dry-run`**: Show the Docker command that would be executed without running it.

### Examples
#### Run Container with a custom lucee version (tag)
```sh
lucee  -t 6.2.0.137-SNAPSHOT -p 3000
```

#### Attach a Volume and Set Environment Variable
```sh
lucee -v /host/path:/container/path -e ENV_VAR=value
```

#### Run in Detached Mode
```sh
lucee --detach
```

#### List Available Tags for Default Image
```sh
lucee list
```

### Notes
- The script will assign a container name based on the current working directory.
- If a container with the same name is already running, the script will not start a new one. Stop the existing container using the `stop` command.
- By default, the script will find an available port within 100 increments of the provided port.

### Dependencies
- **Docker**: Ensure Docker is installed and running on your system.
- **jq**: Required for listing available tags from Docker Hub. Install it with:
  ```sh
  sudo apt-get install jq
  ```

### Common Scenarios
#### Viewing Logs
To view logs of a currently running container:
```sh
lucee logs
```

#### Stopping a Running Container
To stop the running container associated with the current directory:
```sh
lucee stop
```

### Dry Run Mode
If you'd like to preview the Docker command before actually running it, use the `dry-run` option:
```sh
lucee dry-run
```

## License
This project is licensed under the MIT License.

## Contributions
Feel free to submit issues or pull requests to enhance the script's capabilities or fix bugs. Your contributions are always welcome!

## Author

Maintained by [Mark Drew](https://markdrew.io).
