# Adguard

## Using Macvlan
If you want to use `macvlan` use this instruction.

### Create Macvlan
In this example a network of type `macvlan` will be created, in the command the arguments are:

- `-d macvlan` - driver to use / network type
- `--subnet=192.168.1.0/24` - lan network range
- `--ip-range=192.168.1.240/28` - ip range the vlan will use
- `--gateway=192.168.1.1` - router ip
- `--aux-address="server=192.168.1.254"` - (optional) exclude ip from ip range
- `-o parent=eth0` - network interface from host
- `vlan` - the name of the network

The complete command would be:
```
sudo docker network create -d macvlan --subnet=192.168.1.0/24 --ip-range=192.168.1.240/29 --gateway=192.168.1.1 --aux-address="server=192.168.1.254" -o parent=eth0 vlan
```

With this the network is created.

### Macvlan on Docker Compose
To use the `macvlan` on the container you need to add the configuration to the compose file.
You can specify one ip address to use or let the network assign one from the defined `ip-range`.
```
# Inside the service
services:
  adguardhome:
    ...
    networks:
      vlan:
        ipv4_address: 192.168.1.250

# Specify networks for the stack
networks:
  vlan:
    external: true
```

The container will be created using the `macvlan` network and be assigned with the ip `192.168.1.250`, as if a separate machine in the network.

### Route configuration
You may have some problems reaching the `macvlan` network from `lan` or `vpn`, this is a fixer for that.
On the Docker host run:
```
# Host macvlan bridge
sudo ip link add vlan-br0 link eth0 type macvlan mode bridge
# Add IP for the link, has to be available
sudo ip addr add 192.168.1.240/32 dev vlan-br0
sudo ip link set vlan-br0 up
# Add route to all containers in macvlan subnet
sudo ip route add 192.168.1.240/28 dev vlan-br0
```

Change `vlan` from `vlan-br0`, if you created the network with another name, leaving `-br0`.

This adds a link with the ip address `192.168.1.240` and adds a route to all the containers running in the `vlan` subnet.