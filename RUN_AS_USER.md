## Run docker as a non-root user

Create the docker group:

    $ sudo groupadd docker

Add your user to the docker group:

    $ sudo usermod -aG docker $USER

Update permissions on local docker folder, if you encounter errors:

    $ sudo chown "$USER":"$USER" /home/"$USER"/.docker -R
    $ sudo chmod g+rwx "$HOME/.docker" -R

