# FHRP-CONFIGURATION
------------------

ISP
en
conf t
hostname ISP
int g0/2
ip add 8.8.8.1 255.255.255.0
no shut
exit
int g0/0
ip add 192.168.1.2 255.255.255.252
no shut
exit
int g0/0
ip add 192.168.1.5 255.255.255.252
no shut
exit

R1
en
conf t
hostname R1
int g0/0
ip add 192.168.1.1 255.255.255.252
no shut
exit
int g0/1
ip add 10.1.1.1 255.255.255.0
no shut
exit

R2
en 
conf t
int g0/0
ip add 192.168.1.6 255.255.255.252
no shut
exit
int g0/1
ip add 10.1.1.2 255.255.255.0
no shut
exit


ISP-OSPF
--------
en
conf t
router ospf 1
router-id 3.3.3.3
network 8.8.8.0 0.0.0.255 area 0
network 192.168.1.0 0.0.03 area 0
network 192.168.1.4 0.0.0.3 area 0
end

R1-OSPF
-------
en
conf t
router ospf 1
router-id 1.1.1.1
network 192.168.1.1 0.0.0.3 area 0
network 10.1.1.0 0.0.0.255 area 0
end

R2-OSPF
-------
en
conf t
router ospf 1
router-id 2.2.2.2
network 192.168.1.4 0.0.0.3 area 0
network 10.1.1.0 0.0.0.255 area 0
end


passive-interface
----------------
router ospf 1
passive-interface default
no passive-interface g0/0

HSRP Configuration R1
------------------
en
conf t
int g0/0
standby 10 ip 10.1.1.3
stnadby 10 priority 110
standby 10 premit
end


HSRP Configuration R2
------------------
en
conf t
int g0/0
standby 10 ip 10.1.1.3
end
![FHRP Lab](https://user-images.githubusercontent.com/106605770/178120819-95235edc-07c9-40bc-b20d-bfe794866f0d.png)
