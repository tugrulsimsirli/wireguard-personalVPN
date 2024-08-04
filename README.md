### Requirements

You need to have an VPN machine. On this machine, you should follow the steps in Instructions.

**Note: Commands is available to Linux machines.**



---



### Instructions

#### 1. Install Docker

```bash
sudo apt-get update \
  && sudo apt-get install ca-certificates curl gnupg git wget apt-transport-https software-properties-common \
  && sudo install -m 0755 -d /etc/apt/keyrings \
  && curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg \
  && sudo chmod a+r /etc/apt/keyrings/docker.gpg
```  

```bash
echo \
  "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```  

```bash
# Install docker
sudo apt-get update \
  && sudo apt-get install docker-ce \
  docker-ce-cli \
  containerd.io \
  docker-buildx-plugin \
  docker-compose-plugin \
  && sudo groupadd docker \
  && sudo usermod -aG docker $USER \
  && newgrp docker \
  && sudo systemctl enable docker.service \
  && sudo systemctl enable containerd.service
```

#### 2. Deploy The Repo(wireguard-personalVPN)

```bash
# Clone the repository from GitHub
git clone https://github.com/tugrulsimsirli/wireguard-personalVPN.git

# Change directory to the cloned repository
cd wireguard-personalVPN

# Update the .env file with your configuration. File has explanations.
nano .env

# Start the Docker containers
docker compose up
```


---


### WireGuard Settings

- After the `docker compose up` command. WireGuard and PiHole will be up. Open your web browser on your device and go to <http://YOUR_PUBLIC_IP:51821/>
- Login with your WG_PASSWORD value
- Create new connection with "+ New" button. You can create the connection with QR Code or conf file on your devices.
