## Run docker as a non-root user

1. Create the docker group:

    $ sudo groupadd docker

2. Add your user to the docker group:

    $ sudo usermod -aG docker $USER

3. Update permissions on local docker folder:

    $ sudo chown "$USER":"$USER" /home/"$USER"/.docker -R
    $ sudo chmod g+rwx "$HOME/.docker" -R

