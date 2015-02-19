####In the name of god

## CTF Tools and useful commandline options

Basic UNIX command-line tools
=============================

Finding text
------------
```
grep flag /path/to/file
grep -i flag /path/to/file # Non case-sensitive
grep -R flag . # Search all files in current directory recursively
grep -a flag /path/to/file # Process  a binary file as if it were text
```

In vim and man pages: `[ESC] /flag [enter]` jump to next result with `[N]`

Wget options
------------
```
wget -rc http://example.com # Download a mirror of example.com
wget ???? http://example.com # Ignore robots.txt and crawl
wget -rcA .pdf http://example.com # Download all pdf files in example.com
```
@smmsadrnezh **TODO**


Image checks
============

Check exif
----------

That goddamn trivia
------------------
commangline tool `outguess`

Image editing in python
-----------------------
```
From PIL import Image

# Save and load
img = Image.open('/path/to/file')
img.save('/path/to/file')

# Process images
Image.blend(image1,image2,0.5) # Should be the same size
**TODO**: add more stuff here!
```


Audio checks
============
* Changing play speed
* Find difference of left and right channel
* Reversing audio
* Visualizing audio with specterum tool in audacity
* Transforming from time space to frquency space
* Search the lyrics if applicable

Hashes
======

* This online tool is good: http://string-functions.com/
* AES en/de-cryption: http://aes.online-domain-tools.com/


Encrypting MD5
--------------
* Online: http://www.md5calc.com/
* PHP: `echo "<?=md5('plain text');?>" | php`
* Python:
```
import hashlib
def md5(string):
	hasher = hashlib.md5()
	hasher.update(string)
	return hasher.hexdigest()
```
* Bash: `printf plain text | md5sum`

Decrypting MD5
--------------
* Good for bath decoing. Has a simple captcha: http://www.hashkiller.co.uk/md5-decrypter.aspx
* No captcha, can be used in python:
```
import requests

def decrypt_md5(encrypted):
  post_values = {
    'hash':encrypted,
    'submit':'Decrypt It!',
  }
  resp_text = requests.post(url='http://md5decryption.com/', data=post_values).text
  ii = resp_text.find('Decrypted Text: </b>') + 1
  ii = resp_text.find('>', ii) + 1
  jj = resp_text.find('<', ii)
  resp = resp_text[ii:jj]
  return resp
```

Secure coding
=============
* Check for array length (overflow)
* Check for array index [0..n-1], non negative, not \ge n
* printf(string) -> printf("%s", string)
**TODO**

Web
===
* Vularnablity scanner: http://www.acunetix.com/
* Stealing cookies
* Changing php session id
* SQL injection
* Inspect ajax requests
* Using javascript in fields like username and search \([XSS](https://en.wikipedia.org/wiki/Cross-site_scripting)\)
* Check these:
  1. `../../../../passwd`
  2. postgresql tables: `pg_catalog` `pg_namespace`
  3. `../flag.txt`
  4. **TODO**
* Add characters like %00 and %20 to ajax URLs

Reverse and Exploit
===================
Well, i **should** put some time in mastering these tools, they're very useful in CTF contests.
Best ever tool: [IDA](https://www.hex-rays.com/products/ida/support/download.shtml)

Windows
-------
* Files may be packed using [ASPack](http://aspack.com/)
* Snowman is very good in decompiling C programs

Linux
-----
1. nm
**TODO**
2. objdump
**TODO**
3. gdb
**TODO**
