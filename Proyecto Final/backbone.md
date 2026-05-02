# BGP

# BMS0 - ISP1
```BASH
enable
conf t
    hostname AS100
    ip routing
    interface gig 1/0/1
        no switchport
        ip address 172.16.13.210 255.255.255.252
        no shutdown
    exit
    interface gig 1/1/3
        no switchport
        ip address 192.168.93.1 255.255.255.252
        no shutdown
    exit
    interface gig 1/1/1
        no switchport
        ip address 192.168.93.5 255.255.255.252
        no shutdown
    exit
    router ospf 12
        redistribute bgp 100 metric 100 subnets
        network 172.16.13.208 0.0.0.3 area 0
    exit
    router bgp 100
        redistribute ospf 12
        neighbor 192.168.93.2 remote-as 200
        neighbor 192.168.93.6 remote-as 300
        network 192.168.93.0 mask 255.255.255.252
        network 192.168.93.4 mask 255.255.255.252
    exit

``` 

# BMS0 - ISP2 - AS200
```BASH
en
conf t
    hostname AS200
    ip routing
    interface gig 1/1/1
        no switchport
        ip address 192.168.93.2 255.255.255.252
        no shutdown
    exit
    interface gig 1/1/2
        no switchport
        ip address 192.168.93.9 255.255.255.252
        no shutdown
    exit
    router ospf 1
        redistribute bgp 200 metric 100 subnets
    exit

    router bgp 200
    redistribute ospf 1
    neighbor 192.168.93.1 remote-as 100
    neighbor 192.168.93.10 remote-as 300
    network 192.168.93.0 mask 255.255.255.252
    network 192.168.93.8 mask 255.255.255.252
    exit
``` 

# BMS0 - ISP3
```BASH
en
conf t
    hostname AS300
    ip routing
    interface gig 1/1/3
        no switchport
        ip address 192.168.93.6 255.255.255.252
        no shutdown
    exit
    interface gig 1/1/2
        no switchport
        ip address 192.168.93.10 255.255.255.252
        no shutdown
    exit

    router bgp 300
        redistribute eigrp 12 
        neighbor 192.168.93.5 remote-as 100
        neighbor 192.168.93.9 remote-as 200
        network 192.168.93.4 mask 255.255.255.252
        network 192.168.93.8 mask 255.255.255.252
    exit

``` 