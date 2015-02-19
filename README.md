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


Image checks
------------

*Check exif*


*the goddamn trivia*
commangline tool `outguess`

*Image editing in python*
```
From PIL import Image

# Save and load
img = Image.open('/path/to/file')
img.save('/path/to/file')

# Process images
Image.blend(image1,image2,0.5) # Should be the same size
# TODO: add more stuff here!
```

