# Reversing documents (doc, docx, pdf, ...)
## info
* static techniques
  * embedded string analyzes
  * searching encoded or encrypted data
* dynamic techniques

## tools
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
