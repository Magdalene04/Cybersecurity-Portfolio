# Defensive Security Tooling: CyberChef-The Basics
CyberChef is a simple, intuitive web-based application designed to help with various “cyber” operation tasks within your web browser. Think of it as a Swiss Army knife for data - like having a toolbox of different tools designed to do a specific task. These tasks range from simple encodings like XOR or Base64 to complex operations like AES encryption or RSA decryption. CyberChef operates on recipes, a series of operations executed in order.

## Accessing the Tool
We can access the tool in both online and offline mode. For online, we can open Cyberchef in the browser itself. As for offline mode, we can download the latest version for stability in both Windows and Linux operating systems.

## Navigating the Interface
CyberChef consists of four areas. Each consists of different components or features.

These are the following areas:

**a)** Operations <br>
**b)** Recipe <br>
**c)** Input <br>
**d)** Output <br>

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

### Recipe Area
This is considered as the heart of the tool. In this area, we can select, arrange, and fine-tune operations to suit our needs. This is where we can take control, defining each operation's arguments and options precisely to our needs. 

It is a designated space to select and arrange specific operations and then define their respective arguments and options to customize their behaviour further. In the recipe area, we can drag the operations we want to use and specify arguments and options.

Features include the following:

* **Save recipe:** This feature allows the user to save selected operations.
* **Load recipe:** Allows the user to load previously saved recipes.
* **Clear Recipe:** This feature will enable users to clear the chosen recipe during usage.

After we are done with recipe we can click the *Bake* button to confirm the operation. We can also select *Auto Bake* to automatically cook with the recipe instead of manually choosing everytime.

### Input Area
The input area provides a user-friendly space where we can easily input text or files by pasting, typing, or dragging them to perform operations.

Additionally, it has the following features:

* **Add a new input tab:** This is where an additional tab is created for the user to use different values from the previous tab.
* **Open folder as input:** This feature allows users to upload a whole folder as input value.
* **Open file as input:** This feature allows the user to upload a file as its input value.
* **Clear input and output:** This feature allows the user to clear any input values inserted and the corresponding output value.
* **Reset pane layout:** This feature brings the tool's interface to its default window sizes.

### Output Area
The output area is a visual space that showcases the data processing results. It neatly presents the outcomes of any manipulations or transformations we have applied to the input data, allowing for a clear and intuitive display of the processed information.

Features include:

* **Save output to file:** This feature allows the users to save the result into a .dat file.
* **Copy raw output to the clipboard:** This feature allows users to copy raw output directly to their clipboard, allowing them to quickly copy the results for use in other applications or documents.
* **Replace input with output:** This feature allows users to quickly overwrite the input data based on the operations' results.
* **Maximise output pane:** This feature brings the tool's interface to its default window sizes.

#### Questions:
1) In which area can you find "From Base64"? <br>
**Ans:** Operations

2) Which area is considered the heart of the tool? <br>
**Ans:** Recipe

## Before Anything Else
Let's look at the thought process before using CyberChef

* **Step 1:** Set a clear objective.
* **Step 2:** Put the data into the input area.
* **Step 3:** Select the operations we need to use.
* **Step 4:** Check the output to see if it is the intended result. If not repeat the steps from 1 to 3.

Example scenario for each steps: <br>
Let's say that, we have found a gibberish sentence during a security investigation and we want to know what it is.

* **Step 1:** During the security investigation, I found a gibberish string and want to know what that means if it has any meaning.
* **Step 2:** Paste or upload the gibberish string that we found.
* **Step 3:** Determine through research to see what operation to use, to find what the gibberish string is. Eg: Operations such as ROT13, Base64, Base85, ROT47
* **Step 4:** Were we able to find the message behind the gibberish string? If yes, no more actions to do. If no, continue working with various operations.

#### Questions:
1) At which step would you determine, "What do I want to accomplish? <br>
**Ans:** 1

## Practice, Practice, Practice
More options on operations in detail.

### Extractors
Extractors extract IP addresses, Domain Names and URL's.

* The **Extract IP addresses** will extract any valid IPv4/6 address from any given input. 
* The **Extract email addresses** extracts any strings and characters with this format, anything@domain[.]com. Examples of domains include hotmail.com, google.com
* **Extract URLs** extracts Uniform Resource Locator, commonly known as URL. , a URL is the address used to access resources on the internet.

### Date and Time
This operation is based on date and time to set an operation or convert it into another format. 

A UNIX timestamp is a 32-bit value representing the number of seconds since January 1, 1970 UTC (the UNIX epoch). To convert **"Fri Sep 6 20:30:22 +04 2024"** into a UNIX Timestamp, use the operations **To UNIX Timestamp**, where the result would be **1725654622**. If you wish to convert it back to a more readable format, you can use **From UNIX Timestamp**.

### Data Format
The specific data formts are listed in the table below

| Operations | Description | Examples |
| --- | --- | --- |
| **From Base64** | This operation decodes data from an ASCII Base64 string back into its raw format. | `V2VsY29tZSB0byB0cnloYWNrbWUh` becomes `Welcome to tryhackme!` |
| **URL Decode** | Converts URI/URL percent-encoded characters back to their raw values. | `https%3A%2F%2Fgchq%2Egithub%2Eio%2FCyberChef%2F` becomes `https://gchq.github.io/CyberChef/` |
| **From Base85** | Notation for encoding arbitrary byte data. It is usually more efficient than Base64. This operation decodes data from an ASCII string (with an alphabet of your choosing, presets included). | `BOu!rD]j7BEbo7` becomes `hello world` |
| **From Base58** | Is a notation for encoding arbitrary byte data. It differs from Base64 by removing efficiently misread characters (i.e. l, I, 0, and O) to improve human readability. | `AXLU7qR` becomes `Thm58` |
| **To Base62** | Is a notation for encoding arbitrary byte data using a restricted set of symbols that humans can conveniently use and process by computers. The high number base results in shorter strings than with the decimal or hexadecimal system. | `Thm62` becomes `6NiRkOY` |

#### Questions:
1) What is the hidden email address? <br>
**Ans:** hidden@hotmail.com

<img width="1916" height="633" alt="image" src="https://github.com/user-attachments/assets/5d241a77-2ac7-4509-8609-640248d77b8f" />

2) What is the hidden IP address that ends in .232? <br>
**Ans:** 102.20.11.232

<img width="1919" height="642" alt="image" src="https://github.com/user-attachments/assets/9bb9ea59-114b-4dd7-8b57-03368c9bffce" />

3) Which domain address starts with 'T'? <br>
**Ans:** TryHackMe.com

<img width="1919" height="658" alt="image" src="https://github.com/user-attachments/assets/a4d77bcc-342d-4918-a586-d69ba73064c6" />

4) What is the binary value of the decimal number 78? <br>
**Ans:** 01001110

<img width="1919" height="668" alt="image" src="https://github.com/user-attachments/assets/913dc612-81c7-4f72-a34f-a33dea057c2a" />

5) What is the URL encoded value of https://tryhackme.com/r/careers? <br>
**Ans:** https%3A%2F%2Ftryhackme%2Ecom%2Fr%2Fcareers

<img width="1919" height="652" alt="image" src="https://github.com/user-attachments/assets/8ec09cfe-33b8-4c07-a5d0-ef0ab3d01ab4" />

## Your First Official Cook
#### Questions:
1) Using the file you downloaded in Task 5, which IP starts and ends with "10"? <br>
**Ans:** 10.10.2.10

<img width="1919" height="623" alt="image" src="https://github.com/user-attachments/assets/54f7c20a-50a9-4060-835c-d9f82e0fb580" />

2) What is the base64 encoded value of the string "Nice Room!"? <br>
**Ans:** TmljZSBSb29tIQ==

<img width="1919" height="593" alt="image" src="https://github.com/user-attachments/assets/8196ee05-a249-4d7c-8875-b7c2210dabb0" />

3) What is the URL decoded value for https%3A%2F%2Ftryhackme%2Ecom%2Fr%2Froom%2Fcyberchefbasics? <br>
**Ans:** https://tryhackme.com/r/room/cyberchefbasics

<img width="1919" height="611" alt="image" src="https://github.com/user-attachments/assets/c330a005-dd68-40e1-844f-f747d0fd3e9e" />

4) What is the datetime string for the Unix timestamp 1725151258? <br>
**Ans:** Sun 1 September 2024 00:40:58 UTC

<img width="1919" height="623" alt="image" src="https://github.com/user-attachments/assets/3c5ab7c9-fc23-41c0-994f-109da26234ef" />

5)  What is the Base85 decoded string of the value <+oue+DGm>Ap%u7? <br>
**Ans:** This is fun!

<img width="1919" height="647" alt="image" src="https://github.com/user-attachments/assets/f5e90b31-3506-421e-ba9d-a6778c26d2af" />

## Conclusion

Through this room, I learned the core concepts of web data formats and encoding methods that are commonly used in cyber security operations. By working through the hands-on exercises, I took notes on how to effectively utilize CyberChef to manipulate, decode, and analyze various data structures like Base64, URL encoding, Base58, Base62, and Base85. Mastering these conversion techniques gives me a solid foundation for analyzing obfuscated scripts, decoding network traffic, and working with defensive security tools in the future.
