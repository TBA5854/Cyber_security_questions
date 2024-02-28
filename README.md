# Problem 1 : Wireshark
## Intro :
Given is a Wireshark Capture File .
## Tools Used: 
Wireshark, Termux , Termux-x11
## Analysis:

<p align="center" width="100%">
    <img src="https://github.com/TBA5854/Cyber_security_questions/blob/main/resources/PurpleBlock.jpg?raw=true">
</p>

In this screenshot (packets 6,8,10,12), we can see the user is logging into a ftp server with the following credentials:  

USERNAME="0ffs3cUs3r3"  
PASSWORD="very_secret_password"  

FTP protocol is considered unsafe due to it transferring data without encryption leading to sniffing attacks. Hence ftps is preferred.

<p align="center" width="100%">
    <img src="https://github.com/TBA5854/Cyber_security_questions/blob/main/resources/GreenBlock.jpg?raw=true">
</p>

In packet 24, the user is downloading a JPEG file(flag.jpg) through the HTTP protocol. From the packets 25 to 29, we can see that packets of data are being transmitted and are finally reassembled in packet 30. The transfer takes place using HTTP , which is also a unsafe and data can be exported simply without any hassle using wireshark itself.

(side_note : we can just download the image from the given ip , but it was a lan ip hence we can't download it as we are not in the same lan)

<p align="center" width="100%">
    <img src="https://github.com/TBA5854/Cyber_security_questions/blob/main/resources/pcap_flag.jpg?raw=true">
</p>
## Steps Taken:

1. apt install wireshark-qt.
2. Looking for hidden data in the .pcap file by opening in wireshark .
3. Finding flag.jpg and exporting it as HTTP object (File -> show data -> it displays the file).
# Problem 2 - Spectrum

## Intro :
Given is a .wav file that doesn't contain only sound hinting at something irrelevant to the given sound .
## Tools used:
Spectrum Analyzer:

https://academo.org/demos/spectrum-analyzer/

## Analysis:
Upon uploading the sound.wav file, we can see its spectrum containing the flag on the website.

video of flag :

<p align="center" width="100%">
    <a href="https://github.com/TBA5854/Cyber_security_questions/blob/main/resources/spectrum.mp4"> Spectrum.mp4 </a>
</p>

By playing the audio completely, we can get the contents of flag.  

flag: e5353bb7b57578bd4da1c898a8e2d767  

The flag looks like a MD5 Hash and could be brute forced using hashcat or Jacktheripper .

## Steps Taken:
1. Opening the sound.wav on Spectrum Analyzer.
2. Noting down the flag.

# Problem 3 - hexdump
## Intro :
Given is an encrypted text file which contains whitespace characters.
## Tools Used: 
xxd , python3 , Binary Text to ASCII (https://www.rapidtables.com/convert/number/binary-to-ascii.html)
## Analysis:
Viewing the file in xxd , we can see that there are **two** characters - 09(tab) and 20(space).


<p align="center" width="100%">
    <img src="https://github.com/TBA5854/Cyber_security_questions/blob/main/resources/xxd.jpg?raw=true">
</p>

Replacing spaces with 0 and tabs with 1 using we get something that looks like this:
<p align="center" width="100%">
    <img src="https://github.com/TBA5854/Cyber_security_questions/blob/main/resources/py.jpg?raw=true">
</p>
Grouping 8 bits of Binary for utf-8 encoding and running this through a Binary to Text Translator, we took the flag:
<p align="center" width="100%">
    <img src="https://github.com/TBA5854/Cyber_security_questions/blob/main/resources/conversion.jpg?raw=true">
</p>  

## Steps Taken:
1. Replacing space with 0 and tabs with 1 using python3 (read binary->replace tab with 1 and space with 0).
2. Grouping 8 bits of Binary and delimiting them with spaces.
3. Running them through a Binary to Text Translator and capturing the flag.

flag : csi{not_all_spaces_are_born_the_same}