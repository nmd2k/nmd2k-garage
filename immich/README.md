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

## Backup