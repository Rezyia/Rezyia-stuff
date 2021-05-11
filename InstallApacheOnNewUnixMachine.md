## I didn't find any good guide to help me setup Apache2 on my new Ubuntu VM so here's what I did :

***

I suppose :
- apt up to date (`sudo apt update`)
- build esssential installed (for GCC) (`sudo apt install build-essential` + `sudo apt-get install manpages-dev`)
- You need to be root or have root access (pretty obvious though)

***

-	Need [pcre](https://ftp.pcre.org/pub/pcre/) ( DO NOT USE pcre2-xx.xx : pcre2 still doesn't work for it on this May 11th 2021 )
-	Need [apr](https://apr.apache.org/download.cgi) and [apr-util](https://apr.apache.org/download.cgi)
-	Need [httpd](https://httpd.apache.org/download.cgi#apache24)
(I recommend downloading with the .tar.gz extension)

How to decompress :
+ use : gzip -d xxxx.tar.gz
+ use : xvf xxxx.tar

```
Suppose a directory with : 		(versions used :)
./httpd-x.x.xx				(httpd-2.4.46)
./pcre-x.xx				(pcre-8.42)
./apr-x.x.x				(arp-1.7.0)
./apr-util-x.x.x                        (arp-util-1.6.1)
```

***

```
cd ./pcre-x.xx/
./configure                                                     (by default in /usr/local/bin)
sudo make
sudo make install

cd ..
cp -r ./pcre-x.xx/ /tmp/pcre                                    (or mv)

mv ./apr-x.x.x/ ./httpd-x.x.xx/srclib/apr		        (or cp)
mv ./apr-util-x.x.x/ ./httpd-x.x.xx/srclib/apr-util		(or cp)

cd ./httpd-x.x.xx
./configure –with-included-apr –with-included-apr-util –with-pcre=/usr/local/bin/pcre-config –with-pcre-dir=/tmp/pcre
sudo make						        (by default in /usr/local/apache2)
sudo make install
```

***

Now Apache2 should be installed correctly.
