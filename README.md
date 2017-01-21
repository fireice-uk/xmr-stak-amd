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

sha1sum xmr-stak-cpu.exe
32f551c891040eda2c25e18e6287665471a5a653  xmr-stak-cpu.exe

sha3sum xmr-stak-cpu.exe
ed12841738c899a3eb61f51787aa670c25b64ce3c5a626717e6a8f6b  xmr-stak-cpu.exe

date
Mon 16 Jan 15:13:25 GMT 2017
-----BEGIN PGP SIGNATURE-----
Version: GnuPG v2

iQEcBAEBCAAGBQJYfONvAAoJEPsk95p+1Bw02coH/0by+VMK76gnmpNjIxDcphkV
S1GG+f0sIAYUrGpoMCJTXbr7hU3Na+grTbt6xLM2Tb0xJjX4Mc47Cixajzy7+TTx
R2+CvBRl8LG9zob6JNiohvxD1+SK7RWDKWenFyDlr9BewgE/ArqZM+16BQBrLP9H
XIWy1wh/lcSYuS548tnUYdNOmEnR9TqA454M4r8PED85HSpNmvI+eG8fZ8OK471C
3yMupjYlAbiEBT+gE6bZwLeeCH9NO2gGeBAb31w8RBsMRjy+VvhFhTOoJwZbXj9e
sMUwNBu+fLVoilMVvp8SDpQ7Uw/WFT085N2eJiCCuEbHgFAwM3uwD6VHz3eXd0s=
=QJQj
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

#### CPU mining performance 

Performance is nearly identical to the closed source paid miners. Here are some numbers:

* **I7-2600K** - 266 H/s
* **I7-6700** - 276 H/s (with a separate GPU miner)
* **Dual X5650** - 466 H/s (depends on NUMA)
* **Dual E5640** - 365 H/s (same as above)

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
* 4581HhZkQHgZrZjKeCfCJxZff9E3xCgHGF25zABZz7oR71TnbbgiS7sK9jveE6Dx6uMs2LwszDuvQJgRZQotdpHt1fTdDhk



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




