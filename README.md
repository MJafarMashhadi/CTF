# CTF tools and useful command-line tips #

## Preparation Checklist ##

### Installation ###

#### Operating Systems (VMware) ####

* [Kali Linux](https://www.kali.org/downloads/)
* Windows (32-bit version preffered)
* SQL databases viewer

#### Apps ####

* Wireshark (for opening network capture files)
* audacity (for manipulating on voice files)
* VMware and VirtualBox (for recovering corrupted disk image files)
* one email client (for opening .eml email and attachment backups)

#### Other Stuff ####

* Backup Internet Connection
* Anonymous Masks

#### Command Line Tools ####

* ExifTool (check files meta info)
* outguess
* net-tools (includes nmap and netstat and nc and other primary networking tools)
* binwalk

# Basic UNIX command-line tips #

## Finding text ##

```
grep flag /path/to/file
grep -i flag /path/to/file # Non case-sensitive
grep -R flag . # Search all files in current directory recursively
grep -a flag /path/to/file # Process a binary file as if it were text
grep -oba PNG binaryfile.bin # Finds "PNG" in binaryfile.bin and returns the binary offset of it
```

In vim and man pages: `[ESC] /flag [enter]` jump to next result with `[N]`

## Binary Stuff ##
```
grep -oba PNG binaryfile.bin # Finds "PNG" in binaryfile.bin and returns the binary offset of it
dd status=none if=binaryfile.bin bs=1 skip=M count=N  # get a part of a binary file
binwalk  # Finds stuff in a binary file
binwalk --dd='.*' file  # Extracts stuff in a file
foremost -T  # Finds stuff in binary files
strings  # Finds strings within a file
radare2  # Static analysis of disassemblies
xxd  # make a hexdump or do the reverse.

```

[http://superuser.com/questions/294270/how-to-view-raw-binary-data-as-an-image-with-given-width-and-height](http://superuser.com/questions/294270/how-to-view-raw-binary-data-as-an-image-with-given-width-and-height) 
[http://serverfault.com/questions/173999/dump-a-linux-processs-memory-to-file](http://serverfault.com/questions/173999/dump-a-linux-processs-memory-to-file)

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
ExifTool example.jpg
```

#### That goddamn trivia ####

command-line tool `outguess`

#### Least Significant Bit (LSB) Insertion ####

* idea: 8th bit of some or all of the bytes is changed to a bit of secret message.
* symptoms: BMP files

#### diff command ####

* you may find the original image by searching problem image in [Google](https://images.google.com/) if it's not given.
* also it works for finding the difference between two text files.

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
* Find difference between left and right channel
* Reversing audio
* Visualizing audio with spectrum tool in audacity
* Transforming from time-space to frequency space
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

* Good for bath decoding. Has a simple captcha: http://www.hashkiller.co.uk/md5-decrypter.aspx
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

## Network ##

* check for open ports with nmap. Then connect through ssh or telnet or netcat or open it in a web browser. Maybe it is a non-standard port.

### wireshark ###

* find packets with telnet protocol. right-click on a packet in the session, and select 'Follow TCP Stream.' you see credential because telnet does not encrypt data.
* use HTTP filter to clean up the listed packets to only include those using the HTTP protocol. find URL or some meaningful text.
* find flag using the device which is captured [TODO]
* Network miner is a good windows software for mining pcap files


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
* check robots.txt file content and html page source for any information is hidden from the web.
* monitor cookies set on your browser when you send request to a web page.
* ?page=php://filter/read=convert.base64-encode/resource=../delete  To get files source codes on server (LFI)


## Reverse and Exploit ##

Well, I **should** put some time into mastering these tools, they're very useful in CTF contests.
Best ever tool: [IDA](https://www.hex-rays.com/products/ida/support/download.shtml)

Check binary tools in command line tools above.

`ltrace -C -i ./file` Dynamically analyses function calls

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

5. strings

