---
title: Running Docker on MacOS
draft: false
tags:
---
Terminology:
* Docker Engine
	* open-source
	* container lifecycle, isolation of resources
	* **runs on Linux only** (or a Linux virtual machine)
* Docker CLI
	* open-source
	* interacts with engine using `docker` command
* Docker Desktop
	* closed-source
	* manages virtualization required for Docker Engine on Windows and macOS

### Running the Docker Engine on a Linux VM without Docker Desktop

We will use the Docker engine (daemon) that comes with [minikube](https://minikube.sigs.k8s.io/docs/) and [hyperkit](https://minikube.sigs.k8s.io/docs/drivers/hyperkit/) for virtualization:
```bash
brew install hyperkit   # virtualization
brew install minikube   # K8s cluster, with Docker daemon
brew install docker     # Docker CLI
```

We can then start the minikube cluster an connect it with the Docker CLI:
```bash
minikube start
eval $(minikube docker-env)
```

References:
* [Blog post](https://dhwaneetbhatt.com/blog/run-docker-without-docker-desktop-on-macos/) by Dhwaneet Bhatt