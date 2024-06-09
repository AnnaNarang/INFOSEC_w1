# WEEK 1
## CHALLENGE 1
### INFORMATION
####  Description:
Files can always be changed in a secret way. Can you find the flag?
#### Writeup:
I got no hind looking at the image, therefore used exiftool to get the metadata.
```shell
anna@anna:~/Downloads$ exiftool cat.jpg 
ExifTool Version Number         : 11.88
File Name                       : cat.jpg
Directory                       : .
File Size                       : 858 kB
File Modification Date/Time     : 2024:06:09 11:34:03+05:30
File Access Date/Time           : 2024:06:09 11:52:50+05:30
File Inode Change Date/Time     : 2024:06:09 11:52:45+05:30
File Permissions                : rw-rw-r--
File Type                       : JPEG
File Type Extension             : jpg
MIME Type                       : image/jpeg
JFIF Version                    : 1.02
Resolution Unit                 : None
X Resolution                    : 1
Y Resolution                    : 1
Current IPTC Digest             : 7a78f3d9cfb1ce42ab5a3aa30573d617
Copyright Notice                : PicoCTF
Application Record Version      : 4
XMP Toolkit                     : Image::ExifTool 10.80
License                         : cGljb0NURnt0aGVfbTN0YWRhdGFfMXNfbW9kaWZpZWR9
Rights                          : PicoCTF
Image Width                     : 2560
Image Height                    : 1598
Encoding Process                : Baseline DCT, Huffman coding
Bits Per Sample                 : 8
Color Components                : 3
Y Cb Cr Sub Sampling            : YCbCr4:2:0 (2 2)
Image Size                      : 2560x1598
Megapixels                      : 4.1
```
The license string looked like it was encoded.
Using base64, the decoded string gave the flag.
```shell
anna@anna:~/Downloads$ echo "cGljb0NURnt0aGVfbTN0YWRhdGFfMXNfbW9kaWZpZWR9"|base64 --decode
picoCTF{the_m3tadata_1s_modified}
```

