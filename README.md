### XMR-Stak-AMD - Monero mining software

XMR-Stak is a universal Stratum pool miner. This is the AMD GPU-mining version; there is also an [CPU version](https://github.com/fireice-uk/xmr-stak-cpu) and an [NVIDA GPU version](https://github.com/fireice-uk/xmr-stak-nvidia)

#### HTML reports

<img src="https://gist.githubusercontent.com/fireice-uk/2da301131ac01695ff79539a27b81d68/raw/e948641897ba79e5a6ee78e8248cc07779d6eac7/xmr-stak-amd-hashrate.png" width="260"> <img src="https://gist.githubusercontent.com/fireice-uk/2da301131ac01695ff79539a27b81d68/raw/e948641897ba79e5a6ee78e8248cc07779d6eac7/xmr-stak-amd-results.png" width="260"> <img src="https://gist.githubusercontent.com/fireice-uk/2da301131ac01695ff79539a27b81d68/raw/e948641897ba79e5a6ee78e8248cc07779d6eac7/xmr-stak-amd-connection.png" width="260">

The hashrate shown above was generated on a non-modded, non-overclocked RX 480.

#### Usage on Windows 

1) Edit the config.txt file to enter your pool login and password. 
2) Double click the exe file. 

XMR-Stak should compile on any C++11 compliant compiler. Windows compiler is assumed to be MSVC 2015 CE. MSVC build environment is not vendored.
```
-----BEGIN PGP SIGNED MESSAGE-----
Hash: SHA256

Windows binary release checksums

sha1sum
774f20271610741ec20c5f1c7e9d20467e3f3834  xmr-stak-amd.exe
cc7c22b0800a4c615d05dd53f8c6faa65d20ba24  xmr-stak-amd-notls.exe
d34a0ba0dd7b3b1f900a7e02772e197e974b4a73  libeay32.dll
2ee9966a0fc163da58408d91be36b84fa287c10b  ssleay32.dll
5acb656005a86cad90c6327985c3795d96a96c91  opencl/blake256.cl
603322cbe721964d76de68660f63f97f1bcd4057  opencl/cryptonight.cl
c9fb5e4bfb137ff60063978eecd10bffb7c4deb6  opencl/groestl256.cl
361dfce776ee4a89b100d139a879af5d0f0d65e4  opencl/jh.cl
429f559190d1163335847cc08df955234051504b  opencl/wolf-aes.cl
e2862a6d7094aeab21844d3155803e5da99b4a46  opencl/wolf-skein.cl

sha3sum
487b2f05cfd71a9cb4acd0eba2734162d605ada539900f83f43d7a6b  xmr-stak-amd.exe
d79dec89112811ea61a4486a91e1c22e48f3293b1d6e28e951d346af  xmr-stak-amd-notls.exe
133c065d9ef2c93396382e2ba5d8c3ca8c6a57c6beb0159cb9a4b6c5  ssleay32.dll
05003137a87313c81d6c348c9b96411c95d48dc22c35f36c39129747  libeay32.dll
a52b05548fd094e7bbb2367d7922bf19af3ed23ad5df53004fae0825  opencl/blake256.cl
8b3d0f4a39fca8a6d21afe9121796343379605017a167fa148c374d3  opencl/cryptonight.cl
13315b0a475212c92e10b7627b03a0813132437d4496b6596821b909  opencl/groestl256.cl
89548b917dbe216f5809624ebe350859c1d800048909322049f93d23  opencl/jh.cl
806eb1d4e3d7b6630a422bb42ee00faa76d31143b7c1cbde65e46938  opencl/wolf-aes.cl
052176a740a5a0bc088feea0aa7a72f0e9d96d6b6ffd00844676dd17  opencl/wolf-skein.cl

date
Sun 28 May 10:18:31 BST 2017
-----BEGIN PGP SIGNATURE-----
Version: GnuPG v2

iQEcBAEBCAAGBQJZKpX9AAoJEPsk95p+1Bw0BAYIALFYF5Ud+kKxb9uNyQaD3h5n
yv1MrdI81lpTRWpjK2naAN+pymAx7MwMi4KU0hTy5FMOuX+Ssb8kJsCAXKUYogff
W4+M4Bk6JaCcrJVhhgK2ucuDm8H1uQ+Ps/nPa+a7foT6d+7kGtj7bXPeOWyr+oUB
IbP/LnG40jOJnzG1u6/1e3YLXewWOEdLOYi8fN7VAl5b5uwmWw4DcWkQT1aiaFCV
awJCjDUNWtZ3+wgzE9ZU2cPmNXDKTuVHnR9F6+S8CDJs+yPe5phQuTrIObB5dhpD
trZnODWL/fZehf1koNCxKxpBDhGaDX7nx7j0NjN/btYhNwm9dckd9Xz3B3/Cod8=
=0alz
-----END PGP SIGNATURE-----
```

#### Usage on Linux (Debian-based distros)

**AMD Driver**

http://support.amd.com/en-us/kb-articles/Pages/AMDGPU-PRO-Install.aspx


```
    sudo apt-get install ocl-icd-opencl-dev libmicrohttpd-dev libssl-dev cmake build-essential
    cmake .
    make
```

#### Usage on Linux (Fedora-based distros)

**Download the CentOS 7 AMD Driver**

http://support.amd.com/en-us/kb-articles/Pages/AMDGPU-PRO-Install.aspx

Do not install the full AMDGPU-PRO driver, as Fedora has a newer version of X11 than the driver works with, instead do the following on the AMDGPU-PRO Installer.

Press Y when it prompts to install OpenCL related packages. Ignore the DKMS errors.
```
sudo amdgpu-pro-install --compute
```

```
    sudo dnf install ocl-icd-devel libmicrohttpd-devel openssl-devel cmake gcc-c++
    cmake .
    make
```

To run the miner with the newly installed OpenCL libraries, create a shell script in the bin folder containing the following

```
#!/bin/bash
LD_LIBRARY_PATH=/usr/lib64/amdgpu-pro-opencl/ ./xmr-stak-amd
```

GCC version 5.1 or higher is required for full C++11 support. CMake release compile scripts, as well as CodeBlocks build environment for debug builds is included.

#### Mining performance 

Mining core is a direct port (except for sercurity fixes) of wolf9466's AMD mining code. Performance is likely to be identical.

#### Default dev donation
By default the miner will donate 2% of the hashpower (2 minute in 100 minutes) to my pool. If you want to change that, edit **donate-level.h** before you build the binaries.

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

