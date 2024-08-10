# Docker Networking Issue and Solution

## Introduction

Like many people, after putting together a few docker-compose projects, I hit an error when I tried to bring a project up:

> ERROR: could not find an available, non-overlapping IPv4 address pool among the defaults to assign to the network

Specifically, this happened when I had 31 bridge networks, and tried to bring up a compose project that would increase this total to 32.

Searching for the issue, I found it was fairly common, and could be resolved by expanding the range of default address pools.

Before I tell you more - Here’s the rundown on how to fix the problem.

````
sudo nano /etc/docker/daemon.json
````
````
{
  "default-address-pools" : [
    {
      "base" : "172.17.0.0/12",
      "size" : 20
    },
    {
      "base" : "192.168.0.0/16",
      "size" : 24
    }
  ]
}
````
````
sudo systemctl restart docker
````
>After this, contaner may be down, you have to up again previous container

````
docker start <containers-name>
````

Let’s see how many networks I have right now:
````
sudo docker network ls --filter driver=bridge --quiet | wc -l 
````


