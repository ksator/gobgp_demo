# About this repository

GoBGP demo using Docker Compose 

# Requirements to run this repository 

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

# Instructions to use this repository

- Clone this repository 
```
git clone https://github.com/ksator/gobgp_demo.git
cd gobgp_demo
```
- Run these commands 
```
docker-compose -f docker-compose.yml up -d
Creating network "gobgp_demo_test_net" with driver "bridge"
Creating gobgp_2 ... done
Creating gobgp_1 ... done
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
430539ef3813   ksator/gobgp:1.0   "gobgpd -t yaml -f /…"   About a minute ago   Up About a minute   179/tcp   gobgp_2
0b042e4b3a1a   ksator/gobgp:1.0   "gobgpd -t yaml -f /…"   About a minute ago   Up About a minute   179/tcp   gobgp_1
```
```
docker network ls | grep gobgp
2b346040f380   gobgp_demo_test_net   bridge    local
```
```
docker-compose ps
 Name                Command               State    Ports 
----------------------------------------------------------
gobgp_1   gobgpd -t yaml -f /etc/gob ...   Up      179/tcp
gobgp_2   gobgpd -t yaml -f /etc/gob ...   Up      179/tcp
```
```
docker exec -it gobgp_1 gobgp neighbor
Peer          AS  Up/Down State       |#Received  Accepted
10.0.0.200 65002 00:01:43 Establ      |        0         0
```
```
docker exec -it gobgp_2 bash
root@430539ef3813:/go# gobgp neighbor
Peer          AS  Up/Down State       |#Received  Accepted
10.0.0.100 65001 00:00:57 Establ      |        0         0
root@430539ef3813:/go# gobgp global  
AS:        65002
Router-ID: 192.168.255.0
Listening Port: 179, Addresses: 0.0.0.0, ::
root@430539ef3813:/go# exit
exit
```
```
docker-compose down
Stopping gobgp_1 ... done
Stopping gobgp_2 ... done
Removing gobgp_1 ... done
Removing gobgp_2 ... done
Removing network gobgp_demo_test_net
```


