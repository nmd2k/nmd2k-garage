# Immich

To install Immich, follow our guide: https://immich.app/docs/install/docker-compose

## Remote ML
If you wish to run Machine learning features (including facial detection, etc), run this in your machine:

```
name: immich

services:
    immich-machine-learning:
        container_name: immich_machine_learning
        # For hardware acceleration, add one of -[armnn, cuda, rocm, openvino, rknn] to the image tag.
        # Example tag: ${IMMICH_VERSION:-release}-cuda
        image: ghcr.io/immich-app/immich-machine-learning:${IMMICH_VERSION:-release}
        # extends: # uncomment this section for hardware acceleration - see https://immich.app/docs/features/ml-hardware-acceleration
        #   file: hwaccel.ml.yml
        #   service: cpu # set to one of [armnn, cuda, rocm, openvino, openvino-wsl, rknn] for accelerated inference - use the `-wsl` version for WSL2 where applicable
        volumes:
        - model-cache:/cache
        env_file:
        - .env
        restart: always
        healthcheck:
        disable: false

volumes:
   model-cache:

```

And config via admin control panel for directing task to port 3003 (e.g. 192.168.1.222:3003) (the default port is 3003)
*Notes*: If run via wsl2, remember to forward port to window. (https://learn.microsoft.com/en-us/windows/wsl/networking#accessing-a-wsl-2-distribution-from-your-local-area-network-lan)

In short, run:
```bash
netsh interface portproxy add v4tov4 listenport=<yourPortToForward> listenaddress=0.0.0.0 connectport=<yourPortToConnectToInWSL> connectaddress=(wsl hostname -I)
```
Example:

```bash
netsh interface portproxy add v4tov4 listenport=4000 listenaddress=0.0.0.0 connectport=4000 connectaddress=192.168.101.100
```

*Notes 2:* Might need a crontab to schedule this task since wsl hostname can change after reboot.

## Backup

## Nginx config

Add this to proxy nginx manager:
```bash
# allow large file uploads
client_max_body_size 50000M;

# set timeout
proxy_read_timeout 600s;
proxy_send_timeout 600s;
send_timeout       600s;
```