[linuxserverurl]: https://linuxserver.io
[forumurl]: https://forum.linuxserver.io
[ircurl]: https://www.linuxserver.io/irc/
[podcasturl]: https://www.linuxserver.io/podcast/

[![linuxserver.io](https://raw.githubusercontent.com/linuxserver/docker-templates/master/linuxserver.io/img/linuxserver_medium.png)][linuxserverurl]

The [LinuxServer.io][linuxserverurl] team brings you another container release featuring easy user mapping and community support. Find us for support at:
* [forum.linuxserver.io][forumurl]
* [IRC][ircurl] on freenode at `#linuxserver.io`
* [Podcast][podcasturl] covers everything to do with getting the most from your Linux Server plus a focus on all things Docker and containerisation!

# linuxserver/h5ai

h5ai is a modern file indexer for HTTP web servers with focus on your files. Directories are displayed in a appealing way and browsing them is enhanced by different views, a breadcrumb and a tree overview. Initially h5ai was an acronym for HTML5 Apache Index but now it supports other web servers too.

[hub]: https://hub.docker.com/r/linuxserver/h5ai/

[![h5ai](https://raw.githubusercontent.com/linuxserver/docker-templates/master/linuxserver.io/img/h5ai-icon.png)][h5ai]
[h5ai]: https://larsjung.de/h5ai/

## Usage

```
docker create \
  --name=h5ai \
  -v <path to data>:/config \
  -v <path to shared folder>:/config/www/sharedfolder/
  -e PGID=<gid> -e PUID=<uid>  \
  -p 80:80 \
  linuxserver/h5ai
```

## Parameters

`The parameters are split into two halves, separated by a colon, the left hand side representing the host and the right the container side. 
For example with a port -p external:internal - what this shows is the port mapping from internal to external of the container.
So -p 8080:80 would expose port 80 from inside the container to be accessible from the host's IP on port 8080
http://192.168.x.x:8080 would show you what's running INSIDE the container on port 80.`



* `-p 80` - the port(s)
* `-v /config` - config files for h5ai
* `-v /config/www/shared-folder - Folder to be shared over h5ai
* `-e PGID` for GroupID - see below for explanation
* `-e PUID` for UserID - see below for explanation

It is based on alpine linux with s6 overlay, for shell access whilst the container is running do `docker exec -it organizr /bin/bash`.

### User / Group Identifiers

Sometimes when using data volumes (`-v` flags) permissions issues can arise between the host OS and the container. We avoid this issue by allowing you to specify the user `PUID` and group `PGID`. Ensure the data volume directory on the host is owned by the same user you specify and it will "just work" ™.

In this instance `PUID=1001` and `PGID=1001`. To find yours use `id user` as below:

```
  $ id <dockeruser>
    uid=1001(dockeruser) gid=1001(dockergroup) groups=1001(dockergroup)
```

## Setting up the application

Access the webui at http://[IP]:[PORT]/h5ai/

## Info

* Shell access whilst the container is running: `docker exec -it h5ai /bin/bash`
* To monitor the logs of the container in realtime: `docker logs -f h5ai`

* container version number 

`docker inspect -f '{{ index .Config.Labels "build_version" }}' h5ai`

* image version number

`docker inspect -f '{{ index .Config.Labels "build_version" }}' linuxserver/h5ai`

## Versions

+ **dd.MM.yy:** Initial Release.

