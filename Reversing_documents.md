# Document reversing source
* https://www.udemy.com/course/malware-analysis-of-documents/
* lots of other info in the course:
  * tools to use
  * pdf file format, objects, keywords, strings, data encoding methods
# Reversing Operating Systems
* FlareVM (Windows)
* Remnux (Linux)
# Pdf analysis
## Tools
### pdfid
* identify PDF object types and filters
* https://blog.didierstevens.com/programs/pdf-tools/
* (it only tells you what is in the document not where it is)
  * in case of suspicious things you should move on to pdf-parser
### pdf-parser
* parses, searches, and extracts data from PDF documents
* https://blog.didierstevens.com/programs/pdf-tools/
* options
<pre>
-s TERM: Search for TERM
-o #: Print object number
-f: Decode data in object
-w: Display raw data from object
</pre>
### peepdf
* combines multiple tools into once
* finds suspicious objects
* decodes data
* javascript analysis built-in
* http://eternal-todo.com/tools/peepdf-pdf-analysis-tool
* options
<pre>
-i: inline mode
-u: update
</pre>
## Online documentation
* https://acrobatusers.com/tutorials/print/importing-and-exporting-pdf-file-attachments-acrobat-javascript/
# Javascript analysis
## Tools
### peepdf
* beautifies and executes javascript in a sandbox
* not work in Remnux because of some python lib dependency issue
* http://eternal-todo.com/tools/peepdf-pdf-analysis-tool
* inline commands
<pre>
js_beautify file JSFILE
js_analyze file JSFILE
</pre>
### spidermonkey
* mozilla's implementation of javascript
* modified to write file when JS executes - eval, document.write, windows.navigate - commands
* https://blog.didierstevens.com/programs/spidermonkey/
* Remnux command
<pre>
js-file JSFILE
</pre>
## Javascript deobfuscation
* online tools
* manual techniques
# MS Office documents analysis
## Info
* malicious components: scripts (VBA macros), commands, embedded files
* office document formats
  * Office Open XML Format: Zip archive containing XML (.docx, .docm, ...)
  * Structured Storage Format: Binary format (.doc, .xls, .ppt...)
## Workflow in analysis office documents
* Determine the document type (file identification tools)
* Search for malicious indicators
* Extract and continue analysis
## Tools
* oletools
  * olebrowse - View and extract streams
  * oletimes - Extract times
  * oleid - Looks for malicious characteristics
  * olevba - Extract VBA scripts
  * https://www.decalage.info/python/oletools
* Office Open XML Format tools
  * exiftool - Metadata
  * zipdump + yara - Signature detection
  * olevba - VBA
# VBA script analysis
## Info
* VBA (Visual Basic for Applications) features
  * write to file system
  * open network connection
  * execute other programs
* Suspicious VBA commands
  * AutoOpen(), AutoExec(), AutoClose(), Chr(), Shell()
* Commands for loading external DLLs and APIs
  * GetWindowThreadProcessId, OpenProcess, WriteProcessMemory, ReadProcessMemory
* Script analysis indicators
  * URLs, commands, filenames
* VBA emulation engine
  * https://github.com/decalage2/ViperMonkey
<pre>
python vmonkey.py file1.docx
</pre>
# Misc tools
## Basic analysis tools (Linux)
<pre>
$ file file1.pdf
$ strings -a file1.pdf | less
$ xorsearch file1.pdf http
$ xorsearch -p file1.pdf (-p is for password)
$ exiftool file1.pdf | less
$ yara ./yara-rules/index.yar file1.pdf
</pre>
## Tipical virus scanner and analysis tools (Windows)
* Windows Defender
* virustotal (Windows and Linux as well)
* Tridnet
* dir /R (view Alternate Data Streams)
## Steganography tools
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
## Yara rules
* yara rule files for other tools
* https://github.com/Yara-Rules/rules
## yara
<pre>
# usage
yara ./yara-rules/index.yar file1.pdf
# parameters
-w: Turn off warnings
-g: Print tags
-m: Print metadata
-s: Print matching strings
</pre>
## zipdump
* iterate over zip archive
* run yara signatures against each file
* https://github.com/DidierStevens
<pre>
zipdump -y signature.yar document.docx
</pre>
## exiftool
* extracts metadata from dozens of file types
* https://www.sno.phy.queensu.ca/-phil/exiftool/
