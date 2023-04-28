# Docker cheat sheet
runs images on docker engine  
running container, rm - removes docker container after exiting, it - interactable, d - detached, p - port `<host port>:<container port>`  
```
docker run --rm -itd -p 80:80 --name <container name> <image>
```

-v  tells to mount given dir to container dir, `<host dir>:<container dir>`  

run container with compose from yml file  


check running containers  
```
docker ps
```
list iamges  
```
docker images
```

docker exec https://docs.docker.com/engine/reference/commandline/exec/  
executes command in container  
```
docker exec -d <containername> <command> <args>
```
start new shell session on wanted container  
```
docker exec -it <containername> sh
```

### networking
after installing docker we get docker0 interface. The default bridge.  
every deployed container gets connected to the interface (default interface if not specified)  
```
bridge link
```
```
docker inspect bridge
```

run container connected to the specified network. host can be used in which case container doesnt have virtual interface  
```
--network <network> 
```

creates user defined bridge, which you specify when creating container  

```
docker network create <name>
```

creating macvlan, https://docs.docker.com/network/macvlan/  
```
docker network create --driver=macvlan --subnet=<subnet> --gateway=<gateway> --ip-range=<ip_range> -o parent=<physical interface> <name>
```
ip range =  is not needed if you are going to specify ip address when creating container, using  
```
--ip <ipaddr>
```
dockers dhcp assigns ip addresses to containers and so it wont get ip from local one, so container has its own ip  
all containers made on macvlan network are connected through **same interface(parent)** on router,  might not work,  

macvlan 802.1q trunk bridge, requires trunking set up,  
```
-o parent=<phyint>.20
```

ipvlan L2, containers created in this network will have same mac as host but will have their own ip address  
```
--driver=ipvlan
```

ipvlan L3 https://docs.docker.com/network/ipvlan/  

overlay  

null network, name none  

#### issues encountered
making docker bridge network with subnet as phyiscal (as you would make macvlan and ipvlan) 'breaks' network for that machine, as you cant have two interfaces with same subnet. not really a docker issue, but networking.  