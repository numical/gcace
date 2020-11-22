# Port Numbers
| port | protocol |
| --- | --- |
| 22 | SSH |
| 80 | HTTP |
| 443 | HTTPS |

#  CIDR
## Theory
* classless interdomain routing
* group of ip addresses
* <IP>/xy notation
* to understand
    * ip > 32 bit binary number: 10.10.0.254 > 00001010 00001010 00000000 11111110
    * then lock the first xy bits
* 0.0.0.0/0 = any IP address
* equivalent subnet mask
    * /16 > 255.255.0.0
    * /24 > 255.255.255.0
* google subnets
    * google reserves 4 ip addresses in every subnet
    * hence /29 goes from 2^3 = 8 - 4 = 4

## RFC 1918
* defines private address ranges:
* 10.0.0.0/8 > 16.8M addresses
* 172.16.0.0/12 > 1M addresses
* 192.168.0.0/16 > 65k addresses
    
# Address Classes
* A 8/24
    * 127 networks, 16M computers
    * 0.xxx > 127.xxx
    * first bits: 0
    * private subnet
      * range 10.0.0.0
      * mask 255.0.0.0
* B 16/16
    * 16k networks, 65k computers
    * 128.0.xxx > 191.255.xxx
    * first bits: 10
    * private subnet
      * range 172.16.0.0
      * mask 255.255.0.0
* C 24/8  
    * 2M networks, 255 computers   
    * 192.0.0.xxx > 223.255.255.xxx
    * first bits: 110
    * private subnet
      * range 192.168.0.0
      * mask 255.255.255.0

 
