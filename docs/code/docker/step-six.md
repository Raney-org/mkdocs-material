---
tags:
  - DOCKER
  - TUTORIAL
---

# Step 6 — Managing `Docker` Containers

After using `Docker` for a while, you’ll have many active (running) and inactive containers on your computer. To view the active ones, use:

``` sh
docker ps
```

You will see output similar to the following:

``` sh title="Output"
CONTAINER ID        IMAGE               COMMAND             CREATED
```

In this tutorial, you started two containers; one from the hello-world image and another from the ubuntu image. Both containers are no longer running, but they still exist on your system.

To view all containers — active and inactive, run `#!shell docker ps with the -a switch`:

``` sh
docker ps -a
```

You’ll see output similar to this:

``` sh title="Output"
CONTAINER ID   IMAGE         COMMAND   CREATED         STATUS                     PORTS     NAMES
1c08a7a0d0e4   ubuntu        "bash"     About a minute ago   Exited (0) 7 seconds ago             dazzling_taussig
587000e49d53   hello-world   "/hello"   5 minutes ago        Exited (0) 5 minutes ago             adoring_kowalevski
```

To view the latest container you created, pass it the `-l` switch:

``` sh
docker ps -l
```

``` sh title="Output"
CONTAINER ID   IMAGE     COMMAND   CREATED         STATUS                     PORTS     NAMES
1c08a7a0d0e4   ubuntu    "bash"    3 minutes ago   Exited (0) 2 minutes ago             dazzling_taussig
```

To start a stopped container, use `docker start`, followed by the container ID or the container’s name. Let’s start the Ubuntu-based container with the ID of `#!shell 1c08a7a0d0e4`:

``` sh
`docker start 1c08a7a0d0e4
```

The container will start, and you can use `#!shell docker ps` to see its status:

``` sh title="Output"
CONTAINER ID   IMAGE     COMMAND   CREATED         STATUS         PORTS     NAMES
1c08a7a0d0e4   ubuntu    "bash"    6 minutes ago   Up 8 seconds             dazzling_taussig
```

To stop a running container, use `#!shell docker stop`, followed by the container ID or name. This time, we’ll use the name that Docker assigned the container, which is `dazzling_taussig`:

``` sh
`docker stop dazzling_taussig
```

Once you’ve decided you no longer need a container anymore, remove it with the `#!shell docker rm` command, again using either the container ID or the name. Use the `#!shell docker ps -a` command to find the container ID or name for the container associated with the `hello-world` image and remove it.

``` sh
`docker rm adoring_kowalevski
```

You can start a new container and give it a name using the `--name` switch. You can also use the `--rm` switch to create a container that removes itself when it’s stopped. See the `docker run` **help** command for more information on these options and others.

Containers can be turned into images which you can use to build new containers. Let’s look at how that works.
