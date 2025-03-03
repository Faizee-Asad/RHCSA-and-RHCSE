# Archiving and compression

* Backup data is generally in-frequently accessed. 
* To save storage spcace on server, the best practice is to keep backup data in comparessed form.
* In all linux flavous, there are multiple compression tools that can work with tR archive manager to compress the archived data.

* Various comparession tools are:
* gzip -> fast performance speed, average compression ratio.
* bzip2 -> bit slow performance speed, better compression ratio.
* xzip -> very slow performance speed, best compression ratio.

* Combination can be either tar & gzip or tar & bzip2 or tar & xzip
* Eg:
* tar cf /data.tar /usr/bin - tar cf /data.tar /usr/bin
* gzip /data.tar - bzip2 /data.tar
* gunzip /data.tar.gz - bunzip2 /data.bz2

```
## Compression using tar and gzip
# du -h /usr/sbin (to know directory size)
# tar zcf /bin.tar.gz /usr/sbin (to create an archive) 
# ls -lh /bin.tar.gz (to know the size of compressed archive)
# tar ztvf /bin.tar.gz (to list contents of an archive)
# tar zxf /bin.tar.gz (to extract full content)
# tar zxf /bin.tar.gz usr/sbin/nvme usr/sbin/ledmon (to extract some content)
# tar zxf /bin.tar.gz -C /home (to extract in different directory)

## Compression using tar and bzip2
# tar jcf /bin.tar.bz2 /usr/sbin (to create an archive)
# tar jtvf /bin.tar.bz2  (to list contents of an archive)
# tar jxf /bin.tar.bz2  (to extract content)

## Compression using tar and xzip
# tar Jcf /bin.tar.xz /usr/bin (To create an atchive)
# tar Jtvf /bin.tar.xz (to list contents of an archive)
# tar Jxf /bin.tar.xz  (to extract content)
```
