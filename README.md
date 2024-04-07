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
[Ep 018: Introduction to Floating-Point Binary and IEEE-754 Notation](https://www.youtube.com/watch?v=bFLchKMm6YA) <br />
[Understanding and Using Floating Point Numbers](https://www.cprogramming.com/tutorial/floating_point/understanding_floating_point.html) <br />
[Floating point number representation](https://www.cprogramming.com/tutorial/floating_point/understanding_floating_point_representation.html) <br />
[Printing floating point numbers](https://www.cprogramming.com/tutorial/floating_point/understanding_floating_point_printing.html) <br />
[Introduction to Fixed Point Number Representation](https://inst.eecs.berkeley.edu/~cs61c/sp06/handout/fixedpt.html) <br />
[Floating Point Numbers - Computerphile](https://www.youtube.com/watch?v=PZRI1IfStY0) <br />

## Concepts

| Task | Prototype | Description |
|:----|:-----:|:--------|
| **TCP** |  | |
| **IP** | | |
| **local IP address** | `ipconfig getifaddr en0` | Using the terminal command line, reveal your local IP address. |
| **IP address size** | `128 - 64 - 32 - 16 - 8 - 4 - 2 - 1 => convert from binary to decimal` `11000000.10101000.00000001.00010101 = 192.168.1.21` | 4 bytes = 32 bits, each octet 8 bits, size of an IP address. Lowest level of storage in a computer. |
| **Subnet mask** | | It tells how big the network is. `255` = the corresponding octet is frozen, it won't change. Convert 255 into binary, will turn every bit on `255.255.255.0 = 11111111.11111111.11111111.00000000`. The octets made by 1s are the network bits, they won't change. The zeros are the host bits. It also tells how many hosts there are in the network. |
| **Formula to discover how many hosts** | `2` | |
