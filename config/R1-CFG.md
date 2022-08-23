```terminal
conf t
!
hostname R1     
!
interface GigabitEthernet0/0
 no shut
 description WAN Link
 ip address dhcp
 ip nat outside
!
interface GigabitEthernet0/1
 no shut
 description LAN Link
 ip address 10.1.1.1 255.255.255.0
 ip nat inside
!
ip nat inside source list 1 interface GigabitEthernet0/0 overload
!
access-list 1 permit any
!
!
end
```
