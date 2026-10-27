# osint-case3-metadata-analysis-investigations
\# OSINT, Case 3: Whose Photo Is This?

case 3 photo.zip



/\* Background: You have received a photograph.

Determine: Who took this photo and the camera model used to take it. \*/







\*\*In short.\*\* The metadata in the file has been tampered with. This is a cropped copy of an image from Wikimedia Commons; the author listed there is user davric, and it was published in 2007. We were unable to directly identify the camera used to take the photo itself. The most likely candidate is a Nikon Coolpix 5700, but this is an indirect conclusion.



\## Task



The file `photo 3.jpg` (JPEG, 1024×749). The exact wording of the task: “You have received a photograph. Determine: who took this photo and the model of the camera used to take it.”

\## What the metadata revealed



The command `exiftool -a -u -g1 “photo 3.jpg”`, output:

ExifToolVersion                 : 13.59

FileName                        : photo 3.jpg

Directory                       : .

FileSize                        : 167 kB

ZoneIdentifier                  : Exists

FileModifyDate                  : 2026:10:22 13:04:06+03:00

FileAccessDate                  : 2026:10:27 22:07:23+02:00

FileCreateDate                  : 2026:10:22 12:41:46+03:00

FilePermissions                 : -rw-rw-rw-

FileType                        : JPEG

FileTypeExtension               : jpg

MIMEType                        : image/jpeg

JFIFVersion                     : 1.01

ResolutionUnit                  : inches

XResolution                     : 96

YResolution                     : 96

ExifByteOrder                   : Big-endian (Motorola, MM)

Make                            : Motorola

Model                           : Moto G3

Artist                          : Roger Smith

ISO                             : 80

DateTimeOriginal                : 2019:01:06 19:56:33

CreateDate                      : 2019/01/06 19:56:33

MeteringMode                    : Multi-segment

Flash                           : No Flash

SubSecTimeOriginal              : 49

SubSecTimeDigitized             : 49

FocalLengthIn35mmFormat         : 45 mm

Padding                         : (Binary data 1972 bytes; use the -b option to extract)

XPAuthor                        : Roger Smith

Padding                         : (Binary data 2000 bytes; use the -b option to extract)

About                           : uuid:faf5bdd5-ba3d-11da-ad31-d33d75182f1b

Creator                         : Roger Smith

CreateDate                      : 2019/01/06 19:56:33.491

ImageWidth                      : 1024

ImageHeight                     : 749

EncodingProcess                 : Progressive DCT, Huffman coding

BitsPerSample                   : 8

ColorComponents                 : 3

YCbCrSubSampling                : YCbCr4:2:0 (2 2)

ImageSize                       : 1024x749

Megapixels                      : 0.767

SubSecCreateDate                : 2019-01-06 19:56:33.49

SubSecDateTimeOriginal          : 2019:01:06 19:56:33.49





!Pay attention to the Padding line!!! //Padding                         : (Binary data 1972 bytes, use -b option to extract)

This gives us the answer: Roger Smith, Motorola Moto G3, January 2019.

But! Why didn’t I stop there?



The EXIF data is suspiciously empty. It has the ISO and date, but no shutter speed, aperture, EXIF version, or frame dimensions—even though any real camera would record those. // Interesting!

Next, I dug deeper and ran a reverse image search, which led me to the original photo `Afghanistan\_16.jpg` (1543×1129). It was uploaded on September 9, 2007, by user davric, under a public domain license. This contradicts the metadata: the Moto G3 was released in July 2015, but the photo has been on Commons since 2007. I downloaded the original from Commons and compared it.



1) The SHA-1 (which acts as a unique fingerprint for the photo) matches what is listed on the file page.

2) The original contains neither EXIF nor XMP data, only a JFIF header (149 dpi). In other words, everything that `exiftool` showed in `photo 3.jpg` was added after publication.

According to Commons, the author of the photo is davric (account Davric\~commonswiki). He identified it as his own work from his personal collection. This is his own statement; there is no separate confirmation on the page. I did not determine who this person actually is: it is not necessary for this task. // I determined that this is a soldier from the French ISAF contingent who served in Afghanistan in 2005 as part of the 2nd Foreign Infantry Regiment (possibly a sniper) (2e REI) of the French Foreign Legion.

3)  The original file has no EXIF data, so the model cannot be determined from it. I then looked at other files from the same account. Some of them also lack EXIF data, but `Cougar Afghanistan.JPG` (uploaded on October 2, 2007) does have it: manufacturer NIKON, model E5700 (this is the Nikon Coolpix 5700), software E5700v1.1, 300 dpi, size 2560×1920, camera time 21.04.2005 04:44.

4) Therefore, most likely, the author took the photo with a Nikon Coolpix 5700. //But this is an indirect conclusion!



My mistake was when I assumed that 149 dpi meant it was a scan. This isn’t proof: the resolution is recorded by the last program that saved the file. I also thought the image had been cropped, but it was actually just resized.

//exiftool -a -s -u "" 
//exiftool (hash)









\- Cougar Afghanistan.JPG: <https://commons.wikimedia.org/wiki/File:Cougar\_Afghanistan.JPG>\- Moto G (3rd generation): <https://en.wikipedia.org/wiki/Moto\_G\_(3rd\_generation)>\- ExifTool: <https://exiftool.org/>
