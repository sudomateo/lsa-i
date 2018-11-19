# Network Troubleshooting

All networks will eventually have some issues. Here's some of the ways you can troubleshoot a network connection.

## Troubleshooting Network Connectivity

The `ping` command is used to test network connectivity. The `ping` command will send an ICMP packet to a specified host. If the host is up and responding to ICMP packets, you will receive an ICMP reply. The rule of thumb here is that if you can ping a host, you have network connectivity to that host, barring any firewall restrictions.

!!! example "Example: Usage of `ping`."

    ```
    $ ping 8.8.8.8
    PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
    64 bytes from 8.8.8.8: icmp_seq=1 ttl=63 time=17.7 ms
    64 bytes from 8.8.8.8: icmp_seq=2 ttl=63 time=17.1 ms
    64 bytes from 8.8.8.8: icmp_seq=3 ttl=63 time=18.9 ms
    ^C
    --- 8.8.8.8 ping statistics ---
    3 packets transmitted, 3 received, 0% packet loss, time 2004ms
    rtt min/avg/max/mdev = 17.123/17.945/18.928/0.761 ms
    ```

    ```
    $ ping google.com
    PING google.com (172.217.3.78) 56(84) bytes of data.
    64 bytes from mia07s54-in-f14.1e100.net (172.217.3.78): icmp_seq=1 ttl=63 time=16.4 ms
    64 bytes from mia07s54-in-f14.1e100.net (172.217.3.78): icmp_seq=2 ttl=63 time=17.4 ms
    64 bytes from mia07s54-in-f14.1e100.net (172.217.3.78): icmp_seq=3 ttl=63 time=18.0 ms
    ^C
    --- google.com ping statistics ---
    3 packets transmitted, 3 received, 0% packet loss, time 2003ms
    rtt min/avg/max/mdev = 16.490/17.344/18.044/0.652 ms
    ```

If your `ping` command fails, you might want to see where along the network path your ping dropped off. This is where the `tracepath` and `traceroute` commands come in. These commands are used to measure the network hops from your system to another system.

!!! example "Example: Usage of `tracepath`."

    ```
    $ tracepath centos.org
     1?: [LOCALHOST]                                         pmtu 1500
     1:  gateway                                               0.484ms
     1:  gateway                                               0.142ms
     2:  ubnt                                                  1.555ms asymm 64
     3:  96.120.36.145                                        14.781ms asymm 63
     4:  xe-0-0-2-sur01.westboca.fl.pompano.comcast.net       12.894ms asymm 62
     5:  xe-11-0-3-0-sur02.westboca.fl.pompano.comcast.net    12.551ms asymm 61
     6:  ae-5-ar02.stuart.fl.pompano.comcast.net              18.975ms asymm 60
     7:  be-40-ar01.northdade.fl.pompano.comcast.net          32.310ms asymm 59
     8:  be-20214-cr02.miami.fl.ibone.comcast.net             19.644ms asymm 58
     9:  be-12274-pe01.nota.fl.ibone.comcast.net              18.441ms asymm 57
    10:  ae9.mpr1.mia2.us.zip.zayo.com                        19.733ms asymm 56
    11:  ae3.mpr1.mia1.us.zip.zayo.com                        19.561ms asymm 55
    12:  ae0.mpr2.mia1.us.zip.zayo.com                        20.026ms asymm 54
    13:  ae5.cs1.dca2.us.zip.zayo.com                        119.160ms asymm 53
    14:  ae4.cs1.lga5.us.eth.zayo.com                        121.379ms asymm 52
    15:  ae5.cs1.lhr11.uk.eth.zayo.com                       119.892ms asymm 51
    16:  ae0.cs1.lhr15.uk.eth.zayo.com                       121.345ms asymm 50
    17:  ae2.cs1.ams10.nl.eth.zayo.com                       119.418ms asymm 49
    18:  ae3.er1.ams1.nl.zip.zayo.com                        119.739ms asymm 48
    19:  xe-7-6.rt1.ams2.baseip.com                          136.517ms asymm 47
    20:  xe-1-1.rt1.ams1.baseip.com                          120.726ms asymm 46
    21:  85.12.30.226                                        119.292ms !H
         Resume: pmtu 1500
    ```

## Troubleshooting DNS Resolution

There may be a time where you have network connectivity but you cannot resolve DNS names. Knowing how to troubleshooting is just as useful as troubleshooting network connectivity. There are a few commands you can use to troubleshoot DNS such as `dig`, `host`, and `nslookup`.

The `dig` command is used to make a DNS request and print the reply to the screen. `dig` has many options but the most commonly used options are `-t` and `@` which are detailed below.

!!! example "Example: Usage of `dig`."

    ```
    $ dig google.com

    ; <<>> DiG 9.9.4-RedHat-9.9.4-61.el7_5.1 <<>> google.com
    ;; global options: +cmd
    ;; Got answer:
    ;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 46134
    ;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 0

    ;; QUESTION SECTION:
    ;google.com.			IN	A

    ;; ANSWER SECTION:
    google.com.		300	IN	A	172.217.3.78

    ;; Query time: 39 msec
    ;; SERVER: 10.0.2.3#53(10.0.2.3)
    ;; WHEN: Mon Nov 19 04:54:24 UTC 2018
    ;; MSG SIZE  rcvd: 54
    ```

!!! example "Example: Usage of `dig` with `-t` to query the TXT records."

    ```
    dig -t TXT google.com

    ; <<>> DiG 9.9.4-RedHat-9.9.4-61.el7_5.1 <<>> -t TXT google.com
    ;; global options: +cmd
    ;; Got answer:
    ;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 35208
    ;; flags: qr rd ra; QUERY: 1, ANSWER: 3, AUTHORITY: 0, ADDITIONAL: 0

    ;; QUESTION SECTION:
    ;google.com.			IN	TXT

    ;; ANSWER SECTION:
    google.com.		3600	IN	TXT	"facebook-domain-verification=22rm551cu4k0ab0bxsw536tlds4h95"
    google.com.		3600	IN	TXT	"v=spf1 include:_spf.google.com ~all"
    google.com.		300	IN	TXT	"docusign=05958488-4752-4ef2-95eb-aa7ba8a3bd0e"

    ;; Query time: 32 msec
    ;; SERVER: 10.0.2.3#53(10.0.2.3)
    ;; WHEN: Mon Nov 19 04:55:53 UTC 2018
    ;; MSG SIZE  rcvd: 236
    ```

!!! example "Example: Usage of `dig` with `@` to specify the name server to use."

    ```
    dig google.com @9.9.9.9

    ; <<>> DiG 9.9.4-RedHat-9.9.4-61.el7_5.1 <<>> google.com @9.9.9.9
    ;; global options: +cmd
    ;; Got answer:
    ;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 43882
    ;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

    ;; OPT PSEUDOSECTION:
    ; EDNS: version: 0, flags:; udp: 4096
    ;; QUESTION SECTION:
    ;google.com.			IN	A

    ;; ANSWER SECTION:
    google.com.		123	IN	A	172.217.1.110

    ;; Query time: 24 msec
    ;; SERVER: 9.9.9.9#53(9.9.9.9)
    ;; WHEN: Mon Nov 19 04:57:36 UTC 2018
    ;; MSG SIZE  rcvd: 55
    ```

The `host` and `nslookup` commands are also used to perform DNS lookups. They are much simpler than `dig` and also require the `bind-utils` package to be installed.

!!! example "Example: Usage of `host`."

    ```
    $ host google.com
    google.com has address 172.217.3.78
    google.com has IPv6 address 2607:f8b0:4008:80e::200e
    google.com mail is handled by 30 alt2.aspmx.l.google.com.
    google.com mail is handled by 10 aspmx.l.google.com.
    google.com mail is handled by 40 alt3.aspmx.l.google.com.
    google.com mail is handled by 20 alt1.aspmx.l.google.com.
    google.com mail is handled by 50 alt4.aspmx.l.google.com.
    ```

!!! example "Example: Usage of `nslookup`."

    ```
    nslookup google.com
    Server:		10.0.2.3
    Address:	10.0.2.3#53

    Non-authoritative answer:
    Name:	google.com
    Address: 172.217.3.78
    ```
