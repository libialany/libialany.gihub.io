---
title:  "Self-Hosting Your Music Player!"
subtitle: "Empower Your Music Experience"
author: "Lib"
avatar: "img/authors/wferr.png"
image: "img/music.jpg"
date:   2023-10-8 12:30:39
---

### Description
<p style="font-size: 15px;">In today's digital age, music is more accessible than ever before. With streaming services and online music platforms dominating the industry, we often rely on third-party providers to enjoy our favorite tunes. But what if I told you there's a way to take full control of your music library and listening experience? Enter self-hosted music players – the ultimate solution for music enthusiasts who crave independence and customization.</p>

### Requirements
- Docker
- Nfs
 
 Improved versions: Tailscale

### Getting Started with Self-Hosting

**`self-hosting platform`**

- Jellyfin

 We choose Jellyfin the docker image that we build taking into account that some parts of the dockerfile need to be configured.

 [link docker](https://jellyfin.org/docs/general/installation/container/)


```bash
version: '3.5'
services:
  jellyfin:
    image: jellyfin/jellyfin
    container_name: jellyfin 
    user: 1000:1000 # User perimsion
    network_mode: 'host' # 
    volumes:
      - ./folder/config:/config
      - ./folder/cache:/cache
      - ./folder/media:/media
      - ./folder/media2:/media2:ro #importante
    restart: 'unless-stopped'
    environment:
      - JELLYFIN_PublishedServerUrl=http://example.com #
    extra_hosts:
      - "host.docker.internal:host-gateway" #
```

1. `user`: This field specifies the username or UID (User ID) to use when running the container. 
2. `network_mode`: When you set the network mode to "host," it means that the container shares the network namespace with the host system. 
3. `volumes`: it maps the local directory `./folder/media2` to the container directory `/media2`. The `:ro` at the end specifies that the volume is mounted in read-only mode.
4. `restart`: it's set to `'unless-stopped'`.This is a common policy for services that should always run and recover from failures.
5. `environment`: This section allows you to set environment variables for the container. In our example, it sets the `JELLYFIN_PublishedServerUrl` environment variable to `http://example.com`. Environment variables are often used to configure applications within the container.
6. `extra_hosts`: This section allows you to add entries to the container's `/etc/hosts` file. In our snippet, it adds an entry that maps `"host.docker.internal"` to `"host-gateway"`. This can be useful for resolving hostnames or making the container aware of other services running on the host system.

**`Set up a server`**

- Nfs

I would like all my friends to upload their music, NFS (Network File System) is a mechanism for storing files on a network.
As our music volumes are set to a folder we can share it so that they can upload their files.
Another option is to create another user and allow them to upload.

[link Nfs](https://www.server-world.info/en/note?os=Ubuntu_22.04&p=nfs)


```shell
/home/nfsshare 10.0.0.0/24(rw,no_root_squash)
```

**`Access your music`**

Create an account for all your friends

### Finally

Empower your music collection and listening experience.

I love Open Source.


