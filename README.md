# CTF tools and useful commandline tips #

## Preparation Checklist ##

### Installation ###

#### Operating Systems (VMware) ####

* [Kali Linux](https://www.kali.org/downloads/)
* Windows (32-bit version preffered)
* SQL databases viewer

#### Apps ####

* wireshark (for opening network capture files)
* audacity (for manipulating on voice files)
* VmWare and VirtualBox (for recovering corrupted disk image files)
* one email client (for opening .eml email and attachment backups)

#### Other Stuff ####

* Backup Internet Connection
* Anonymous Masks

#### Command Line Tools ####

* exiftool (check image tags)
* outguess
* net-tools (includes nmap and netstat and other primary networking tools)

# Basic UNIX command-line tips #

## Finding text ##

```
grep flag /path/to/file
grep -i flag /path/to/file # Non case-sensitive
grep -R flag . # Search all files in current directory recursively
grep -a flag /path/to/file # Process a binary file as if it were text
```

In vim and man pages: `[ESC] /flag [enter]` jump to next result with `[N]`

## Wget options ##

```
wget -rc http://example.com # Download a mirror of example.com
wget ???? http://example.com # Ignore robots.txt and crawl
wget -rcA .pdf http://example.com # Download all pdf files in example.com
```
@smmsadrnezh **TODO**

## Steganography ##

### Text ###

#### Poem Code ####

[Solution](http://wmbriggs.com/post/2309/)

### Images checklist ###

#### Check exif tags ####

```
exiftool example.jpg
```

#### That goddamn trivia ####

commandline tool `outguess`

#### Least Significant Bit (LSB) Insertion ####

* idea: 8th bit of some or all of the bytes is changed to a bit of secret message.
* symptoms: BMP files

#### diff command ####

#### Image editing in python ####

```
From PIL import Image

# Save and load
img = Image.open('/path/to/file')
img.save('/path/to/file')

# Process images
Image.blend(image1,image2,0.5) # Should be the same size
**TODO**: add more stuff here!
```

### Audio checklist ###

* Changing play speed
* Find difference of left and right channel
* Reversing audio
* Visualizing audio with specterum tool in audacity
* Transforming from time space to frquency space
* Search the lyrics if applicable

### Hashes ###

* This online tool is good: http://string-functions.com/
* AES en/de-cryption: http://aes.online-domain-tools.com/


#### Encrypting MD5 ####

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

#### Decrypting MD5 ####

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

## Secure coding ##

* Check for array length (overflow)
* Check for array index [0..n-1], non negative, not \ge n
* printf(string) -> printf("%s", string)
**TODO**

## Web ##

* Vularnablity scanner: http://www.acunetix.com/
* Stealing cookies
* Changing php session id
* SQL injection
* Inspect ajax requests
* Using javascript in fields like username and search \([XSS](https://www.owasp.org/index.php/XSS_Filter_Evasion_Cheat_Sheet)\)
* Check these:
  1. `../../../../passwd`
  2. postgresql tables: `pg_catalog` `pg_namespace`
  3. `../flag.txt`
  4. **TODO**
* Add characters like %00 and %20 to ajax URLs

## Reverse and Exploit ##

Well, i **should** put some time in mastering these tools, they're very useful in CTF contests.
Best ever tool: [IDA](https://www.hex-rays.com/products/ida/support/download.shtml)

## Windows ##

* Files may be packed using [ASPack](http://aspack.com/)
* Snowman is very good in decompiling C programs

### Linux ###

1. nm
**TODO**
2. objdump
**TODO**
3. gdb
**TODO**
4. metasploit
