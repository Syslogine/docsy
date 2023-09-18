---
linktitle: Windows
---
# Windows

## Editions 
Hugo is available in two editions: standard and extended. With the extended edition you can:

*	Encode WebP images (you can decode WebP images with both editions)
*	Transpile Sass to CSS using the embedded LibSass transpiler
We recommend that you install the extended edition.

## Prerequisites 
Although not required in all cases, Git and Go are often used when working with Hugo.

Git is required to:
*	Use the [Hugo Modules](https://gohugo.io/hugo-modules/) feature
*	Build Hugo from source
*	Install a theme as a Git submodule
*	Access [commit information](https://gohugo.io/variables/git) from a local Git repository
*	Host your site with services such as [AWS Amplify](https://aws.amazon.com/amplify/), [CloudCannon](https://cloudcannon.com/), [Cloudflare Pages](https://pages.cloudflare.com/), [GitHub Pages](https://pages.github.com/), [GitLab Pages](https://docs.gitlab.com/ee/user/project/pages/), and [Netlify](https://www.netlify.com/).

Go is required to:
*	Use the Hugo Modules feature
*	Build Hugo from source
Please refer to the [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) and [Go](https://go.dev/doc/install) documentation for installation instructions.

## Prebuilt binaries 
Prebuilt binaries are available for a variety of operating systems and architectures. Visit the [latest release](https://github.com/gohugoio/hugo/releases/latest) page, and scroll down to the Assets section.

1.	Download the archive for the desired [edition](https://gohugo.io/installation/windows/#editions), operating system, and architecture
2.	Extract the archive
3.	Move the executable to the desired directory
4.	Add this directory to the `PATH` environment variable
5.	Verify that you have execute permission on the file
Please consult your operating system documentation if you need help setting file permissions or modifying your PATH environment variable.

If you do not see a prebuilt binary for the desired edition, operating system, and architecture, install Hugo using one of the methods described below.

## Package managers 
### Chocolatey 
[Chocolatey](https://chocolatey.org/) is a free and open source package manager for Windows. 
This will install the extended edition of Hugo:
1.	`Chocolatey` can be installed with [this guide](https://chocolatey.org/install).
2.	After the Install of choco we can use the command below to install `hugo-extended`
	```
	choco install hugo-extended
	```
	![choco install](/images/other/choco-windows-install.png)

### Scoop 
[Scoop](https://scoop.sh/) is a free and open source package manager for Windows. This will install the extended edition of Hugo:
```
scoop install hugo-extended
```

## Docker 
[Erlend Klakegg Bergheim](https://github.com/klakegg) graciously maintains [Docker images](https://hub.docker.com/r/klakegg/hugo) based on images for Alpine Linux, Busybox, Debian, and Ubuntu.
```
docker pull klakegg/hugo
```

## Build from source 
To build Hugo from source you must:

1.	Install [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
2.	Install [Go](https://go.dev/doc/install) version 1.18 or later
3.	Update your PATH environment variable as described in the [Go documentation](https://go.dev/doc/code#Command)
The install directory is controlled by the GOPATH and GOBIN environment variables. If GOBIN is set, binaries are installed to that directory. If GOPATH is set, binaries are installed to the bin subdirectory of the first directory in the GOPATH list. Otherwise, binaries are installed to the bin subdirectory of the default GOPATH ($HOME/go or %USERPROFILE%\go).

Then build and test:
```
go install -tags extended github.com/gohugoio/hugo@latest
hugo version
```
When building the extended edition of Hugo from source on Windows, you will also need to install the [GCC compiler](https://gcc.gnu.org/). See these detailed instructions.

## Comparison 
Prebuilt binaries	Package managers	Docker	Build from source	<br>
Easy to install?	✔️	✔️	✔️	✔️	<br>
Easy to upgrade?	✔️	✔️	✔️	✔️	<br>
Easy to downgrade?	✔️	✔️ 1	✔️	✔️	<br>
Automatic updates?	❌	❌ 2	❌ 2	❌	<br>
Latest version available?	✔️	✔️	✔️	✔️	<br>
Easy if a previous version is still installed. ↩︎<br>
<br>
Possible but requires advanced configuration. ↩︎ ↩︎<br>





