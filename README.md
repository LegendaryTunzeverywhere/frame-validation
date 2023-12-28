# Instructions on how to Run Frame Validator Node.
## I will be using Ubuntu 22.04 server on WSL to perform this task.

# Step 1 — Installing Docker

* First, update your existing list of packages:

```
sudo apt update
```

* Set up Docker's `apt` repository.

```
sudo apt-get update
sudo apt-get install ca-certificates curl gnupg
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg
```

* Add the repository to Apt sources:

```
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
```

* Finally, install Docker:

```
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

* Verify that the Docker Engine installation is successful by running the hello-world image.

```
sudo docker run hello-world
```

* If you have an existing Docker installation on your local machine, you should consider updating using the doc : https://docs.docker.com/engine/install/ubuntu/

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
