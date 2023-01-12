---
linktitle: Create FiveM

---

## This easy
Wauw this is fast.

### Prerequisites
1. Install `xz-utils` and `git` packages. 
	```bash
	sudo apt update &&\
	sudo apt install xz-utils git wget -y
	```

### Installation
1. Create a new folder this will be used for the server binaries.
	```bash
	 mkdir -p ~/fivem
	```
2.	Lets enter enetr new created folder.
	```bash
	cd ~/fivem
	```
2. 	Visit [Linux server build listing][linux-artifacts] and right click on `master` branch build and copy the link url then replace that link with `<url>`
	```bash
	wget <url>
	```
3. Extract the build to the directory that was previously created, using:
	```bash
	tar xf fx.tar.xz
	```
4.	Now run `run.sh`
	```bash
	bash run.sh
	```

[windows-artifacts]: https://runtime.fivem.net/artifacts/fivem/build_server_windows/master/
[linux-artifacts]: https://runtime.fivem.net/artifacts/fivem/build_proot_linux/master/
[server-data]: https://github.com/citizenfx/cfx-server-data

[vcredist]: https://aka.ms/vs/16/release/VC_redist.x64.exe
[winrar]: https://www.rarlab.com/download.htm
[7zip]: https://www.7-zip.org/download.html
[git-scm]: https://git-scm.com/download/win

