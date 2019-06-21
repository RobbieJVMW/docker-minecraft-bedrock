# Minecraft Bedrock Server in Docker

Run the official Minecraft [Dedicated Bedrock server](https://minecraft.gamepedia.com/Bedrock_Dedicated_Server) (BDS) in Docker.


## Prerequisites

- [Docker](https://www.docker.com/get-started)

## Arguments

| Flag | Description | Default |
| ---- | ----------- | ------- |
| BEDROCK_VERSION | Specific BDS (verion)[https://minecraft.gamepedia.com/Bedrock_Dedicated_Server#History] to download | `1.11.4.2` |
| BEDROCK_DOWNLOAD_URL | Override BDS download URL | "https://minecraft.azureedge.net/bin-linux/bedrock-server-${BEDROCK_VERSION}.zip" |


## Instructions

1. Pull the latest image from [Docker Hub](https://cloud.docker.com/u/iwhite/repository/docker/iwhite/minecraft-bedrock)

```bash
docker pull iwhite/minecraft-bedrock
```

2. Create container and start Bedrock server

See below for a full list of options.

* Create a Bedrock server that accepts connections over ipv4 only

```bash
docker run -dit -p 19132:19132/tcp -p 19132:19132/udp iwhite/minecraft-bedrock
```

* Create a Bedrock server that accepts connections over both ipv4 and ipv6

```bash
docker run -dit -p 19132:19132/tcp -p 19132:19132/udp -p 19133:19133/tcp -p 19133:19133/udp iwhite/minecraft-bedrock
```

* Create a Bedrock server with persistent settings and data

Settings and data are automatically synced before the server starts and anytime the container is stopped.
Doing this ensures files generated by the server are copied to the external volume and loaded after a restart.

Replace `/path/to/minecraft-bedrock` with an absolute path to a local directory.

```bash
docker run -dit -v /path/to/minecraft-bedrock:/data -p 19132:19132/tcp -p 19132:19132/udp iwhite/minecraft-bedrock
```

3. Connect to a running Bedrock server console

```bash
# Find running server container id
docker ps -f ancestor=iwhite/minecraft-bedrock --format "{{.ID}}: {{.Image}} {{.Status}}"
# Attach to server console
docker attach {container id}
```
*To detach when done, type `^P^Q`*
