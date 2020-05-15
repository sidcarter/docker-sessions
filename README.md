## Install and Use Docker on Ubuntu 18 LTS:

Step 1 — Installing Docker

The Docker installation package available in the official Ubuntu 16.04 repository may not be the latest version. To get this latest version, install Docker from the official Docker repository. This section shows you how to do just that.

To begin, remove any existing docker installations:

    sudo apt-get remove docker docker-engine docker.io containerd runc

Next, install packages we require to install the official docker version:

    sudo apt-get ca-certificates apt-transport-https curl gnupg-agent software-properties-common

Then, in order to ensure the downloads are valid, add the GPG key for the official Docker repository to your system:

    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

Add the Docker repository to APT sources:

    sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu bionic stable"

Next, update the package database with the Docker packages from the newly added repo:

    sudo apt-get update

Make sure you are about to install from the Docker repo instead of the default Ubuntu 16.04 repo:

    apt-cache policy docker-ce

You should see output similar to the follow:
Output of apt-cache policy docker-ce

    docker-ce:
      Installed: (none)
      Candidate: 18.06.1~ce~3-0~ubuntu
      Version table:
         18.06.1~ce~3-0~ubuntu 500
            500 https://download.docker.com/linux/ubuntu xenial/stable amd64 Packages


Notice that docker-ce is not installed, but the candidate for installation is from the Docker repository for Ubuntu 16.04 (xenial).

Finally, install Docker:

    sudo apt-get install -y docker-ce


Docker should now be installed, the daemon started, and the process enabled to start on boot. Check that it's running:

    sudo systemctl status docker

The output should be similar to the following, showing that the service is active and running:

Output

    ● docker.service - Docker Application Container Engine
       Loaded: loaded (/lib/systemd/system/docker.service; enabled; vendor preset: enabled)
       Active: active (running) since Thu 2018-10-18 20:28:23 UTC; 35s ago
         Docs: https://docs.docker.com
     Main PID: 13412 (dockerd)
       CGroup: /system.slice/docker.service
               ├─13412 /usr/bin/dockerd -H fd://
               └─13421 docker-containerd --config /var/run/docker/containerd/containerd.toml

Installing Docker now gives you not just the Docker service (daemon) but also the docker command line utility, or the Docker client. We'll explore how to use the docker command later in this tutorial.

