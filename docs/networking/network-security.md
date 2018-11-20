# Network Security

## Displaying Network Activity

Before you can secure your network, you need to know what exactly you need to secure. Gathering information about your network is a great place to start. Let's say you want to allow the network to access a service on your Linux system. Before you can do that, you'll need to find out what port is being used by that service. You can use the `ss` or `netstat` commands to find this information. The `ss` command stands for "socket statistics", replacing `netstat` on CentOS 7 and later. Let's take a look on how to use `ss`.

!!! example "Example: Usage of `ss`."

    The `ss` command is best used with the `-p`, `l`, `n`, and `t` options. These options show the process using the socket, show listening sockets, display the numeric port number, and display TCP only sockets respectively. These are by far the most useful options for `ss` and can best be remembered by thinking it's "plant" without the "a".

    ```
    $ ss -plnt
    State       Recv-Q Send-Q                 Local Address:Port                                Peer Address:Port
    LISTEN      0      128                                *:111                                            *:*
    LISTEN      0      128                                *:22                                             *:*
    LISTEN      0      100                        127.0.0.1:25                                             *:*
    LISTEN      0      128                               :::111                                           :::*
    LISTEN      0      128                               :::22                                            :::*
    LISTEN      0      100                              ::1:25                                            :::*
    ```

## Firewall Security

Once you know which ports your service is using, you must configure your firewall to allow or deny access to these ports. Firewalls can be configured to allow or deny access to ports based on a variety of factors such as source IP address or source interface. Firewalls can also inspect a packet's headers to selectively allow or deny a packet. Most firewalls operate using an implicit deny meaning that if a packet does not match an allow rule, the packet is denied.

In CentOS 7 and later, the default firewall program is `firewalld`. The `firewalld` program is essentially a wrapper around the lower-level `iptables` utility, providing a simpler syntax to create firewall rules. The advantage of `firewalld` is that it operates using the concept of zones. Although we are only going to use the default `public` zone here, it is a good idea to understand when and why you would use the other zones.

Before you can use the `firewalld` program, you must install it using `yum install firewalld` and start and enable the `firewalld` service. Once you have the `firewalld` service started, you can begin to run `firewall-cmd` commands. 

The `firewalld` program operates using two configurations. The first configuration is the runtime configuration which is the live configuration that is currently loaded in the kernel. The second configuration is the permanent configuration that will be applied on a reboot of the service or the system. Understanding the difference between these two configurations is key to making persistent firewall changes. All `firewall-cmd` commands affect the runtime configuration unless the `--permanent` option is used. 

Let's take a look at how we can use `firewall-cmd` to configure the firewall.

!!! example "Example: Usage of `firewall-cmd`."

    List all of the current rules for the default zone.

    ```
    $ sudo firewall-cmd --list-all
    public (active)
      target: default
      icmp-block-inversion: no
      interfaces: eth0
      sources:
      services: ssh dhcpv6-client
      ports:
      protocols:
      masquerade: no
      forward-ports:
      source-ports:
      icmp-blocks:
      rich rules:
    ```
    
    Add a rule to the runtime configuration to allow port 80/tcp.

    ```
    $ sudo firewall-cmd --add-port=80/tcp
    ```
    
    Add a rule to the permanent configuration to allow port 80/tcp.

    ```
    $ sudo firewall-cmd --add-port=80/tcp --permanent
    ```
    
    Remove a rule from the runtime configuration to allow port 80/tcp.

    ```
    $ sudo firewall-cmd --remove-port=80/tcp
    ```
    
    Remove a rule from the permanent configuration to allow port 80/tcp.

    ```
    $ sudo firewall-cmd --remove-port=80/tcp --permanent
    ```

    Add a rule to the runtime configuration to allow the https service.

    ```
    $ sudo firewall-cmd --add-service=https
    ```
    
    Add a rule to the permanent configuration to allow the https service.

    ```
    $ sudo firewall-cmd --add-service=https --permanent
    ```

    Reload the permanent configuration, overwriting the runtime configuration..

    ```
    $ sudo firewall-cmd --reload
    ```
    
    Save the runtime configuration to the permanent configuration.

    ```
    $ sudo firewall-cmd --runtime-to-permanent
    ```
