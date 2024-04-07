# Net_Practice
This project was developed for 42 school. For comprehensive information regarding the requirements, please consult the PDF file in the subject folder of the repository. Furthermore, I have provided my notes and a concise summary below.

```diff
+ keywords: how TCP/IP addressing works
+ subnetting (network/host)
```

## High-level Overview

- C++11 (and derived forms) and Boost libraries are forbidden. The following functions are forbidden too: *printf(), *alloc() and free(). If you use them, your grade will be 0 and that’s it.

### References
[Subnet](https://en.wikipedia.org/wiki/Subnet) <br />

## Concepts

| Task | Prototype | Description |
|:----|:-----:|:--------|
| **TCP** |  | |
| **IP** | | |
| **local IP address** | `ipconfig getifaddr en0` | Using the terminal command line, reveal your local IP address. |
| **IP address size** | `128 - 64 - 32 - 16 - 8 - 4 - 2 - 1 => convert from binary to decimal` `11000000.10101000.00000001.00010101 = 192.168.1.21` | 4 bytes = 32 bits, each octet 8 bits, size of an IP address. Lowest level of storage in a computer. |
| **Subnetting** | | Change the subnet mask to suit your needs. |
| **Subnet mask** | | **It tells how big the network is.** `255` = the corresponding octet is frozen, it won't change. Convert 255 into binary, will turn every bit on `255.255.255.0 = 11111111.11111111.11111111.00000000`. The octets made by 1s are the network bits, they won't change. The zeros are the host bits. It also tells how many hosts there are in the network. The numbers are contiguous, always a row of 1s and 0s. |
| **Formula to discover how many hosts** | $2^n$ `where n is the number of zeros` | 8 zeros, give me 256 possible hosts, from wich I must subtract 2 (subnet ID/address and the broadcast address. first and last IP address in the network). Total 254 usable IP addresses. If I need more hosts than that, I must steal from network bits... |
| **Break one network into smaller networks** | `256 - 128 - 64 - 32 - 16 - 8 - 4 - 2 = discover how many bits do you need for creating networks. e.g. 4 networks demand 2 bits` | When you need more network, you need more bits (still them from host bits). E.g. how many host bits do you need for creating four networks? |
| **CIDR notation** | `192.168. 1.0/22` |  This means that the first 22 bits of the IP address are reserved for network routing. Counting all the network bits in our mask. |
| **Increment** | 11111111.11111111.11111111.1**1**000000 `64 is the increment` | Last network bit we have. We use it to determin the size of a network and its range. ![image](https://github.com/shinckel/net_practice/assets/115558344/f1009e8f-548f-440a-be40-bac892f44f83) |

