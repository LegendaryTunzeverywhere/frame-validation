# Instructions on how to Run Frame Validator Node.
## I will be using Ubuntu 20.04 server on WSL to perform this task.

# Step 1 — Installing Docker

* First, update your existing list of packages:

```
sudo apt update
```

* Next, install a few prerequisite packages which let apt use packages over HTTPS:

```
sudo apt install apt-transport-https ca-certificates curl software-properties-common
```

follow th prompt that comes during the installation.

* Next, add the GPG key for the official Docker repository to your system:

```
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```

you should get the 'ok' respond if it was successful.

* Then, add the Docker repository to APT sources:

```
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"
```

* This will also update our package database with the Docker packages from the newly added repo.

* Make sure you are about to install from the Docker repo instead of the default Ubuntu repo:

```
apt-cache policy docker-ce
```

You’ll see output like this, although the version number for Docker may be different:

`docker-ce:
  Installed: (none)
  Candidate: 5:19.03.9~3-0~ubuntu-focal
  Version table:
     5:19.03.9~3-0~ubuntu-focal 500
        500 https://download.docker.com/linux/ubuntu focal/stable amd64 Packages`

* Finally, install Docker:

```
sudo apt install docker-ce
```

follow the prompt and complete installation.

# Step 2. 
