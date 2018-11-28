---?image=template/img/volume.jpeg

@title[Docker Volumes]

@snap[north text-black span-100]
@fa[terminal fa-2x](Docker Volumes)
@snapend

+++
@title[Overview]

@snap[north-west]
### Overview
@snapend

![types-of-mounts-bind.png](template/img/types-of-mounts-bind.png)

+++
@title[CLI reference]

@snap[north-west]
### CLI reference 
@snapend

@snap[north-east]
### [@fa[info]](https://docs.docker.com/engine/reference/commandline/volume) 
@box[bg-gray rounded](docker volume [COMMAND])
@snapend
<br/>
<br/>

Parameter | Description
------------ | -------------
create | Create a volume
inspect | Display detailed information
ls | List volumes
prune | Remove all unused local volumes
rm | Remove volume

+++
@title[CLI reference]

@snap[north-west]
### CLI reference 
@snapend

@snap[north-east]
### [@fa[info]](https://docs.docker.com/engine/reference/commandline/volume_create) 
@box[bg-gray rounded](docker volume create [OPTIONS] [VOLUME])
@snapend
<br/>

Parameter | Description
------------ | -------------
-d | Driver (default: local)
--label | Metadata
--name | Volume name
-o | Options

+++
@title[Mount vs -v]

@snap[north-west]
### Mount vs -v
@snapend
@ul[](false)
- To bind mounts, all options for volumes are available for both --mount and -v flags.
- When using volumes with services (Swarm), only --mount is supported.
@ulend

+++
@title[Mount vs -v]

@snap[north-west]
### Mount vs -v
@snapend
```bash
# --mount
docker run -d \
  --name devtest \
  --mount source=myvol2,target=/app \
  nginx:latest

# -v
docker run -d \
  --name devtest \
  -v myvol2:/app \
  nginx:latest
```
@[1-5]
@[7-11]

+++
@title[Example tmpfs]

@snap[north-west]
### Example tmpfs 
@snapend

```
# Create tmpfs
docker volume create --driver local \
    --opt type=tmpfs \
    --opt device=tmpfs \
    --opt o=size=100m,uid=1000 \
    foo

# Mount into container
docker run -it --rm -v foo:/foo busybox df -h
```

+++
@title[Example btrfs]

@snap[north-west]
### Example btrfs 
@snapend

```
# Create btrfs
docker volume create --driver local \
    --opt type=btrfs \
    --opt device=/dev/sda2 \
    foo
```
+++
@title[Example nfs]

@snap[north-west]
### Example nfs 
@snapend

```bash
# Create nfs
docker volume create --driver local \
    --opt type=nfs \
    --opt o=addr=192.168.1.1,rw \
    --opt device=:/path/to/dir \
```
