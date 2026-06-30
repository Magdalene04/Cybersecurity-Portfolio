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

