# OhSINT

## Step 1: Picture metadata

We get a picture called WindowsXP.jpg from the challenge. Looking at the metadata with an online exif viewer we get:

```
WindowsXP.jpg
File Metadata

File Type:   image/jpeg
Error:       0
Upload Size: 234081
exiftool:

Name	                          Value
ExifTool Version Number	          12.25
File Name	                  phpdYljN8
Directory	                  /tmp
File Size	                  229 KiB
File Modification Date/Time	  2025:07:01 14:11:03+00:00
File Access Date/Time	          2025:07:01 14:11:02+00:00
File Inode Change Date/Time	  2025:07:01 14:11:03+00:00
File Permissions	          -rw-------
File Type	                  JPEG
File Type Extension	          jpg
MIME Type	                  image/jpeg
XMP Toolkit	                  Image::ExifTool 11.27
GPS Latitude	                  54º 17' 41.27" N
GPS Longitude	                  2º 15' 1.33" W
Copyright	                  OWoodflint
Image Width	                  1920
Image Height	                  1080
Encoding Process	          Baseline DCT, Huffman coding
Bits Per Sample	                  8
Color Components	          3
Y Cb Cr Sub Sampling	          YCbCr4:2:0 (2 2)
Image Size	                  1920x1080
Megapixels	                  2.1
GPS Latitude Ref	          North
GPS Longitude Ref	          West
GPS Position	                  54º 17' 41.27" N, 2º 15' 1.33" W
```
We see the copyright is by OWoodflint.

## Step 2: Search for OWoodflint

Searching on google for OWoodflint gives us an X account [@OWoodflint](https://x.com/owoodflint) and a github account [OWoodfl1nt](https://github.com/OWoodfl1nt).

## Step 3: The X Account

On the X account, the users profile picture is a cat, so we can answer the question **What is this user's avatar of?** with **cat**.  
From the X account, we get the BSSID of the WAP the user is connected to: B4:5D:50:AA:86:41  
We can put it into [WiGLE](https://wigle.net/) and get the SSID **UnileverWiFi** to answer the question **What is the SSID of the WAP he connected to?**.

## Step 4: The GitHub Account

On there, we find the e-mail address **OWoodflint@gmail.com** in the people_finder repository to answer the question **What is his personal email address?**.  
The user states in his repo, that he is from **London** so we can answer **What city is this person in?**.  
Also in this repo, we can see that the user has a [blog](https://oliverwoodflint.wordpress.com/).

## Step 5: The Blog

Here, we can see that the user is currently in **New York** to answer the question **Where has he gone on holiday?**.  
Inspecting the source code of the blog (or using ctrl+a), we can see that he accidentally posted his password in white text: **pennYDr0pper.!**

