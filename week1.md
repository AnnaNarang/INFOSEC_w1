# WEEK 1
## CHALLENGE 1
### INFORMATION
#### 
I got no hint looking at the image, therefore used exiftool to get the metadata.
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
### MATRYOKSHA DOLL
####
I started by using exiftool which did not give me any hint as to how to procede. Next I used zsteg which revealed there was hidden data in the image, so I used binwalk to extract that data.
```shell
anna@anna:~/Downloads$ zsteg dolls.jpg 
[?] 379140 bytes of extra data after image end (IEND), offset = 0x4286c
extradata:0         .. file: Zip archive data, at least v2.0 to extract
    00000000: 50 4b 03 04 14 00 00 00  08 00 e2 02 70 52 48 16  |PK..........pRH.|
    00000010: 82 2d 48 c8 05 00 c1 db  05 00 13 00 1c 00 62 61  |.-H...........ba|
    00000020: 73 65 5f 69 6d 61 67 65  73 2f 32 5f 63 2e 6a 70  |se_images/2_c.jp|
    00000030: 67 55 54 09 00 03 68 fa  4f 60 68 fa 4f 60 75 78  |gUT...h.O`h.O`ux|
    00000040: 0b 00 01 04 00 00 00 00  04 00 00 00 00 ec fc 67  |...............g|
    00000050: 58 53 5f d7 2e 8e d2 a4  86 26 4a 27 40 40 10 90  |XS_......&J'@@..|
    00000060: 2e d2 42 13 10 50 8a 82  0a d2 8b 4a 93 de 12 3a  |..B..P.....J...:|
    00000070: 82 84 a2 14 01 11 81 d0  45 3a 2a bd 43 e8 28 bd  |........E:*.C.(.|
    00000080: 28 3d b4 04 10 08 a1 85  fe 4f fc 3d cf f3 be 7b  |(=.......O.=...{|
    00000090: bf fb ff ed 7c 38 e7 da  87 eb 0a 59 59 6b ce b1  |....|8.....YYk..|
    000000a0: d6 1c 73 8c 7b dc 63 ae  b1 56 f4 43 7d 2d 5a 6a  |..s.{.c..V.C}-Zj|
    000000b0: 76 6a 22 22 22 5a 1d 6d  0d 43 22 22 12 3a 22 22  |vj"""Z.m.C"".:""|
    000000c0: 32 43 4a 72 fc 9e 5e 41  48 3c 11 11 e0 85 a3 ba  |2CJr..^AH<......|
    000000d0: fa 43 1d 75 75 9e 87 9e  6e 2f 1d 5f bd 20 22 d2  |.C.uu...n/._. ".|
    000000e0: 8e 4e 49 a5 30 31 ea 63  0e 45 7d 78 7c d5 94 87  |.NI.01.c.E}x|...|
    000000f0: c4 f0 ae 5b ae 36 2d cf  8d 08 66 35 d5 62 1e 61  |...[.6-...f5.b.a|
meta XML:com.adobe.xmp.. text: "<x:xmpmeta xmlns:x=\"adobe:ns:meta/\" x:xmptk=\"XMP Core 5.4.0\">\n   <rdf:RDF xmlns:rdf=\"http://www.w3.org/1999/02/22-rdf-syntax-ns#\">\n      <rdf:Description rdf:about=\"\"\n            xmlns:exif=\"http://ns.adobe.com/exif/1.0/\">\n         <exif:PixelXDimension>594</exif:PixelXDimension>\n         <exif:UserComment>Screenshot</exif:UserComment>\n         <exif:PixelYDimension>1104</exif:PixelYDimension>\n      </rdf:Description>\n   </rdf:RDF>\n</x:xmpmeta>\n"
b1,rgba,lsb,xy      .. file: compacted data
b1,rgba,msb,xy      .. file: MPEG ADTS, AAC, v2 SSR, 64 kHz, stereo
b1,abgr,msb,xy      .. file: MPEG ADTS, AAC, v4 Main, 44.1 kHz, stereo+center+LFE
b2,r,lsb,xy         .. text: ["U" repeated 11 times]
b2,r,msb,xy         .. text: "_UUUUUUUUUUUUUek"
b2,rgb,lsb,xy       .. file: MPEG ADTS, AAC, v4 Main, 32 kHz, surround + LFE
b2,rgb,msb,xy       .. file: , OEM-ID "UUU\377\", Bytes/sector 32768, sectors/cluster 170, reserved sectors 27306, FATs 85, root entries 21845, sectors 65525 (volumes <=32 MB), Media descriptor 0xff, sectors/FAT 65535, sectors/track 4095, FAT (12 bit by descriptor)
b2,abgr,msb,xy      .. text: ["W" repeated 9 times]
b3,rgb,lsb,xy       .. file: very old 16-bit-int little-endian archive
b3,rgba,lsb,xy      .. file: very old 16-bit-int little-endian archive
b4,r,lsb,xy         .. text: "\"\"3333DDDUUUVffffwx"
b4,r,msb,xy         .. text: ["D" repeated 8 times]
b4,rgb,lsb,xy       .. text: "\"\"\"\"\"\"\"333333333333DDDDDDDDDUUUUUUUUUUVfffffffffffffwwwwx"
b4,rgb,msb,xy       .. text: "HDDDDDDD"
b4,rgba,lsb,xy      .. text: "\"/\"/\"/\"/\"/3?3?3?3?3?3?3?3?DODODODODODOU_U_U_U_U_U_U_fofofofofofofofofow"
b4,abgr,msb,xy      .. text: "ODODODODOD"
anna@anna:~/Downloads$ binwalk -e dolls.jpg 

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             PNG image, 594 x 1104, 8-bit/color RGBA, non-interlaced
3226          0xC9A           TIFF image data, big-endian, offset of first image directory: 8
272492        0x4286C         Zip archive data, at least v2.0 to extract, compressed size: 378952, uncompressed size: 383937, name: base_images/2_c.jpg
651610        0x9F15A         End of Zip archive, footer length: 22
```
I traversed to 2_c.jpg and used the same approach,taking hint from "placed inside another" which in turn led me to 3_c.jpg and 4_c.jpg. 
Finally, the extracted 4_c.jpg data contained the flag.
```shell
anna@anna:~/Downloads/_dolls.jpg.extracted/base_images/_2_c.jpg.extracted/base_images/_3_c.jpg.extracted/base_images/_4_c.jpg.extracted$ ls
136DA.zip  flag.txt
anna@anna:~/Downloads/_dolls.jpg.extracted/base_images/_2_c.jpg.extracted/base_images/_3_c.jpg.extracted/base_images/_4_c.jpg.extracted$ cat flag.txt 
picoCTF{96fac089316e094d41ea046900197662}
```
### tunn3l v1s10n
####
### MacroHard WeakEdge
#### Using exiftool, the metadat showed details of zip and using strings showed the file content had various paths one labelled hidden. therefore I used binwalk to extract the data. Traversing to the file hidden and displaying it showed a string. Using base 64, decoding gave the flag.
```shell
anna@anna:~/Downloads/_Forensics is fun.pptm.extracted/ppt/slideMasters$ ls
hidden  _rels  slideMaster1.xml
anna@anna:~/Downloads/_Forensics is fun.pptm.extracted/ppt/slideMasters$ cat hidden
Z m x h Z z o g c G l j b 0 N U R n t E M W R f d V 9 r b j B 3 X 3 B w d H N f c l 9 6 M X A 1 f Q
anna@anna:~/Downloads/_Forensics is fun.pptm.extracted/ppt/slideMasters$ echo 'ZmxhZzogcGljb0NURntEMWRfdV9rbjB3X3BwdHNfcl96MXA1f'|base64 --decode
flag: picoCTF{D1d_u_kn0w_ppts_r_z1p5}
```
### ENHANCE!
####
Using exiftool, I got the file type as SVG (scalable vector graphic). There was no other usefool metadata. 
Since SVG is XML based, I opened the file in a text editor, to analyze the markup.
On analyzing, the text portion of the contained the flag picoCTF{3nh4nc3d_aab729dd}

```svg
<text
       xml:space="preserve"
       style="font-style:normal;font-weight:normal;font-size:0.00352781px;line-height:1.25;font-family:sans-serif;letter-spacing:0px;word-spacing:0px;fill:#ffffff;fill-opacity:1;stroke:none;stroke-width:0.26458332;"
       x="107.43014"
       y="132.08501"
       id="text3723"><tspan
         sodipodi:role="line"
         x="107.43014"
         y="132.08501"
         style="font-size:0.00352781px;line-height:1.25;fill:#ffffff;stroke-width:0.26458332;"
         id="tspan3748">p </tspan><tspan
         sodipodi:role="line"
         x="107.43014"
         y="132.08942"
         style="font-size:0.00352781px;line-height:1.25;fill:#ffffff;stroke-width:0.26458332;"
         id="tspan3754">i </tspan><tspan
         sodipodi:role="line"
         x="107.43014"
         y="132.09383"
         style="font-size:0.00352781px;line-height:1.25;fill:#ffffff;stroke-width:0.26458332;"
         id="tspan3756">c </tspan><tspan
         sodipodi:role="line"
         x="107.43014"
         y="132.09824"
         style="font-size:0.00352781px;line-height:1.25;fill:#ffffff;stroke-width:0.26458332;"
         id="tspan3758">o </tspan><tspan
         sodipodi:role="line"
         x="107.43014"
         y="132.10265"
         style="font-size:0.00352781px;line-height:1.25;fill:#ffffff;stroke-width:0.26458332;"
         id="tspan3760">C </tspan><tspan
         sodipodi:role="line"
         x="107.43014"
         y="132.10706"
         style="font-size:0.00352781px;line-height:1.25;fill:#ffffff;stroke-width:0.26458332;"
         id="tspan3762">T </tspan><tspan
         sodipodi:role="line"
         x="107.43014"
         y="132.11147"
         style="font-size:0.00352781px;line-height:1.25;fill:#ffffff;stroke-width:0.26458332;"
         id="tspan3764">F { 3 n h 4 n </tspan><tspan
         sodipodi:role="line"
         x="107.43014"
         y="132.11588"
         style="font-size:0.00352781px;line-height:1.25;fill:#ffffff;stroke-width:0.26458332;"
         id="tspan3752">c 3 d _ a a b 7 2 9 d d }</tspan></text>
  </g>
```
### Hideme
#### 
The file was a png. Using zsteg on the image, it showed it contained hidden data, which I extracted using binwalk.
The extracted file contained a directory secret which in turn contained another png image which gave the flag: picoCTF{Hiddinng_An_imag3_within_@n_ima9e_96539bea}
``` shell
anna@anna:~/Downloads$ cd _flag.png.extracted/
anna@anna:~/Downloads/_flag.png.extracted$ ls
29  29.zlib  9B3B.zip  secret
anna@anna:~/Downloads/_flag.png.extracted$ cd secret
anna@anna:~/Downloads/_flag.png.extracted/secret$ ls
flag.png
anna@anna:~/Downloads/_flag.png.extracted/secret$ file flag.png
flag.png: PNG image data, 600 x 50, 16-bit grayscale, non-interlaced
anna@anna:~/Downloads/_flag.png.extracted/secret$ display flag.png 
```
### MSB
####
I downloaded the image and put it through online steg tool, using maximum bit to extract data taking hint from challenge name.
The extracted data was an eBook which contained the flag that I extracted using grep command.
```shell
anna@anna:~/Downloads$ cat Ninja-and-Prince-Genji-Ukiyoe-Utagawa-Kunisadaflag.dat |grep pico
picoCTF{15_y0ur_que57_qu1x071c_0r_h3r01c_ee3cb4d8}
```
### Extensions
####
Using file command, I got to know that this was a png file but with extension txt.
On correcting the extension and displaying the image flag was obtained.
picoCTF{now_you_know_about_extensions}

```shell
anna@anna:~/Downloads$ file flag.txt
flag.txt: PNG image data, 1697 x 608, 8-bit/color RGB, non-interlaced
anna@anna:~/Downloads$ mv flag.txt extflag.png
anna@anna:~/Downloads$ display extflag.png 
```
## CHALLENGE 2
### SAKURA ROOM
#### Task 1:
##### 
Flag was already provided.
#### Task 2:
#####
On opening the webpage, an image was displayed. On inspecting the page, the username was found as SakuraSnowAngelAiko.
#### Task 3:
#####
On searching for the username, a LinkedIn page was found, which contained the full name of the attacker Aiko Abe.
Also, a github account was foung which contained a few repos.
Analyzing the repos, the PGP reository contained a public key block. On searching, I converted it into a .asc file and ran the command as follows to obtain the email address.
```shell
anna@anna:~/INFOSEC$ gpg --import email.asc 
gpg: key ECDD0FD294110450: public key "SakuraSnowAngel83@protonmail.com" imported
gpg: Total number processed: 1
gpg:               imported: 1
```
#### Task 4:
#####
While analyzing the repositories during the previous task, I fount one contained something about the ewallet. However, it was modified. THe original line was different. 
stratum://0xa102397dbeeBeFD8cD2F73A89122fCdB53abB6ef.Aiko:pswd@eu1.ethermine.org:4444
On searching, I found that that 0xa102397dbeeBeFD8cD2F73A89122fCdB53abB6ef was the wallet address. This took me to Ethereum transactions site and thus cryptocurrency was obttained.
The transaction history showed that the the mining pool on said date was Ethermine.
Some transactions showed Tether to be used which was the second cryptocurrency.

#### Task 5:
#####


