# Requirements to run this demo 

- Install Docker 
- Install Docker Compose 

```
docker --version
Docker version 20.10.1, build 831ebea
```
```
docker-compose --version
docker-compose version 1.27.4, build 40524192
```

# Instructions 

- Clone this repository 
```
git clone https://github.com/ksator/gobgp_demo.git
cd gobgp_demo
```
- Run these commands 
```
docker-compose -f docker-compose.yml up -d
```
```
docker images
REPOSITORY         TAG           IMAGE ID       CREATED          SIZE
ksator/gobgp       1.0           f8cbe28b2372   56 minutes ago   1.05GB
golang             latest        b09f7387a719   12 days ago      862MB
```
```
docker ps
CONTAINER ID   IMAGE              COMMAND                  CREATED              STATUS              PORTS     NAMES
f1493531e5d3   ksator/gobgp:1.0   "gobgpd -t yaml -f /…"   About a minute ago   Up About a minute   179/tcp   gobgp_2
68e99c720baa   ksator/gobgp:1.0   "gobgpd -t yaml -f /…"   About a minute ago   Up About a minute   179/tcp   gobgp_1
```
```
docker exec -it gobgp_1 gobgp neighbor
Peer          AS  Up/Down State       |#Received  Accepted
10.0.0.200 65002 00:01:43 Establ      |        0         0
```
```
docker stop gobgp_1 gobgp_2
gobgp_1
gobgp_2
```
```
docker rm gobgp_1 gobgp_2
gobgp_1
gobgp_2
```


