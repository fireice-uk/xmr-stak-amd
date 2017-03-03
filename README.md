### XMR-Stak-AMD - Monero mining software

XMR-Stak is a universal Stratum pool miner. This is the AMD version.

#### Usage on Windows 
1) Edit the config.txt file to enter your pool login and password. 
2) Double click the exe file. 

XMR-Stak should compile on any C++11 compliant compiler. Windows compiler is assumed to be MSVC 2015 CE. MSVC build environment is not vendored.
```
-----BEGIN PGP SIGNED MESSAGE-----
Hash: SHA256

Windows binary release checksums

sha1sum
57a1b9fa24d19f13a0cbcba9fb9cc0f12fa5fd49  xmr-stak-amd.exe
d34a0ba0dd7b3b1f900a7e02772e197e974b4a73  libeay32.dll
2ee9966a0fc163da58408d91be36b84fa287c10b  ssleay32.dll
5acb656005a86cad90c6327985c3795d96a96c91  opencl/blake256.cl
9e4e276afd9000945c25f6e5a5259977a29239f4  opencl/cryptonight.cl
c9fb5e4bfb137ff60063978eecd10bffb7c4deb6  opencl/groestl256.cl
361dfce776ee4a89b100d139a879af5d0f0d65e4  opencl/jh.cl
429f559190d1163335847cc08df955234051504b  opencl/wolf-aes.cl
e2862a6d7094aeab21844d3155803e5da99b4a46  opencl/wolf-skein.cl

sha3sum
8a6fd1f761706a57a115b1b4196536802b15ba759b25ad5de75f0fac  xmr-stak-amd.exe
133c065d9ef2c93396382e2ba5d8c3ca8c6a57c6beb0159cb9a4b6c5  ssleay32.dll
05003137a87313c81d6c348c9b96411c95d48dc22c35f36c39129747  libeay32.dll
a52b05548fd094e7bbb2367d7922bf19af3ed23ad5df53004fae0825  opencl/blake256.cl
a49c9da554d7b01d091eea56e8b97b943ca33cd2a64a1f3f3169e202  opencl/cryptonight.cl
13315b0a475212c92e10b7627b03a0813132437d4496b6596821b909  opencl/groestl256.cl
89548b917dbe216f5809624ebe350859c1d800048909322049f93d23  opencl/jh.cl
806eb1d4e3d7b6630a422bb42ee00faa76d31143b7c1cbde65e46938  opencl/wolf-aes.cl
052176a740a5a0bc088feea0aa7a72f0e9d96d6b6ffd00844676dd17  opencl/wolf-skein.cl

date
Fri  3 Mar 23:38:11 GMT 2017
-----BEGIN PGP SIGNATURE-----
Version: GnuPG v2

iQEcBAEBCAAGBQJYuf57AAoJEPsk95p+1Bw08hQIAJSCNUfd7tHx8FXH7O4Up4Q8
ONXefhssOIHeoRsQFjKb6eXzG705YpvqeF24XPvmd/GKRKaisVq9WZ0PJDkTlXNU
k4KIefsvOPiLGMFvQRSUjvXlgB2lcuidwW+zCevQVtk8Iq5MCZmjbqs9l6HkFp5E
ceiAPFct7OgI49lAEX1HvA0FTf1JCzyqkAYzFDo54n3zeyiLNmfM/UdvLFTDyck7
o2wrL/HXIGfuABeUX9WPW8SJCRdVhGscNbhbdIoP6jRnXK0/Ggnkk7DHjE+cWKVm
EnJKo9xo5MURJOKVpTgkxBa/d5jjCIKynUjPfphIBhWTtbDbArdWPEbA3X/dsT4=
=j9kt
-----END PGP SIGNATURE-----

```

#### Usage on Linux
```
    sudo apt-get install ocl-icd-opencl-dev
    sudo apt-get install libmicrohttpd-dev
    cmake .
    make
```

GCC version 5.1 or higher is required for full C++11 support. CMake release compile scripts, as well as CodeBlocks build environment for debug builds is included.

To do a static build for a system without gcc 5.1+
```
    cmake -DCMAKE_BUILD_TYPE=STATIC
    make
```
Note - cmake caches variables, so if you want to do a dynamic build later you need to specify '-DCMAKE_BUILD_TYPE=RELEASE'

#### Mining performance 

Mining core is a direct port (except for sercurity fixes) of wolf9466's AMD mining code. Performance is likely to be identical.

#### Example reports
```
HASHRATE REPORT
| ID | 2.5s |  60s |  15m | ID | 2.5s |  60s |  15m |
|  0 | 31.7 | 30.7 | 30.5 |  1 | 30.6 | 30.6 | 30.6 |
|  2 | 30.3 | 30.6 | 30.6 |  3 | 30.6 | 30.6 | 30.6 |
|  4 | 35.3 | 35.5 | 35.6 |  5 | 35.7 | 35.7 | 35.7 |
|  6 | 35.4 | 35.6 | 35.6 |  7 | 35.7 | 35.7 | 35.7 |
|  8 | 31.7 | 30.7 | 30.5 |  9 | 30.6 | 30.6 | 30.6 |
| 10 | 30.4 | 30.6 | 30.6 | 11 | 30.6 | 30.6 | 30.6 |
-----------------------------------------------------
Totals:   388.7 388.7 388.7 H/s
Highest:  388.7 H/s
```

```
RESULT REPORT
Difficulty       : 8192
Good results     : 5825 / 5826 (100.0 %)
Avg result time  : 10.3 sec
Pool-side hashes : 22683648

Top 10 best results found:
|  0 |         15407238 |  1 |         12699745 |
|  2 |         12194202 |  3 |          6999845 |
|  4 |          5533935 |  5 |          5315338 |
|  6 |          4700351 |  7 |          4500227 |
|  8 |          4023567 |  9 |          4021473 |

Error details:
| Count |                       Error text |           Last seen |
|     1 | [NETWORK ERROR]                  | 2017-01-02 21:29:15 |
```

```
CONNECTION REPORT
Connected since : 2017-01-02 21:29:40
Pool ping time  : 288 ms

Network error log:
| Date                |                                                       Error text |
| 2017-01-02 21:29:15 | CALL error: Timeout while waiting for a reply                    |
| 2017-01-02 21:29:30 | CONNECT error: GetAddrInfo: Name or service not known            |
```

#### Default dev donation
By default the miner will donate 1% of the hashpower (1 minute in 100 minutes) to my pool. If you want to change that, edit **donate-level.h** before you build the binaries.

If you want to donate directly to support further development, here is my wallet
```
4581HhZkQHgZrZjKeCfCJxZff9E3xCgHGF25zABZz7oR71TnbbgiS7sK9jveE6Dx6uMs2LwszDuvQJgRZQotdpHt1fTdDhk
```

#### PGP Key
```
-----BEGIN PGP PUBLIC KEY BLOCK-----
Version: GnuPG v2

mQENBFhYUmUBCAC6493W5y1MMs38ApRbI11jWUqNdFm686XLkZWGDfYImzL6pEYk
RdWkyt9ziCyA6NUeWFQYniv/z10RxYKq8ulVVJaKb9qPGMU0ESfdxlFNJkU/pf28
sEVBagGvGw8uFxjQONnBJ7y7iNRWMN7qSRS636wN5ryTHNsmqI4ClXPHkXkDCDUX
QvhXZpG9RRM6jsE3jBGz/LJi3FyZLo/vB60OZBODJ2IA0wSR41RRiOq01OqDueva
9jPoAokNglJfn/CniQ+lqUEXj1vjAZ1D5Mn9fISzA/UPen5Z7Sipaa9aAtsDBOfP
K9iPKOsWa2uTafoyXgiwEVXCCeMMUjCGaoFBABEBAAG0ImZpcmVpY2VfdWsgPGZp
cmVpY2UueG1yQGdtYWlsLmNvbT6JATcEEwEIACEFAlhYUmUCGwMFCwkIBwIGFQgJ
CgsCBBYCAwECHgECF4AACgkQ+yT3mn7UHDTEcQf8CMhqaZ0IOBxeBnsq5HZr2X6z
E5bODp5cPs6ha1tjH3CWpk1AFeykNtXH7kPW9hcDt/e4UQtcHs+lu6YU59X7xLJQ
udOkpWdmooJMXRWS/zeeon4ivT9d69jNnwubh8EJOyw8xm/se6n48BcewfHekW/6
mVrbhLbF1dnuUGXzRN1WxsUZx3uJd2UvrkJhAtHtX92/qIVhT0+3PXV0bmpHURlK
YKhhm8dPLV9jPX8QVRHQXCOHSMqy/KoWEe6CnT0Isbkq3JtS3K4VBVeTX9gkySRc
IFxrNJdXsI9BxKv4O8yajP8DohpoGLMDKZKSO0yq0BRMgMh0cw6Lk22uyulGALkB
DQRYWFJlAQgAqikfViOmIccCZKVMZfNHjnigKtQqNrbJpYZCOImql4FqbZu9F7TD
9HIXA43SPcwziWlyazSy8Pa9nCpc6PuPPO1wxAaNIc5nt+w/x2EGGTIFGjRoubmP
3i5jZzOFYsvR2W3PgVa3/ujeYYJYo1oeVeuGmmJRejs0rp1mbvBSKw1Cq6C4cI0x
GTY1yXFGLIgdfYNMmiLsTy1Qwq8YStbFKeUYAMMG3128SAIaT3Eet911f5Jx4tC8
6kWUr6PX1rQ0LQJqyIsLq9U53XybUksRfJC9IEfgvgBxRBHSD8WfqEhHjhW1VsZG
dcYgr7A1PIneWsCEY+5VUnqTlt2HPaKweQARAQABiQEfBBgBCAAJBQJYWFJlAhsM
AAoJEPsk95p+1Bw0Pr8H/0vZ6U2zaih03jOHOvsrYxRfDXSmgudOp1VS45aHIREd
2nrJ+drleeFVyb14UQqO/6iX9GuDX2yBEHdCg2aljeP98AaMU//RiEtebE6CUWsL
HPVXHIkxwBCBe0YkJINHUQqLz/5f6qLsNUp1uTH2++zhdBWvg+gErTYbx8aFMFYH
0GoOtqE5rtlAh5MTvDZm+UcDwKJCxhrLaN3R3dDoyrDNRTgHQQuX5/opJBiUnVNK
d+vugnxzpMIJQP11yCZkz/KxV8zQ2QPMuZdAoh3znd/vGCJcp0rWphn4pqxA4vDp
c4hC0Yg9Dha1OoE5CJCqVL+ic4vAyB1urAwBlsd/wH8=
=B5I+
-----END PGP PUBLIC KEY BLOCK-----
```

### Common Issues

**msvcp140.dll and vcruntime140.dll not available errors**

Download and install this [runtime package](https://www.microsoft.com/en-us/download/details.aspx?id=48145) from Microsoft.  *Warning: Do NOT use "missing dll" sites - dll's are exe files with another name, and it is a fairly safe bet that any dll on a shady site like that will be trojaned.  Please download offical runtimes from Microsoft above.*

