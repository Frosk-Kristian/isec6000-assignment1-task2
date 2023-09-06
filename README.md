# ISEC6000 Assignment 1 Task 2 - Fork of Saleor Platform
Kristian Frossos, Student No. 20853161

## Table of Contents
* [Introduction](#introduction)
* [Requirements](#requirements)
* [Setup](#setup)
  - [Clone](#cloning-this-repository)
  - [Build](#build-the-project)
* [Run](#run)
  - [Components](#running-application-components)
  - [Stop](#stopping-the-application)
  - [Remove Volumes](#removing-docker-volumes)
  - [Prune Cache](#pruning-docker-cache)
* [Usage](#usage)
* [More Details](#more-details)

## Introduction
Fork of the [Saleor Platform](https://github.com/saleor/saleor-platform) project for use in ISEC6000 Secure Dev Ops - Assignment 1 Task 2, Semester 2 2023 by Kristian Frossos.

## Requirements
* [Docker](https://docs.docker.com/install/)

Tested with WSL2 running a Ubuntu 22.04.2 LTS distro with Docker Desktop on Windows 10.

## Setup
### Cloning this repository
To clone this repository to your local machine, first open a terminal and navigate to or create the folder you wish to store the project in:
```shell
user@host:~$ mkdir folder_name
user@host:~$ cd /path/to/folder_name
user@host:/path/to/folder_name$
```
Then run the following command in your terminal, assuming you have git installed:
```shell
git clone https://github.com/Frosk-Kristian/isec6000-assignment1-task2.git
```

### Build the project
1. The source project uses shared folders to enable live code reloading. Without this, Docker Compose will not start:
    - Windows/MacOS: Add the cloned `isec6000-assignment1-task2` directory to Docker shared directories (Preferences -> Resources -> File sharing).
    - Windows/MacOS: Make sure that in Docker preferences you have dedicated at least 5 GB of memory (Preferences -> Resources -> Advanced).
    - Linux: No action is required, sharing is already enabled and memory for the Docker engine is not limited.

2. In your terminal, navigate to the folder you've stored the project in:
```shell
user@host:~$ cd /path/to/isec6000-assignment1-task2
user@host:/path/to/isec6000-assignment1-task2$
```

3. Build the application:
```shell
docker compose build
```

4. Apply django migrations:
```shell
docker compose run --rm api python3 manage.py migrate
```

5. Populate the database with example data and create the admin user:
```shell
docker compose run --rm api python3 manage.py populatedb --createsuperuser
```
*Note: the `--createsuperuser` argument creates an admin account for `admin@example.com` with the password set to `admin`.*

## Run
1. If you have not already done so, open your terminal and navigate to the directory you've cloned this project to.
```shell
user@host:~$ cd /path/to/isec6000-assignment1-task2
user@host:/path/to/isec6000-assignment1-task2$
```

2. Run the application:
```shell
docker compose up
```

### Running application components
* Backend services only:
```shell
docker compose up api worker
```

* Backend and frontend services
```shell
docker compose up
```

### Stopping the application
* To stop the application, open a terminal in the project directory and run the following:
```shell
docker compose stop
```

### Removing docker volumes
* To remove existing docker volumes, open a terminal in the project directory and run the following:
```shell
docker compose rm
```
*After doing this, you will need to repeat step 3 of [build the project](#build-the-project) before being able to run the application again.*

### Pruning docker cache
* To prune the docker cache, open a terminal in the project directory and run the following:
```shell
docker system prune
```
* This will remove:
    - all stopped containers.
    - all networks not used by at least one container.
    - all dangling images.
    - all dangling build cache.

*After doing this, you will need to redo each step listed under [build the project](#build-the-project) before being able to run the application again.*

## Usage
After running the application, you can find it's components at the following addresses:
* Saleor Core (API) - http://localhost:8000
* Saleor Dashboard - http://localhost:9003
* Jaeger UI (APM) - http://localhost:16686
* Mailpit (Test email interface) - http://localhost:8025

If attempting to access remotely, substitute *localhost* for the address of the server.

## More Details
For further information regarding Saleor Platform, view [their readme](https://github.com/saleor/saleor-platform#readme) and visit [their documentation](https://docs.saleor.io/docs/3.x/).

*[Back to Top](#isec6000-assignment-1-task-2---fork-of-saleor-platform)*
