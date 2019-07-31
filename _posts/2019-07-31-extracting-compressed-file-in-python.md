---
title: Extracting Compressed File in Python
---

In our daily life data compressing is a must need work for handling large data file. And also we need to decompress or extract data from compress data. Common compress file extension are `zip`, `tar`, `tar.gz`, `bz2`, `7z` and so on. While working with python we need to know how to extract those compressed data in python. 

Here is some way in python to extract data from common compressed extension

## `.zip` File Extracting

```py
from zipfile import ZipFile
zf = ZipFile('path_to_file/file.zip', 'r')
zf.extractall('path_to_extract_folder')
zf.close()

```

## `.tar` or `.tar.gz` File Extracting

```py
import tarfile
tar = tarfile.open("file.tar.gz") # or file.tar
tar.extractall()

```

## `.bz2` File Extracting

```py
import bz2
zipfile = bz2.BZ2File(filepath) # open the file
data = zipfile.read() # get the decompressed data
newfilepath = filepath[:-4] # assuming the filepath ends with .bz2
open(newfilepath, 'wb').write(data) # write a uncompressed file

```

## `.7z` File Extracting(python 3 only)

```py
import lzma
with lzma.open('data.7z') as f:
    f.extractall("<output path>")

```

## References
* [stackoverflow](stackoverflow.com)
