# Reversing documents (doc, docx, pdf, ...)
## info
* static techniques
  * embedded string analyzes
  * searching encoded or encrypted data
* dynamic techniques
## tools
### basic tools, commands
<pre>
$ strings -a file1.pdf | less
$ xorsearch file1.pdf http
$ xorsearch -p file1.pdf
</pre>
### Yara rules
* yara rule files for other tools
* https://github.com/Yara-Rules/rules
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
