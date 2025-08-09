# Portainer

Check out the official page: https://docs.portainer.io/start/install-ce/server/docker/linux

First, create the volume that Portainer Server will use to store its database:

```bash
docker volume create portainer_data
```
Then, download and install the Portainer Server container:

```bash
docker run -d -p 8000:8000 -p 9443:9443 --name portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce:lts
```

## Agent
If connect multiple portainer, we use agent. Go to environment and start wizard with docker standalone. Run this on monitor machine:

```bash
docker run -d \
  -p 9001:9001 \
  --name portainer_agent \
  --restart=always \
  -v /var/run/docker.sock:/var/run/docker.sock \
  -v /var/lib/docker/volumes:/var/lib/docker/volumes \
  -v /:/host \
  portainer/agent:2.27.9
```

Now you should able to connect agent via port 9001 (e.g. 192.168.1.222:9001).

*Notes:* Using wsl2 need to forward port to windows before it can connect to your deployed port. (https://learn.microsoft.com/en-us/windows/wsl/networking#accessing-a-wsl-2-distribution-from-your-local-area-network-lan)

In short, run:
```bash
netsh interface portproxy add v4tov4 listenport=<yourPortToForward> listenaddress=0.0.0.0 connectport=<yourPortToConnectToInWSL> connectaddress=(wsl hostname -I)
```
Example:

```bash
netsh interface portproxy add v4tov4 listenport=4000 listenaddress=0.0.0.0 connectport=4000 connectaddress=192.168.101.100
```

*Notes 2:* Might need a crontab to schedule this task since wsl hostname can change after reboot.