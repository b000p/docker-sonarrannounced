[linuxserverurl]: https://linuxserver.io
[forumurl]: https://forum.linuxserver.io
[ircurl]: https://www.linuxserver.io/irc/
[podcasturl]: https://www.linuxserver.io/podcast/

[![linuxserver.io](https://raw.githubusercontent.com/linuxserver/docker-templates/master/linuxserver.io/img/linuxserver_medium.png)][linuxserverurl]

The [LinuxServer.io][linuxserverurl] team brings you another container release featuring easy user mapping and community support. Find us for support at:
* [forum.linuxserver.io][forumurl]
* [IRC][ircurl] on freenode at `#linuxserver.io`
* [Podcast][podcasturl] covers everything to do with getting the most from your Linux Server plus a focus on all things Docker and containerisation!

# linuxserver/sonarrannounced


[![](https://images.microbadger.com/badges/image/linuxserver/sonarrannounced.svg)](http://microbadger.com/images/linuxserver/sonarrannounced "Get your own image badge on microbadger.com")[![Docker Pulls](https://img.shields.io/docker/pulls/linuxserver/sonarrannounced.svg)][hub][![Docker Stars](https://img.shields.io/docker/stars/linuxserver/sonarrannounced.svg)][hub][![Build Status](http://jenkins.linuxserver.io:8080/buildStatus/icon?job=Dockers/LinuxServer.io-hub-built/linuxserver-sonarrannounced)](http://jenkins.linuxserver.io:8080/job/Dockers/job/LinuxServer.io-hub-built/job/linuxserver-sonarrannounced/)
[hub]: https://hub.docker.com/r/linuxserver/sonarrannounced/

[sonarrannounced](https://github.com/l3uddz/sonarrAnnounced) is an automatic NZB and torrent downloader. You can keep a "movies I want" list and it will search for NZBs/torrents of these movies every X hours. Once a movie is found, it will send it to SABnzbd or download the torrent to a specified directory.


## Usage

```
docker create \
	--name=sonarrannounced \
	-v <path to data>:/config \
	-e PGID=<gid> -e PUID=<uid>  \
	-e TZ=<timezone> \
	-p 3467:3467 \
	stealthgyro/sonarrannounced
```

## Parameters

`The parameters are split into two halves, separated by a colon, the left hand side representing the host and the right the container side. 
For example with a port -p external:internal - what this shows is the port mapping from internal to external of the container.
So -p 8080:80 would expose port 80 from inside the container to be accessible from the host's IP on port 8080
http://192.168.x.x:8080 would show you what's running INSIDE the container on port 80.`


* `-p 3467` - the port(s)
* `-v /config` - sonarrannounced Application Data
* `-e PGID` for for GroupID - see below for explanation
* `-e PUID` for for UserID - see below for explanation
* `-e TZ` for timezone information, eg Europe/London

It is based on alpine-linux with S6 overlay, for shell access whilst the container is running do `docker exec -it sonarrannounced /bin/bash`.

### User / Group Identifiers

Sometimes when using data volumes (`-v` flags) permissions issues can arise between the host OS and the container. We avoid this issue by allowing you to specify the user `PUID` and group `PGID`. Ensure the data volume directory on the host is owned by the same user you specify and it will "just work" ™.

In this instance `PUID=1001` and `PGID=1001`. To find yours use `id user` as below:

```
  $ id <dockeruser>
    uid=1001(dockeruser) gid=1001(dockergroup) groups=1001(dockergroup)
```

## Setting up the application
Access the webui at `<your-ip>:3467`, for more information check out [sonarrannounced](https://github.com/l3uddz/sonarrAnnounced).

## Info

* To monitor the logs of the container in realtime `docker logs -f sonarrannounced`.

## Version Log

+ **07.02.17:** Rebase to alpine 3.5. 
+ **11.11.16:** Stop cp logging to docker log (they are accessible in the webui and the config folder)
+ **30.09.16:** Fix umask.
+ **09.09.16:** Add layer badges to README
+ **27.08.16:** Add badges to README
+ **08.08.16:** Rebase to alpine linux
+ **12.11.15:** Misc Code Cleanup
+ **02.10.15:** Change to python baseimage. 
+ **28.07.15:** Updated to latest baseimage (for testing), and a fix to autoupdate. 
