# eXchange ORIC - xoric.js

(C) 2020 Jonas S Karlsson (jsk@yesco.org)

https://github.com/yesco/Xoric.git

## file and format converter for ORIC

Convert, flatten, extract files from .tap tape arhieves.

## Why?

There are several converters, but they all seem to have complicated dependencies, and or, only runs on window with UI. Source code is in many caseees not available, so, too my knowledge, there are few unix/style tools available.

It is also an explicit goal to have a single file, it can just be copied from githumb (click on 'raw' when viewing the file)

## LICENCE

AGPL: GNU Affero

http://www.gnu.org/licenses/agpl-3.0.html

The intention in my words (which may not be completely AGPL but close hopefully):

- conribute to the still vibrant ORIC community!
- open source to make it widely available and portable
- single file (easy share)
- javascript (nodejs +/- web!)
- generic command line tool
- generic converter library (require/<script>)
- please share back changes to the tool, if modified, contributions welcome
- fun, fun, and more fun!
- *NOTE:* AGPL *does* require changes to the tool/file to be contributed back (shared) even if running as web-service and not distributing (major diff from GPL).

Note: all data output is only on STDOUT, so it can be safely '> tofile', all descriptive messages go to STDERR and help, (not for -h "only"). '-q' can be used to remove (most) STDERR infos, '-v' (one or more) increses debug info.

Note: Files are only created for:
- format: '???2new'
- output file '-Ofil'

## Developement

Inside a simple "linux"-style environment, Termux on android-phone running emacs!

## Dependencies

It only depends on node(js), and only uses require('fs').

## Description

   node xoric -h	# gives ==>
   
<pre>
eXchange ORIC - xoric.js
          eXchange ORIC - xoric.js

 (C) 2020 Jonas S Karlsson (jsk@yesco.org)

    file and format converter for ORIC

==========================================
Usage: node xoric.js FMTLIST FILE ...
 
-h	print help to stderr
-dDIR	change default directory (OUT)
-oNAME	new name for last file
-ONAME	output all (tap?) to one file
        (if "xoric DIR/* -ODIR.tap" remove DIR from file names_
-q	quiet, no info output on stderr
-v      more verbose (default 1)
-v -v ... even more (up to 3/4)

FUNCTIONS

 (lowercase works fine too...)
 
- bas2bac: convert from BASs to BAC (tokenized)
- bac2bas: convert from BAC to BAS (text from tokenized)
- txt2num: convert from TXT to NUM (number lines of plaintext! == poor mans ORIC text editor? 'UNM' to undo)
- txt2hex: convert TXT to HEX
- txt2b64: convert TXT to B64
- tap2bas: print plain text basic from token-encoded TAP file
- raw2tap: make new tap-files from unmodified raw files
- tap2dir: list meta info from TAP files as DIR (actually just prints JSON-haha!)
- tap2new: extract NEW files from one or more .tap-files to the OUT directory (-dDIR)
- tap2tap: extract files from several .tap-files and put together in one tap file! (ok, easier to just concatenate files yourself..., lol)

- ???2???: maybe it works! - try it...

Basically, the first format (from-format) is used to decode. Use 'raw' to not decode. And, the last format is used to encode.

CAVEAT
  totally untested on actual ORIC ;-)

  feel free to send patches!

FILE
  filename (oric accepts upto 15 chars)

  FOO		- file to read from
  FOO.BAS,AUTO  - mark it to be AUTO loaded
		  (if written out/.tap)
  foo.o,A4#300	- load machine code in page 3
  foo.o,AUTO,A. - -"-, and mark it to be called
  big.txt,A..,E. - if E-A+1 < len(big.txt) trunc!

 (Note: file names are created with ,AUTO,E.. etc if needed (not basic) when extracted from .tap-files)
 (Note: 'EMPTYEMPTYEMPTY' is used instead of '' when creating files; it's also converted to '' when creating .tap-file)

FMTLIST
  comma(or 2)-separated list formats:

  (input/outout)
    raw = byte array
    hex = hexify bytes in
    b64 = base64 encoding
    txt = string
    bas = string
    bac = ORIC BASIC tokenized
    tap = ORIC .tap (archieve)
    fil = fil(e) object (as below)
    new = create new files (from tap)

  (specific for output)
    dir = [fil, ...] ('json' output from tap)
    new = create new files (from tap)
    num = string (NUMber text lines, see -n)
    unm = string (UNuMber text lines)

  (unsupported)
    dir = [fil, ...]

EXAMPLES
  (default prints to stdout)

  (hex and b64 (base64))
node xoric txt2hex dump.mem > dump.hex # hexdump
node xoric hex2txt dump.hex > dump.mem # 'unhex
node xoric txt2hex dump.hex > dump.2hx # 2xhex

  (NOP)
node xoric hex2hex fil
node xoric XXX2XXX fil

  (make .tap)
node xoric txt2tap a b c > abc.tap   # tap-archieve
node xoric txt2tap a b c -Oabc.tap # tap-archieve
node xoric tap2dir a b c     # "json" dir list
node xoric tap2txt abc.tap   # print a b c stdout
node xoric tap2new           # create files OUT/a OUT/b OUT/c
node xoric tap2new -Dtmp     # create files tmp/a tmp/b tmp/c

  (merge .tap archieves)
node xoric tap2tap a.tap b.tap -Oa.tap

  (make tap from directory)
node xoric Games/* -OGamees.tap" # remove 'Games'rom file names

---
Usage: node xoric.js FMTLIST FILE ...
</pre>



