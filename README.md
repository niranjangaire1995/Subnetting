IP ADDRESSING CLASSES FACTS:
- Classes were deprecated as CIDR system and VLSM were founded
- Class A range: 0.0.0.0 - 127.255.255.255 but usable range is 1.0.0.0 - 126.255.255.255
- CIDR for Class A : /8
- 127.0.0.0 range is reserved and used as loopback or local addressing
- 0.0.0.0 is also reserved
- Class B Range: 128.0.0.0 - 191.255.255.255
- Usable  Class B range: Usable is same as the range i.e., 128.0.0.0 - 191.255.255.255
- CIDR Class B is /16
- Class C Range: 192.0.0.0 - 223.255.255.255
- Usable Class C Range: is same as the range : -> 192.0.0.0 - 223.255.255.255
- CIDR Class C is : /24
- Class D Range: 224.0.0.0 - 239.255.255.255  -> It is not usable   -> Used by protocols like OSPF 
- Class E Range: 240.0.0.0 - 255.255.255.255  -> This is also not usable -> Experimental used for research -> Not used publicly
- Below are the Private IP classes with respective CIDR:
10.0.0.0/8
172.16.0.0/12
192.168.0.0/16

10.0.0.0/8 ← large enterprises           ->   “We expect growth → choose 10.0.0.0/8”

172.16.0.0/12 ← mid-size

192.168.0.0/16 ← small offices


Questions in my mind that is not clear yet.
- If NAT Translates my private ip into public ip, My router gets a public ip, are there not 4 billion routers in the world? Who is 4 billion ip enough for each router?



If the IP Address that a Hospital uses is 192.168.1.0 and we have 4 different departments i.e, IT, Finance, HR, Clinical

IT needs 10 hosts, Financce needs 10 pcs, HR needs 5 hosts, Clinical needs 50 hosts

NOTE: Always start from the bigger subnet and in out case it is clinical with 50 hosts
--------------------------------------------------------------------------------------------------------------------------------------------------------
CLINICAL
2^n-2 >= 50 
2^6 -2  = 62 which is bigger than 50     Note: We will use 52 addresses from 62 and 10 will be idle addresses of no use. 2 addresses from 52 includes broadcast and Network Address
Number we need is -> 6   -> we flip 6 bits in the 4th octet of the subnet -> we write subnet is binary and count from the right 

Note: If it was networks we needed, we would count from the left of the working subnet.

192.168.1.0 is from Class C so, CIDR /24 -> Subnet Mask -> 255.255.255.0 -> 11111111.11111111.11111111.00|000000  -> 11111111.11111111.11111111.11000000 -> 255.255.255.192 -> CIDR -> /26

Note: we count the one in the binary and that is our new CIDR for this subnet.

256-192 = 64 hosts -> we add 64 in the last octet of the starting Network addresss -> 192.168.1.0+64 -> 192.168.1.64 -> This the network address for next subnet

The ip range of the clinical is 192.168.1.0/26 - 192.168.1.63/26  -> the CIDR used here is /26
-> first usable is 192.168.1.1/26 and broadcast is 192.168.1.63/26
-------------------------------------------------------------------------------------------------------------------------------------------------------------------

Number of hosts for IT is 10, 2^n-2 ->  2^4-2 >= 10 

subnet binary for 192.168.1.64/26 ->  11111111.11111111.11111111.11000000 -> count 4 bits from left to right and flip it -> 11111111.11111111.11111111.1100|0000 -> CIDR /28 -> 255.255.255.240

256-240=16 -> we now add 16 to the network address to get next network address -> 192.168.1.64+16 -> 192.168.1.80

The ip range for the IT department is : 192.168.1.64/28 - 192.168.1.79/28 -> CIDR is /28 -> first usable is 192.168.1.65/28 and broadcast is 192.168.1.79/28
--------------------------------------------------------------------------------------------------------------------------------------------------------
Number of Hosts for finance 10. we flips 4 bits from subnet -> subnet becomes 255.255.255.240 -> 256-240 -> 16 
we add 16 to the network address -> 192.168.1.80-16 - > 192.168.1.96
The ip range is 192.168.1.80 - 192.168.1.95 -> cidr is /28
first ip is 192.168.1.81/28 and broadcast is 192.168.1.95/28
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------
We need 5 hosts for finance department.

n = 3 -> we flip 3 bits as we count right to left -> new cidr -> /29 -> subnet is -> 255.255.255.248
256-248 = 8  -> add 8 in the network address -> 192.168.1.96+8 -> 192.168.1.104

The ip range for finance department is : 192.168.1.96/29 - 192.168.1.103/29
First ip is 192.168.1.97/29 broadcast is 192.168.1.103/29 and cidr is /29

Ip's list : .97 .98 .99 .100. 101 .102 .103   -> needed 5 

BASIC ROUTER AND SWITCH COMMANDS:

config t -> hostname <anythin>
password setup: config t -> enable secret <password>
console password: config t -> line console 0 -> password <password> -> login -> exit



for ssh setup hostname is mandatory for a device and you need a domain name and it can be anything: 

config t -> username admin password password 123 -> ip domain-name example.com -> crypto key generate rsa -> choose a number and enter -> line vty 0 4 -> login local -> transport input ssh -> ext


















