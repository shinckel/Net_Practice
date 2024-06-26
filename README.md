# Net_Practice
This project was developed for 42 school. For comprehensive information regarding the requirements, please consult the PDF file in the subject folder of the repository. Furthermore, I have provided my notes and a concise summary below.

```diff
+ keywords: how TCP/IP addressing works
+ efficient allocation of address space is necessary
+ subnetting (network -> how big, host -> how many)
+ IPv4 (32 bits) - subnet mask (bitwise AND operation yields the routing prefix)
```

## High-level Overview
- Subnet: logical division of an IP network (dividing a network into two or more network is called subnetting) => network number or routing prefix, and the rest field or host identifier.
- The rest field is an identifier for a specific host or network interface.
- The routing prefix may be expressed as the first address of a network, written in Classless Inter-Domain Routing (CIDR) notation, followed by a slash character (/), and ending with the bit-length of the prefix.
- For example, 198.51.100.0/24 is the prefix of the Internet Protocol version 4 network starting at the given address, having 24 bits allocated for the network prefix, and the remaining 8 bits reserved for host addressing. Addresses in the range 198.51.100.0 to 198.51.100.255 belong to this network, with 198.51.100.255 as the subnet broadcast address.

1. Calculate how many host bits you need to hack `255.255.255.0 = 11111111.11111111.11111111.00000000` `10.1.1.0`;
2. Save the host bits. How many do we need? `e.g. consider you have to find space for at least 40 hosts, 3 networks => 6 bits`;
   ![image](https://github.com/shinckel/net_practice/assets/115558344/e55eae12-7a94-4616-8d5a-1ac69cdb0cdf)
   ![image](https://github.com/shinckel/net_practice/assets/115558344/5aefcdde-5211-40ad-8722-cdef8c86d63e)
4. Find the increment = last network bit. It is used to create the network (how big they are, network ranges). `E.g. following the previous example it would be 64`;
5. Create your networks
   `10.1.1.0 - 10.1.1.63 /26 => it is 63 because we are couting zero` <br />
   `10.1.1.64 - 10.1.1.127 /26` <br />
   `10.1.1.128 - 10.1.1.191 /26` <br />
   `255.255.255.192 = 11111111.11111111.11111111.11000000`

### References
[Subnet](https://en.wikipedia.org/wiki/Subnet) <br />
[Let’s subnet your home network // You SUCK at subnetting // EP 6](https://www.youtube.com/watch?v=mJ_5qeqGOaI&list=PLIhvC56v63IKrRHh3gvZZBAGvsvOhwrRF&index=6) <br />
[Guide to NetPractice](https://github.com/lpaube/NetPractice) <br />
[Subnet Calculator](https://www.calculator.net/ip-subnet-calculator.html?cclass=any&csubnet=30&cip=192.168.36.222&ctype=ipv4&x=Calculate) <br />
[Internet Primer - CS50 Shorts](https://www.youtube.com/watch?v=04GztBlVo_s) <br />

## Concepts

| Task | Prototype | Description |
|:----|:-----:|:--------|
| **TCP** | `Transmission Control Protocol` | It is a communications standard that enables application programs and devices to exchange messages over a network. It is used to send packets across the internet. **Router => Go from A to B. TCP => What the data package is for, port number, chuncks of data, handling errors (e.g. browsing the web port 80, email port 25).** |
| **Router** | x | Give IP addresses for any connected device. Devices in the same network has the same network bits: is it the same network? Are we close? When network is too far from router, it needs help => `default gateway`. **Network Address Translation (NAT)** => router is the only public address. Therefore, all devices (private IP) will be connected to it and the router itself will translate and connect all devices to the internet. Routers constitute logical or physical borders between the subnets, and manage traffic between them. They also separate different networks. **The router has an interface for each network it connects to.** Router, a.k.a. access point. |
| **Routing Table** | `Destination: 0.0.0.0/0 (all possible destinations)` | the destination in a route specifies where outbound packets are intended to go, and the next hop indicates the next router or gateway to which these packets should be forwarded in order to reach their destination network. Routing tables use these route entries to determine how to forward packets efficiently across networks. Go from A (destination) to B (next-hop). **Route data to some next-hop, a.k.a. go to the next router.** |
| **IP** | `class A - B - C = how many octects for network and hosts` `home network = class C, less hosts per network` `class D - E = reserved for multicast experiments, people can't use it` | An address fulfills the functions of identifying the host and locating it on the network in destination routing. An IP address is divided into two logical parts, the network prefix and the host identifier. All hosts on a subnet have the same network prefix. **This addressing structure permits the selective routing of IP packets across multiple networks via special gateway computers, called routers, to a destination host if the network prefixes of origination and destination hosts differ, or sent directly to a target host on the local network if they are the same.** |
| **network switches** | x | Just as the switch connects multiple devices on a single network, the router connects multiple networks together. The router has an interface for each network it connects to. |
| **local IP address** | `ipconfig getifaddr en0` `ifconfig` | Using the terminal command line, reveal your local IP address. |
| **IP address size** | `128 - 64 - 32 - 16 - 8 - 4 - 2 - 1 => convert from binary to decimal` `11000000.10101000.00000001.00010101 = 192.168.1.21` | 4 bytes = 32 bits, each octet 8 bits, size of an IP address. Lowest level of storage in a computer. ![image](https://github.com/shinckel/net_practice/assets/115558344/35c75233-3501-462b-8afc-05fc5b500469) |
| **Subnetting** | `11111111.11111111.11111111.11000000`  | Change the subnet mask to suit your needs => esignating some high-order bits from the host part as part of the network prefix and adjusting the subnet mask appropriately. This divides a network into smaller subnets. ![image](https://github.com/shinckel/net_practice/assets/115558344/ba76c243-eef1-495a-b3bf-91b924a18ee7) |
| **Subnet mask** | `bitwise AND operation` | **It tells how big the network is.** `255` = the corresponding octet is frozen, it won't change. Convert 255 into binary, will turn every bit on `255.255.255.0 = 11111111.11111111.11111111.00000000`. The octets made by 1s are the network bits, they won't change. The zeros are the host bits. It also tells how many hosts there are in the network. The numbers are contiguous, always a row of 1s and 0s. ![image](https://github.com/shinckel/net_practice/assets/115558344/154e1d38-1358-4b7f-93ad-ecc32b726cb9) |
| **Formula to discover how many hosts** | $2^n - 2$ `where n is the number of zeros, two to the power of host bits. Then, subtract 2.` | 8 zeros, give me 256 possible hosts, from wich I must subtract 2 (subnet ID/address and the broadcast address. first and last IP address in the network... all-zeros versus all-ones). Total 254 usable IP addresses. If I need more hosts than that, I must steal from network bits... |
| **Break one network into smaller networks** | `256 - 128 - 64 - 32 - 16 - 8 - 4 - 2 => discover how many bits do you need for creating networks. e.g. 4 networks demand 2 bits` | When you need more network, you need more bits (still them from host bits). E.g. how many host bits do you need for creating four networks? |
| **CIDR notation** | `192.168. 1.0/22` |  This means that the first 22 bits of the IP address are reserved for network routing. It counts the number of bits in the prefix and appends that number to the address after a slash (/) character separator. E.g. IPv4 network `192.0.2.0` with the subnet mask `255.255.255.0` is written as `192.0.2.0/24`. IPv6 follows this standard too. |
| **Increment** | 11111111.11111111.11111111.1**1**000000 `64 is the increment` | Last network bit we have. We use it to determin the size of a network and its range. Each one of the networks below will have the subnet mask `255.255.255.192/26` ![image](https://github.com/shinckel/net_practice/assets/115558344/f1009e8f-548f-440a-be40-bac892f44f83) |
| **Traffic** | x | When the routing prefixes of the source address and the destination address differ. **A router serves as a logical or physical boundary between the subnets.** |
| **Broadcast** | | Last IP address from the network. E.g. network => `192.168.1.0` broadcast => `192.168.1.255` router => `192.168.1.1` (connect with public IP addresses outside of the network) |
| **Internet** | x | Interconnected network. Set of rules about how networks communicate to eachother. |
| **Domain Name System (DNS)** | `Yellow pages of the web` | DNS correlates IP address to human readable words. Mapping, translating IPs. |

## Exercises
<details>
<summary>Level 1</summary>
<img width="1171" alt="Screenshot 2024-04-17 at 21 54 02" src="https://github.com/shinckel/net_practice/assets/115558344/1b1d7f71-04b8-4963-8b1f-1b467729734a">
</details>

<details>
<summary>Level 2</summary>
<img width="1068" alt="Screenshot 2024-04-17 at 22 41 16" src="https://github.com/shinckel/net_practice/assets/115558344/00e3c5b1-c097-490a-bfeb-f24b8437959a">
</details>

<details>
<summary>Level 3</summary>
<img width="1095" alt="Screenshot 2024-04-17 at 22 42 31" src="https://github.com/shinckel/net_practice/assets/115558344/36a09fed-454e-448f-bcd9-892a584e2d73">
</details>

<details>
<summary>Level 4</summary>
<img width="1132" alt="Screenshot 2024-04-17 at 22 44 43" src="https://github.com/shinckel/net_practice/assets/115558344/7e8ea9d1-ed5d-49e0-b835-e29f89deefd1">
</details>

<details>
<summary>Level 5</summary>
<img width="1154" alt="Screenshot 2024-04-17 at 22 47 23" src="https://github.com/shinckel/net_practice/assets/115558344/2874f8e1-820d-4a4a-a9c5-d90d163af989">
</details>

<details>
<summary>Level 6</summary>
<img width="1221" alt="Screenshot 2024-04-17 at 22 52 21" src="https://github.com/shinckel/net_practice/assets/115558344/edcb046a-7315-4633-ac8f-e1b76299182e">
</details>

<details>
<summary>Level 7</summary>
<img width="1318" alt="Screenshot 2024-04-17 at 22 57 37" src="https://github.com/shinckel/net_practice/assets/115558344/4d3bf68b-0ab6-46d1-b795-272c10f9e082">
</details>

<details>
<summary>Level 8</summary>
<img width="1261" alt="Screenshot 2024-04-15 at 16 50 18" src="https://github.com/shinckel/net_practice/assets/115558344/3f7557c3-b7d4-4ae2-be13-9000e1f7238b">
</details>

<details>
<summary>Level 9</summary>
<img width="1082" alt="Screenshot 2024-04-15 at 17 56 45" src="https://github.com/shinckel/net_practice/assets/115558344/35f8571d-6a67-40db-b97f-ff9d98cda32a">
</details>

<details>
<summary>Level 10</summary>
<img width="1091" alt="Screenshot 2024-04-15 at 18 39 06" src="https://github.com/shinckel/net_practice/assets/115558344/d4c74123-f445-4ff9-ab36-54072aa1ed14">
</details>

