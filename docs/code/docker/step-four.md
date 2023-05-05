---
tags:
  - DOCKER
  - TUTORIAL
---

# Step Four — Working with `Docker` Images

`Docker` containers are built from `Docker` images. By default, `Docker` pulls these images from `Docker` Hub, a `Docker` registry managed by `Docker`, the company behind the `Docker` project. Anyone can host their `Docker` images on [Docker Hub], so most applications and Linux distributions you’ll need will have images hosted there.

To check whether you can access and download images from `Docker` Hub, type:

``` sh
docker run hello-world
```

The output will indicate that `Docker` in working correctly:

``` sh title="Output"
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
2db29710123e: Pull complete
Digest: sha256:bfea6278a0a267fad2634554f4f0c6f31981eea41c553fdf5a83e95a41d40c38
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working correctly.

...
```

`Docker` was initially unable to find the hello-world image locally, so it downloaded the image from [Docker Hub], which is the default repository. Once the image downloaded, `Docker` created a container from the image and the application within the container executed, displaying the message.

You can search for images available on Docker Hub by using the `docker` command with the search subcommand. For example, to search for the Ubuntu image, type:

``` sh
docker search ubuntu
```

The script will crawl Docker Hub and return a listing of all images whose name matches the search string. In this case, the output will be similar to this:

``` sh title="Output"
NAME                             DESCRIPTION                                     STARS     OFFICIAL   AUTOMATED
ubuntu                           Ubuntu is a Debian-based Linux operating sys…   14048     [OK]
websphere-liberty                WebSphere Liberty multi-architecture images …   283       [OK]
ubuntu-upstart                   DEPRECATED, as is Upstart (find other proces…   112       [OK]
neurodebian                      NeuroDebian provides neuroscience research s…   88        [OK]
open-liberty                     Open Liberty multi-architecture images based…   51        [OK]
...
```

In the **OFFICIAL** column, **OK** indicates an image built and supported by the company behind the project. Once you’ve identified the image that you would like to use, you can download it to your computer using the pull subcommand.

Execute the following command to download the official ubuntu image to your computer:

``` sh
docker pull ubuntu
```

You’ll see the following output:

``` sh title="Output"
Using default tag: latest
latest: Pulling from library/ubuntu
e0b25ef51634: Pull complete
Digest: sha256:9101220a875cee98b016668342c489ff0674f247f6ca20dfc91b91c0f28581ae
Status: Downloaded newer image for ubuntu:latest
docker.io/library/ubuntu:latest
```

After an image has been downloaded, you can then run a container using the downloaded image with the run subcommand. As you saw with the hello-world example, if an image has not been downloaded when `docker` is executed with the run subcommand, the `Docker` client will first download the image, then run a container using it.

To see the images that have been downloaded to your computer, type:

``` sh
docker images
```

The output will look similar to the following:

``` sh title="Output"
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
ubuntu              latest              1d622ef86b13        3 weeks ago         73.9MB
hello-world         latest              bf756fb1ae65        4 months ago        13.3kB
```

As you’ll see later in this tutorial, images that you use to run containers can be modified and used to generate new images, which may then be uploaded (pushed is the technical term) to Docker Hub or other `Docker` registries.

Let’s look at how to run containers in more detail.
