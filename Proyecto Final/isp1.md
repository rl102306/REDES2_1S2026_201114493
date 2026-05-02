# Comandos
# R1
```bash
enable
conf t
    hostname ISP1_R1
    ip routing
   interface port-channel 1 
        no switchport      
        ip address 172.16.13.193 255.255.255.252 
        no shutdown         
    exit
    
    interface range Gig 1/0/1-2    
        no switchport    
        channel-protocol lacp   
        channel-group 1 mode active 
        no shutdown 
    exit
    interface port-channel 2    
        no switchport  
        ip address 172.16.13.197 255.255.255.252 
        no shutdown         
    exit
    
    interface range Gig 1/0/3-4      
        no switchport  
        channel-protocol lacp   
        channel-group 2 mode active  
        no shutdown
    exit
    interface gig 1/0/5
            no switchport
            ip address 172.16.13.209 255.255.255.252
            no shutdown
        exit
    router ospf 12
        network 172.16.13.192 0.0.0.3 area 0
        network 172.16.13.208 0.0.0.3 area 0
        network 172.16.13.196 0.0.0.3 area 0
    end
```
# R2
```bash
enable
conf t
    hostname ISP1_R2
    ip routing
    interface port-channel 2    
        no switchport  
        ip address 172.16.13.198 255.255.255.252 
        no shutdown         
    exit
    
    interface range Gig 1/0/3-4        
        no switchport
        channel-protocol lacp   
        channel-group 2 mode active  
        no shutdown
    exit

   interface gig 1/0/1
        no switchport
        ip address 172.16.13.201 255.255.255.252
        no shutdown
    exit

    interface gig 1/0/2
        no switchport
        ip address 172.16.13.205 255.255.255.252
        no shutdown
    exit

    router ospf 12
        network 172.16.13.196 0.0.0.3 area 0
        network 172.16.13.200 0.0.0.3 area 0
        network 172.16.13.204 0.0.0.3 area 0
    end
```

# R3
```bash
enable
conf t
    hostname ISP1_R3
    ip routing
    interface gig 0/1
        no switchport
        ip address 172.16.13.202 255.255.255.252
        no shutdown
    exit
    
    interface vlan 11
        ip address 172.16.13.1 255.255.255.192
        ip helper-address 172.16.23.130
        no shutdown
    exit
    interface range  fa0/1-2
        switchport mode access
        switchport access vlan 11
    exit

    router ospf 12
        network 172.16.13.200 0.0.0.3 area 0
        network 172.16.13.0 0.0.0.63 area 0
    end

```
# R4
```bash
enable
conf t
    hostname ISP1_R4
    ip routing
    interface gig 0/2
        no switchport
        ip address 172.16.13.206 255.255.255.252
        no shutdown
    exit

    interface vlan 12
        ip address 172.16.13.65 255.255.255.192
        ip helper-address 172.16.23.130
        no shutdown
    exit
    interface range  fa0/1-2
        switchport mode access
        switchport access vlan 12
    exit
    router ospf 12
        network 172.16.13.204 0.0.0.3 area 0
        network 172.16.13.64 0.0.0.63 area 0

    end


```

# R5
```bash
enable
conf t
    hostname ISP1_R5
    ip routing
    interface port-channel 1    
        no switchport  
        ip address 172.16.13.194 255.255.255.252 
        no shutdown         
    exit
    
    interface range Gig 1/0/1-2        
        no switchport
        channel-protocol lacp   
        channel-group 1 mode active  
        no shutdown
    exit

    interface vlan 13
        ip address 172.16.13.129 255.255.255.192
        ip helper-address 172.16.23.130
        no shutdown
    exit
    interface gig 1/0/3
        switchport mode access
        switchport access vlan 13
        no shutdown
    exit
    
    router ospf 12
        network 172.16.13.192 0.0.0.3 area 0
        network 172.16.13.128 0.0.0.63 area 0
    end
```

