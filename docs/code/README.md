---
tags:
  - DOCKER
  - GUIDE
  - LINUX
---

# Docker Tutorial

This guide is for [Linux], specifically [Ubuntu 22.04].

  [Linux]: https://en.wikipedia.org/wiki/Linux

  [Ubuntu 22.04]: https://releases.ubuntu.com/jammy

## Introduction

[**Docker**] is an application that simplifies the process of managing application processes in containers. Containers let you run your applications in resource-isolated processes. They’re similar to virtual machines, but containers are more portable, more resource-friendly, and more dependent on the host operating system.

  [**Docker**]: https://www.docker.com/

For a detailed introduction to the different components of a `Docker` container, check out [The Docker Ecosystem: An Introduction to Common Components].

  [The Docker Ecosystem: An Introduction to Common Components]: https://www.digitalocean.com/community/tutorials/the-docker-ecosystem-an-introduction-to-common-components

In this tutorial, you’ll install and use `Docker` Community Edition (CE) on [Ubuntu 22.04]. You’ll install `Docker` itself, work with containers and images, and push an image to a `Docker` Repository.

## Prerequisites

To follow this tutorial, you will need the following:

- One Ubuntu 22.04 server set up by following the [Ubuntu 22.04 initial server setup guide], including a `sudo` non-**root** user and a firewall.
- An account on [Docker Hub] if you wish to create your own images and push them to Docker Hub, as shown in [Step 7](../code/docker.md#Step-7-Committing-changes-in-a-container-to-a-docker-image) and [Step 8].

  [Step 8]: ../code/docker.md#step-8—pushing-docker-images-to-a-docker-repository

  [Ubuntu 22.04 initial server setup guide]: https://www.digitalocean.com/community/tutorials/initial-server-setup-with-ubuntu-22-04

  [Docker Hub]: https://hub.docker.com/
