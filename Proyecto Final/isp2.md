# Core
# AS200

```bASH
enable
    conf t
    hostname AS200
    no ip domain-lookup
    ip routing

    interface gigabitEthernet 1/0/1
        no switchport
        ip address 172.16.23.146 255.255.255.252
        no shutdown
    exit

    interface gigabitEthernet 1/0/2
        no switchport
        ip address 172.16.23.150 255.255.255.252
        no shutdown
    exit

    interface gigabitEthernet 1/0/3
        no switchport
        ip address 172.16.23.154 255.255.255.252
        no shutdown
    exit

    interface gigabitEthernet 1/0/4
        no switchport
        ip address 172.16.23.158 255.255.255.252
        no shutdown
    exit

    interface gigabitEthernet 1/0/5
        no switchport
        ip address 172.16.23.162 255.255.255.252
        no shutdown
    exit

    
    router ospf 1
        redistribute bgp 200 metric 100 subnets
        network 172.16.23.144 0.0.0.3 area 0
        network 172.16.23.148 0.0.0.3 area 0
        network 172.16.23.152 0.0.0.3 area 0
        network 172.16.23.156 0.0.0.3 area 0
        network 172.16.23.160 0.0.0.3 area 0
    exit
end
```

# R1
```bASH
enable
    conf t
    hostname RN_R0
    no ip domain-lookup
    ip routing
    spanning-tree mode rapid-pvst
    interface gigabitEthernet 0/0
        no shutdown
    exit
    interface gigabitEthernet 0/0.20
        encapsulation dot1q 20
        ip address 172.16.23.2 	255.255.255.192
        standby version 2
        standby 20 ip 172.16.23.1
        standby 20 priority 110
        standby 20 preempt
        ip helper-address 172.16.23.130
        no shutdown
    exit
    interface gigabitEthernet 0/0.21
        encapsulation dot1q 21
        ip address 172.16.23.66 255.255.255.192
        standby version 2
        standby 21 ip 172.16.23.65
        standby 21 priority 110
        standby 21 preempt
        ip helper-address 172.16.23.130
        no shutdown
    exit
    interface gigabitEthernet 0/0.99
        encapsulation dot1q 99
        ip address 172.16.23.131 255.255.255.240
        standby version 2
        standby 99 ip 172.16.23.129
        standby 99 priority 110
        standby 99 preempt
        no shutdown
    exit
    interface gigabitEthernet 0/1
        ip address 172.16.23.145 255.255.255.252
        no shutdown
    exit
    router ospf 1
        network 172.16.23.0  0.0.0.63 area 0
        network 172.16.23.64 0.0.0.63 area 0
        network 172.16.23.128 0.0.0.15 area 0
        network 172.16.23.144 0.0.0.3 area 0
    exit
end
```
# R1
```bASH
enable
    conf t
    hostname RN_R1
    no ip domain-lookup
    ip routing
    interface gigabitEthernet 0/0
        no shutdown
    exit
    interface gigabitEthernet 0/0.20
        encapsulation dot1q 20
        ip address 172.16.23.3 255.255.255.192
        standby version 2
        standby 20 ip 172.16.23.1
        standby 20 priority 100
        standby 20 preempt
        ip helper-address 172.16.23.130
        no shutdown
    exit

    interface gigabitEthernet 0/0.21
        encapsulation dot1q 21
        ip address 172.16.23.67 255.255.255.192
        standby version 2
        standby 21 ip 172.16.23.65
        standby 21 priority 100
        standby 21 preempt
        ip helper-address 172.16.23.130
        no shutdown
    exit

    interface gigabitEthernet 0/0.99
        encapsulation dot1q 99
        ip address 172.16.23.132 255.255.255.240
        standby version 2
        standby 99 ip 172.16.23.129
        standby 99 priority 100
        standby 99 preempt
        no shutdown
    exit

    ! =============== OSPF CONFIGURATION ===============
    interface gigabitEthernet 0/1
        ip address 172.16.23.149 255.255.255.252
        no shutdown
    exit

    router ospf 1
        network 172.16.23.0  0.0.0.63 area 0
        network 172.16.23.64 0.0.0.63 area 0
        network 172.16.23.128 0.0.0.15 area 0
        network 172.16.23.148 0.0.0.3 area 0
    exit
end
```

# R2
```bASH
enable
    conf t
    hostname RN_R2
    no ip domain-lookup
    ip routing
    interface gigabitEthernet 0/0
        no shutdown
    exit
    interface gigabitEthernet 0/0.20
        encapsulation dot1q 20
        ip address 172.16.23.4 255.255.255.192
        standby version 2
        standby 20 ip 172.16.23.1
        standby 20 priority 90
        standby 20 preempt
        ip helper-address 172.16.23.130
        no shutdown
    exit
    interface gigabitEthernet 0/0.21
        encapsulation dot1q 21
        ip address 172.16.23.68 255.255.255.192
        standby version 2
        standby 21 ip 172.16.23.65
        standby 21 priority 90
        standby 21 preempt
        ip helper-address 172.16.23.130
        no shutdown
    exit
    interface gigabitEthernet 0/0.99
        encapsulation dot1q 99
        ip address 172.16.23.133 255.255.255.240
        standby version 2
        standby 99 ip 172.16.23.129
        standby 99 priority 90
        standby 99 preempt
        no shutdown
    exit
     interface gigabitEthernet 0/1
        ip address 172.16.23.153 255.255.255.252
        no shutdown
    exit
    router ospf 1
        network 172.16.23.0  0.0.0.63 area 0
        network 172.16.23.64 0.0.0.63 area 0
        network 172.16.23.128 0.0.0.15 area 0
        network 172.16.23.152 0.0.0.3 area 0
    exit
end
```
# R3
```bASH
enable
    conf t
    hostname RN_R3
    no ip domain-lookup
    ip routing
    interface gigabitEthernet 0/0
        no shutdown
    exit
    interface gigabitEthernet 0/0.20
        encapsulation dot1q 20
        ip address 172.16.23.5 255.255.255.192
        standby version 2
        standby 20 ip 172.16.23.1
        standby 20 priority 80
        standby 20 preempt
        ip helper-address 172.16.23.130
        no shutdown
    exit
    interface gigabitEthernet 0/0.21
        encapsulation dot1q 21
        ip address 172.16.23.69 255.255.255.192
        standby version 2
        standby 21 ip 172.16.23.65
        standby 21 priority 80
        standby 21 preempt
        ip helper-address 172.16.23.130
        no shutdown
    exit
    interface gigabitEthernet 0/0.99
        encapsulation dot1q 99
        ip address 172.16.23.134 255.255.255.240
        standby version 2
        standby 99 ip 172.16.23.129
        standby 99 priority 80
        standby 99 preempt
        no shutdown
    exit
    interface gigabitEthernet 0/1
        ip address 172.16.23.157 255.255.255.252
        no shutdown
    exit
    router ospf 1
        network 172.16.23.0  0.0.0.63 area 0
        network 172.16.23.64 0.0.0.63 area 0
        network 172.16.23.128 0.0.0.15 area 0
        network 172.16.23.156 0.0.0.3 area 0
    exit
end
```
# R4
```bASH
enable
    conf t
    hostname RN_R4
    no ip domain-lookup
    ip routing
    interface gigabitEthernet 0/0
        no shutdown
    exit
    interface gigabitEthernet 0/0.20
        encapsulation dot1q 20
        ip address 172.16.23.6 255.255.255.192
        standby version 2
        standby 20 ip 172.16.23.1
        standby 20 priority 70
        standby 20 preempt
        ip helper-address 172.16.23.130
        no shutdown
    exit
    interface gigabitEthernet 0/0.21
        encapsulation dot1q 21
        ip address 172.16.23.70 255.255.255.192
        standby version 2
        standby 21 ip 172.16.23.65
        standby 21 priority 70
        standby 21 preempt
        ip helper-address 172.16.23.130
        no shutdown
    exit
    interface gigabitEthernet 0/0.99
        encapsulation dot1q 99
        ip address 172.16.23.135 255.255.255.240
        standby version 2
        standby 99 ip 172.16.23.129
        standby 99 priority 70
        standby 99 preempt
        no shutdown
    exit
    interface gigabitEthernet 0/1
        ip address 172.16.23.161 255.255.255.252
        no shutdown
    exit
    router ospf 1
        network 172.16.23.0  0.0.0.63 area 0
        network 172.16.23.64 0.0.0.63 area 0
        network 172.16.23.128 0.0.0.15 area 0
        network 172.16.23.160 0.0.0.3 area 0
    exit
end
```

# dISTRIBUCION
# D1
```bASH
enable
conf t
    hostname RN_D1
    no ip domain-lookup
    vtp version 2
    vtp mode client
    vtp domain RN_VTP
    vtp password RN_VTP
    spanning-tree mode rapid-pvst
    spanning-tree vlan 20,21,99

    interface port-channel 1
        switchport trunk encapsulation dot1q
        switchport mode trunk
        switchport trunk allowed vlan 20,21,99
    exit

    interface range fastEthernet0/4-6
        switchport trunk encapsulation dot1q
        switchport mode trunk
        switchport trunk allowed vlan 20,21,99
        channel-protocol lacp
        channel-group 1 mode passive
        spanning-tree link-type point-to-point
        no spanning-tree portfast
    exit

    interface gigabitEthernet0/1
        switchport trunk encapsulation dot1q
        switchport mode trunk
        switchport trunk allowed vlan 20,21,99
    exit

    interface gigabitEthernet0/2
        switchport trunk encapsulation dot1q
        switchport mode trunk
        switchport trunk allowed vlan 20,21,99
    exit
    interface fastEthernet0/1
        switchport trunk encapsulation dot1q
        switchport mode trunk
        switchport trunk allowed vlan 20,21,99
    exit
    end
```
# R1
```bASH
enable
conf t
    hostname RN_D3
    no ip domain-lookup
    vtp version 2
    vtp mode client
    vtp domain RN_VTP
    vtp password RN_VTP
    spanning-tree mode rapid-pvst
    spanning-tree vlan 20,21,99

    interface port-channel 2
        switchport trunk encapsulation dot1q
        switchport mode trunk
        switchport trunk allowed vlan 20,21,99
    exit

    interface range fastEthernet0/1-3
        switchport trunk encapsulation dot1q
        switchport mode trunk
        switchport trunk allowed vlan 20,21,99
        channel-protocol lacp
        channel-group 2 mode passive
        spanning-tree link-type point-to-point
        no spanning-tree portfast
    exit

    interface gigabitEthernet0/1
        switchport trunk encapsulation dot1q
        switchport mode trunk
        switchport trunk allowed vlan 20,21,99
    exit
    interface gigabitEthernet0/2
        switchport trunk encapsulation dot1q
        switchport mode trunk
        switchport trunk allowed vlan 20,21,99
    exit
    interface fastEthernet0/24
        switchport trunk encapsulation dot1q
        switchport mode trunk
        switchport trunk allowed vlan 20,21,99
    exit
     interface fastEthernet0/5
        switchport trunk encapsulation dot1q
        switchport mode trunk
        switchport trunk allowed vlan 20,21,99
    exit
```
# R1
```bASH
enable
conf t
    hostname RN_D2
    no ip domain-lookup
    vtp version 2
    vtp mode server
    vtp domain RN_VTP
    vtp password RN_VTP
    vtp pruning
    spanning-tree mode rapid-pvst
    spanning-tree vlan 20,21,99 root primary
    vlan 20
        name VENTAS
    vlan 21
        name FACTURACION
    vlan 99
        name DHCP_RN

    interface port-channel 1
        switchport trunk encapsulation dot1q
        switchport mode trunk
        switchport trunk allowed vlan 20,21,99
    exit
    interface range fastEthernet0/4-6
        switchport trunk encapsulation dot1q
        switchport mode trunk
        switchport trunk allowed vlan 20,21,99
        channel-protocol lacp
        channel-group 1 mode active
        spanning-tree link-type point-to-point
        no spanning-tree portfast
    exit
    interface port-channel 2
        switchport trunk encapsulation dot1q
        switchport mode trunk
        switchport trunk allowed vlan 20,21,99
    exit
    interface range fastEthernet0/1-3
        switchport trunk encapsulation dot1q
        switchport mode trunk
        switchport trunk allowed vlan 20,21,99
        channel-protocol lacp
        channel-group 2 mode active
        spanning-tree link-type point-to-point
        no spanning-tree portfast
    exit
     interface fastEthernet0/7
        switchport trunk encapsulation dot1q
        switchport mode trunk
        switchport trunk allowed vlan 20,21,99
    exit
     interface fastEthernet0/9
        switchport trunk encapsulation dot1q
        switchport mode trunk
        switchport trunk allowed vlan 20,21,99
    exit
     interface fastEthernet0/11
        switchport trunk encapsulation dot1q
        switchport mode trunk
        switchport trunk allowed vlan 20,21,99
    exit
    end
```

# Acceso

# S0
```bASH
enable
conf t
    hostname RN_S2
    no ip domain-lookup
    vtp version 2
    vtp mode client
    vtp domain RN_VTP
    vtp password RN_VTP
    spanning-tree mode rapid-pvst
    spanning-tree extended system-id

    interface fastEthernet 0/11
        switchport mode trunk
        switchport trunk allowed vlan 20,21,99
    exit

    interface fastEthernet 0/4
        switchport mode access
        switchport access vlan 99
    exit
    end
```
# s1
```bASH
enable
conf t
    hostname RN_S0
    no ip domain-lookup
    vtp version 2
    vtp mode client
    vtp domain RN_VTP
    vtp password RN_VTP
    spanning-tree mode rapid-pvst
    spanning-tree extended system-id

    interface range fastEthernet 0/7-8
        switchport mode trunk
        switchport trunk allowed vlan 20,21,99
    exit

    interface fastEthernet 0/2
        switchport mode access
        switchport access vlan 20
    exit
   interface fastEthernet 0/3
        switchport mode access
        switchport access vlan 21
    exit
    end
```
# s2
```bASH
enable
conf t
    hostname RN_S3
    no ip domain-lookup
    vtp version 2
    vtp mode client
    vtp domain RN_VTP
    vtp password RN_VTP
    spanning-tree mode rapid-pvst
    spanning-tree extended system-id

    interface range fastEthernet 0/9-10
        switchport mode trunk
        switchport trunk allowed vlan 20,21,99
    exit

    interface fastEthernet 0/2
        switchport mode access
        switchport access vlan 20
    exit
   interface fastEthernet 0/3
        switchport mode access
        switchport access vlan 21
    exit
    end
```
