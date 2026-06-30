# Defensive Security Tooling: CyberChef-The Basics
CyberChef is a simple, intuitive web-based application designed to help with various “cyber” operation tasks within your web browser. Think of it as a Swiss Army knife for data - like having a toolbox of different tools designed to do a specific task. These tasks range from simple encodings like XOR or Base64 to complex operations like AES encryption or RSA decryption. CyberChef operates on recipes, a series of operations executed in order.

## Accessing the Tool
We can access the tool in both online and offline mode. For online, we can open Cyberchef in the browser itself. As for offline mode, we can download the latest version for stability in both Windows and Linux operating systems.

## Navigating the Interface
CyberChef consists of four areas. Each consists of different components or features.

These are the following areas:

**a)** Operations
**b)** Recipe
**c)** Input
**d)** Output

<img width="1919" height="912" alt="Screenshot 2026-06-30 153948" src="https://github.com/user-attachments/assets/5d1e4de5-ecfd-43a4-b724-3f8646970f77" />

### Operations Area
The operations area has a comprehensive repository to perform diverse cybersecurity tasks. Some of the examples are given below:

| Operations | Description | Examples |
| :--- | :--- | :--- |
| **From Morse Code** | Translates Morse Code into (upper case) alphanumeric characters. | `- .... .-. . .- - ...` becomes `THREATS` when used with default parameters. |
| **URL Encode** | Encodes problematic characters into percent-encoding, a format supported by URIs/URLs. | `https://tryhackme.com/r/room/cyberchefbasics` becomes `https%3A%2F%2Ftryhackme%2Ecom%2Fr%2Froom%2Fcyberchefbasics` when used with the parameter “Encode all special chars”. |
| **To Base64** | This operation encodes raw data into an ASCII Base64 string. | `This is fun!` becomes `VGhpcyBpcyBmdW4h`. |
| **To Hex** | Converts the input string to hexadecimal bytes separated by the specified delimiter. | `This Hex conversion is awesome!` becomes `54 68 69 73 20 48 65 78 20 63 6f 6e 76 65 72 73 69 6f 6e 20 69 73 20 61 77 65 73 6f 6d 65 21`. |
| **To Decimal** | Converts the input data to an ordinal integer array. | `This Decimal conversion is awesome!` becomes `84 104 105 115 32 68 101 99 105 109 97 108 32 99 111 110 118 101 114 115 105 111 110 32 105 115 32 97 119 101 115 111 109 101 33`. |
| **ROT13** | A simple Caesar substitution cipher which rotates alphabet characters by the specified amount (default 13). | `Digital Forensics and Incident Response` becomes `Qvtvgny Sberafvpf naq Vapvqrag Erfcbafr`. |

