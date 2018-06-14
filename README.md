# Path  traversal with zip archive

Two examples of zip files that break the current directory and extract a file to the `/tmp/`


 First archive contains symlink `path` to `../../../../../tmp`
```bash
$ zipinfo symlink.zip

Archive:  symlink.zip
Zip file size: 330 bytes, number of entries: 2
lrwxr-xr-x  3.0 unx       18 bx stor 18-Jun-14 13:26 path
-rw-r--r--  3.0 unx        0 bx stor 18-Jun-14 11:46 path/file.txt
2 files, 18 bytes uncompressed, 18 bytes compressed:  0.0%
```
#
Second archive contains file with target directory `/tmp/` (which is not correct, according [zip format speciffication](https://pkware.cachefly.net/webdocs/casestudies/APPNOTE.TXT))

  
         4.4.17 file name: (Variable)
         4.4.17.1 The name of the file, with optional relative path.
         The path stored MUST not contain a drive or
         device letter, or a leading slash. 
         
        


```bash
$ zipinfo absolutepath.zip

Archive:  absolutepath.zip
Zip file size: 289 bytes, number of entries: 2
drwxr-xr-x  2.1 unx        0 bx stor 18-Jun-13 23:13 /tmp/
-rw-r--r--  2.1 unx        5 bX defN 18-Jun-13 23:13 /tmp/file.txt
2 files, 5 bytes uncompressed, 7 bytes compressed:  -40.0%
```