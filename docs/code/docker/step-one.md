---
tags:
  - DOCKER
  - TUTORIAL
---

# Step 1 — Installing `Docker`

The [**Docker**] installation package available in the official Ubuntu repository may not be the latest version. To ensure we get the latest version, we’ll install `Docker` from the official `Docker` repository. To do that, we’ll add a new package source, add the GPG key from `Docker` to ensure the downloads are valid, and then install the package.

First, update your existing list of packages:

```shell title="Update Packages"
sudo apt update
```

Next, install a few prerequisite packages which let `apt` use packages over HTTPS:

``` sh
sudo apt install apt-transport-https ca-certificates curl software-properties-common
```

Then add the GPG key for the official `Docker` repository to your system:

```sh
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/`docker`-archive-keyring.gpg
```

Add the `Docker` repository to APT sources:

```sh
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/`docker`-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/`docker`.list > /dev/null
```

Update your existing list of packages again for the addition to be recognized:

``` sh
sudo apt update
```

Make sure you are about to install from the `Docker` repo instead of the default Ubuntu repo:

``` sh
apt-cache policy docker-ce
```

You’ll see output like this, although the version number for `Docker` may be different:

```sh title="Output of apt-cache policy docker-ce"
docker-ce:
  Installed: (none)
  Candidate: 5:20.10.14~3-0~ubuntu-jammy
  Version table:
     5:20.10.14~3-0~ubuntu-jammy 500
        500 https://download.docker.com/linux/ubuntu jammy/stable amd64 Packages
     5:20.10.13~3-0~ubuntu-jammy 500
        500 https://download.docker.com/linux/ubuntu jammy/stable amd64 Packages
```

???+ info
    Notice that `docker-ce` is not installed, but the candidate for installation is from the `Docker` repository for Ubuntu 22.04 (`jammy`).

Finally, install `Docker`:

``` sh
sudo apt install docker-ce
```

`Docker` should now be installed, the daemon started, and the process enabled to start on boot. Check that it’s running:

``` sh
sudo systemctl status docker
```

The output should be similar to the following, showing that the service is active and running:

``` sh
Output
● docker.service - Docker Application Container Engine
     Loaded: loaded (/lib/systemd/system/docker.service; enabled; vendor preset: enabled)
     Active: active (running) since Fri 2022-04-01 21:30:25 UTC; 22s ago
TriggeredBy: ● docker.socket
       Docs: https://docs.docker.com
   Main PID: 7854 (docker.d)
      Tasks: 7
     Memory: 38.3M
        CPU: 340ms
     CGroup: /system.slice/docker.service
             └─7854 /usr/bin/dockerd -H fd:// --containerd=/run/containerd/containerd.sock
```

Installing `Docker` now gives you not just the `Docker` service (daemon) but also the ``docker`` command line utility, or the `Docker` client. We’ll explore how to use the ``docker`` command later in this tutorial.
