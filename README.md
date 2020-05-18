## Install and Use Docker on Ubuntu 18 LTS

The Docker installation package available in the official Ubuntu 18.04 repository may not be the latest version. To get this latest version, install Docker from the official Docker repository. This section shows you how to do just that.

To begin, remove any existing docker installations:

    sudo apt-get remove docker docker-engine docker.io containerd runc

Next, install packages we require to install the official docker version:

    sudo apt-get ca-certificates apt-transport-https curl gnupg-agent software-properties-common

Then, in order to ensure the downloads are valid, add the GPG key for the official Docker repository to your system:

    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

Verify that the key got added using the following command:

    sudo apt-key fingerprint 0EBFCD88

Add the Docker repository to APT sources:

    sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu bionic stable"

Next, update the package database with the Docker packages from the newly added repo:

    sudo apt-get update

Make sure you are about to install from the Docker repo instead of the default Ubuntu 18.04 repo:

    apt-cache policy docker-ce

You should see output similar to the follow:
Output of apt-cache policy docker-ce

    docker-ce:
      Installed: (none)
      Candidate: 5:19.03.8~3-0~ubuntu-bionic
      Version table:
     *** 5:19.03.8~3-0~ubuntu-bionic 500
            500 https://download.docker.com/linux/ubuntu bionic/stable amd64 Packages


Notice that docker-ce is not installed, but the candidate for installation is from the Docker repository for Ubuntu 18.04 (bionic).

Finally, install Docker:

    sudo apt-get install -y docker-ce

Docker should now be installed, the daemon started, and the process enabled to start on boot. Check that it's running:

    sudo systemctl status docker

The output should be similar to the following, showing that the service is active and running:

    ● docker.service - Docker Application Container Engine
       Loaded: loaded (/lib/systemd/system/docker.service; enabled; vendor preset: enabled)
       Active: active (running) since Thu 2020-05-14 21:30:38 EDT; 2min 1s ago
         Docs: https://docs.docker.com
     Main PID: 19779 (dockerd)
        Tasks: 25
       CGroup: /system.slice/docker.service
               └─19779 /usr/bin/dockerd -H fd:// --containerd=/run/containerd/containerd.sock

Installing Docker installs both Docker service (daemon) and the docker command line utility, or the Docker client.

[Instructions on running docker as a non-root user](RUN_AS_USER.md)