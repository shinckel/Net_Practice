# Net_Practice
This project was developed for 42 school. For comprehensive information regarding the requirements, please consult the PDF file in the subject folder of the repository. Furthermore, I have provided my notes and a concise summary below.

```diff
+ keywords: how TCP/IP addressing works
+
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
| **Subnet mask** | | It tells how big the network is. `255` = the corresponding octet is frozen, it won't change. Convert 255 into binary, will turn every bit on `255.255.255.0 = 11111111.11111111.11111111.00000000`. The octets made by 1s are the network bits, they won't change. The zeros are the host bits. It also tells how many hosts there are in the network. |
| **Formula to discover how many hosts** | $2^n$ `where n is the number of zeros` | 8 zeros, give me 256 possible hosts, from wich I must subtract 2 (subnet ID/address and the broadcast address. first and last IP address in the network). Total 254 usable IP addresses. If I need more hosts than that, I must steal from network bits... |


