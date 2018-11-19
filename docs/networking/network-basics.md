# Networking Basics

## Network Interfaces

Every system connected to the network must have a network interface. On a physical system, a network interface is usually your Ethernet port on the motherboard. On a virtual system, a network interface is virtualized and maps to an underlying physical network interface.

### Loopback Interface

Most, if not all, Linux systems have a loopback interface. This interface is usually named `lo` and uses the IPv4 address `127.0.0.1/8`, the IPv6 address `::1/128`, and the hostname `localhost`. When packets are sent to `localhost`, the packets are sent out the `lo` interface and immediate return via the `lo` interface without ever leaving. This loopback interface is useful for connected to other network services running on your Linux system without opening that network service to the rest of the network.

### Network Interfaces

When you want to communicate to other devices on or outside your network, you need a non-loopback network interface. These network interfaces have an IPv4 or IPv6 on the network and can send packets to other hosts on that same network. This is the most common interface.

In Linux, most of these network interfaces have names similar to `ethX`, `enoX`, `ensX`, or `enpXsX` where `X` is the number of the interface on the system.

If you want to see the current network information for a given interface you can use the `ip address` command. This will show information such as the IP address, the subnet mask, and the MAC address of the interface.

!!! example "Example: Using `ip`."
    
    ```
    [vagrant@lsa-i ~]$ ip address
    1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host
       valid_lft forever preferred_lft forever
    2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP group default qlen 1000
    link/ether 52:54:00:c9:c7:04 brd ff:ff:ff:ff:ff:ff
    inet 10.0.2.15/24 brd 10.0.2.255 scope global noprefixroute dynamic eth0
       valid_lft 86245sec preferred_lft 86245sec
    inet6 fe80::5054:ff:fec9:c704/64 scope link
       valid_lft forever preferred_lft forever
    ```

## Network Interface Configuration

All network interfaces on a CentOS machine are configured in `/etc/sysconfig/network-scripts/ifcfg-NAME` files where `NAME` is the network interface name such as `lo` or `eth0`.

This file takes the parameters defined in the following table.

| Parameter   | Description                                                  |
| ----------- | ------------------------------------------------------------ |
| `BOOTPROTO` | The boot protocol to use. One of `dhcp`, `none`, or `bootp`. |
| `DEFROUTE`  | Whether or not to use this interface as the default route.   |
| `DEVICE`    | The name of the interface.                                   | 
| `HWADDR`    | The MAC address.                                             | 
| `IPADDR`    | The IPv4 address.                                            |
| `NETMASK`   | The IPv4 network mask.                                       |
| `GATEWAY`   | The IPv4 gateway.                                            | 
| `ONBOOT`    | Whether or not to intialize this interface on boot.          | 
| `TYPE`      | The type of the interface. Usually `Ethernet`.               |

!!! example "Example: Showing the configuration for an interface named `eth5` located at `/etc/sysconfig/network-scripts/ifcfg-eth5`."
    
    ```
    BOOTPROTO=none
    DEFROUTE=yes
    DEVICE=eth0
    HWADDR=86:cc:71:46:89:7c
    IPADDR=198.211.113.12
    NETMASK=255.255.255.0
    GATEWAY=198.211.113.1
    ONBOOT=yes
    TYPE=Ethernet
    ```

Once you configure an interface in one of the `/etc/sysconfig/networks-scripts/ifcfg-*` files you must restart the network service using `systemctl restart network`. This will allow the Linux network services to read the configuration files and set the appropriate configuration.

## DNS Configuration

DNS configuration for CentOS systems lives in the `/etc/resolv.conf` file. This file takes the following parameters.

| Parameter    | Description                                                                                  |
| ------------ | -------------------------------------------------------------------------------------------- |
| `nameserver` | The DNS nameserver to use for DNS lookups. You can define this multiple times, one per line. |
| `search`     | A space-delimited list of search domains to use when performing lookups.                     |

!!! example "Example: The `/etc/resolv.conf` file."

    ```
    $ cat /etc/resolv.conf
    nameserver 9.9.9.9
    nameserver 149.112.112.112
    search example.com staging.example.com
    ```

Aside from using `/etc/resolv.conf` to set the nameservers, you define manual DNS entries in the `/etc/hosts` file. This file has the following format.

```
IP FQDN HOSTNAME
```

Each line contains a DNS entry that will override all other entries. This is useful for adding static servers that need to be accessed via hostname or for testing DNS changes locally.

!!! example "Example: The `/etc/hosts` file."

    ```
    $ cat /etc/hosts
    192.168.1.11 myhost.example.com myhost
    ```

## IP Addresses, Ports, and Sockets

Many people confuse IP addresses, ports, and sockets so this section will briefly list what each is.

An IP address is how you communicate to other nodes on the same network. This is how network communication is facilitated. IP addresses can be IPv4 or IPv6 and live at Layer 3 of the 7-layer OSI model. An example IP address is `192.168.1.11`.

A port is what is used to connect to a service. Services listen on a port to provide a service to the network. Ports can be TCP or UDP ports and live at Layer 4 of the 7-layer OSI model. An example port would be port `80` for HTTP communication.

Simply put, a socket is the combination of an IP address and a port. It's actually a bit more detailed than this but this is a great starting point. A socket is the full endpoint to access a service over a network. An example of a socket is `192.168.1.11:80`.

As an IT professional it's important to know the port numbers for common services. Here are some common ports to know.

| Port | Protocol | Service    |
| ---- | -------- | ---------- |
| 22   | TCP      | SSH        |
| 53   | TCP/UDP  | DNS        |
| 80   | TCP      | HTTP       |
| 443  | TCP      | HTTPS      |
| 3306 | TCP      | MySQL      |
| 5432 | TCP      | PostgreSQL |
