# Net_Practice
This project was developed for 42 school. For comprehensive information regarding the requirements, please consult the PDF file in the subject folder of the repository. Furthermore, I have provided my notes and a concise summary below.

```diff
+ keywords: how TCP/IP addressing works
+ efficient allocation of address space is necessary
+ subnetting (network/host)
+ IPv4 (32 bits) - subnet mask (bitwise AND operation yields the routing prefix)
```

## High-level Overview
- Subnet: logical division of an IP network (dividing a network into two or more network is called subnetting) => network number or routing prefix, and the rest field or host identifier.
- The rest field is an identifier for a specific host or network interface.
- The routing prefix may be expressed as the first address of a network, written in Classless Inter-Domain Routing (CIDR) notation, followed by a slash character (/), and ending with the bit-length of the prefix.
- For example, 198.51.100.0/24 is the prefix of the Internet Protocol version 4 network starting at the given address, having 24 bits allocated for the network prefix, and the remaining 8 bits reserved for host addressing. Addresses in the range 198.51.100.0 to 198.51.100.255 belong to this network, with 198.51.100.255 as the subnet broadcast address.

1. Calculate how many host bits you need to hack;
2. Hack the host bits;
3. Find the increment;
4. Create your networks.

### References
[Subnet](https://en.wikipedia.org/wiki/Subnet) <br />
[Let’s subnet your home network // You SUCK at subnetting // EP 6](https://www.youtube.com/watch?v=mJ_5qeqGOaI&list=PLIhvC56v63IKrRHh3gvZZBAGvsvOhwrRF&index=6) <br />

## Concepts

| Task | Prototype | Description |
|:----|:-----:|:--------|
| **TCP** |  | |
| **IP** | | |
| **local IP address** | `ipconfig getifaddr en0` | Using the terminal command line, reveal your local IP address. |
| **IP address size** | `128 - 64 - 32 - 16 - 8 - 4 - 2 - 1 => convert from binary to decimal` `11000000.10101000.00000001.00010101 = 192.168.1.21` | 4 bytes = 32 bits, each octet 8 bits, size of an IP address. Lowest level of storage in a computer. |
| **Subnetting** | | Change the subnet mask to suit your needs. |
| **Subnet mask** | `bitwise AND operation` | **It tells how big the network is.** `255` = the corresponding octet is frozen, it won't change. Convert 255 into binary, will turn every bit on `255.255.255.0 = 11111111.11111111.11111111.00000000`. The octets made by 1s are the network bits, they won't change. The zeros are the host bits. It also tells how many hosts there are in the network. The numbers are contiguous, always a row of 1s and 0s. |
| **Formula to discover how many hosts** | $2^n$ `where n is the number of zeros, two to the power of host bits. Then, subtract 2.` | 8 zeros, give me 256 possible hosts, from wich I must subtract 2 (subnet ID/address and the broadcast address. first and last IP address in the network). Total 254 usable IP addresses. If I need more hosts than that, I must steal from network bits... |
| **Break one network into smaller networks** | `256 - 128 - 64 - 32 - 16 - 8 - 4 - 2 = discover how many bits do you need for creating networks. e.g. 4 networks demand 2 bits` | When you need more network, you need more bits (still them from host bits). E.g. how many host bits do you need for creating four networks? |
| **CIDR notation** | `192.168. 1.0/22` |  This means that the first 22 bits of the IP address are reserved for network routing. Counting all the network bits in our mask. |
| **Increment** | 11111111.11111111.11111111.1**1**000000 `64 is the increment` | Last network bit we have. We use it to determin the size of a network and its range. Each one of the networks below will have the subnet mask `255.255.255.192/26` ![image](https://github.com/shinckel/net_practice/assets/115558344/f1009e8f-548f-440a-be40-bac892f44f83) |
| **Traffic** | x | When the routing prefixes of the source address and the destination address differ. **A router serves as a logical or physical boundary between the subnets.** |

