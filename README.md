In the name of god

CTF Tools and useful commandline options
===========================================

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
@smmsadrnezh

