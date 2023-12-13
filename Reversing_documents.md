# Reversing documents (doc, docx, pdf, ...)
## source
* https://www.udemy.com/course/malware-analysis-of-documents/
* lots of other info in the course:
  * tools to use
  * pdf file format, objects, keywords, strings, data encoding methods
  * 
## info
* static techniques
  * embedded string analyzes
  * searching encoded or encrypted data
* dynamic techniques
## OS
* FlareVM (Windows)
* Remnux (Linux)
## tools
### basic tools, commands (Linux)
<pre>
$ file file1.pdf
$ strings -a file1.pdf | less
$ xorsearch file1.pdf http
$ xorsearch -p file1.pdf (-p is for password)
$ exiftool file1.pdf | less
$ yara ./yara-rules/index.yar file1.pdf
</pre>
### Tipical virus scanner tools
* Windows Defender
* virustotal
* Tridnet
* dir /R (view Alternate Data Streams)
### Steganography tools
<pre>
file file1.jpg
strings -a file1.jpg
steghide info file1.jpg (ha passphrase-t ker probaljuk meg uressel! ha az nem jo, akkor stegcracker kell!)
steghide extract -sf file1.jpg (ha passphrase-t ker probaljuk meg uressel! ha az nem jo, akkor stegcracker kell!)
foremost -i file1.jpg
binwalk file1.jpg
binwalk -e file1.jpg
stegcracker file1.jpg rockyou.txt
</pre>
### Yara rules
* yara rule files for other tools
* https://github.com/Yara-Rules/rules
### yara
<pre>
# usage
yara ./yara-rules/index.yar file1.pdf
# parameters
-w: Turn off warnings
-g: Print tags
-m: Print metadata
-s: Print matching strings
</pre>
### zipdump
* iterate over zip archive
* run yara signatures against each file
* https://github.com/DidierStevens
<pre>
zipdump -y signature.yar document.docx
</pre>
### exiftool
* extracts metadata from dozens of file types
* https://www.sno.phy.queensu.ca/-phil/exiftool/
