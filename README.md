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

`docker-ce:`
  `Installed: (none)`
 `Candidate: 5:19.03.9~3-0~ubuntu-focal`
 `Version table:`
     `5:19.03.9~3-0~ubuntu-focal 500`
        `500 https://download.docker.com/linux/ubuntu focal/stable amd64 Packages`

* Finally, install Docker:

```
sudo apt install docker-ce
```

follow the prompt and complete installation.

# Step 2. create a local directory where the validator config and node data

* Once you have Docker installed, you should create a local directory where the validator config and node data will live. Here's a suggestion:

```
mkdir frame-validator
cd frame-validator
mkdir data
cd data
```

* You will then need to download the frame validator config

```
git clone https://github.com/frame-network/node-config.git && cd node-config
```

* After cloning the repo, open the testnet.config file and replace <SEPOLIA_RPC_HERE> with your Sepolia RPC url.

```
vi testnet.json
```

press letter `i` on your keyboard and change the sepolia rpc to yours.
 _you can get an rpc from [Infura](https://www.infura.io) they provide all type of rpc(S) for evm chain
  _press the `esc` key press `:` and `x` and enter to save your changes.

# Step 3. Running the Validator

* Change directory by using the `cd ..` twice to navigate to the frame-validator directory.
* Then run this.

* create a .sh file by 

```
vi run.sh
```

press the letter `i` on your keyboard, copy the below, press the `esc` key press `:` and `x` and enter to save your changes.

```
docker run \
--name frame \
--rm \
-it \
-v $(pwd)/node-data:/home/user/.frame \
-v $(pwd)/node-config/testnet.json:/home/user/testnet.json public.ecr.aws/o8e2k8j7/nitro-node:frame \
--conf.file testnet.json
```

Then, run this line of bash the shell file created using.

```
bash run.sh
```

This will start the docker and also start the frame validator node.
