# Debian package for Mathematica

## Description

Debian rules to generate a Debian package for [Mathematica](https://www.wolfram.com/mathematica/) for amd64 architecture. The Mathematica installer `Mathematica_*_LINUX.sh` corresponding to the version in changelog has to be provided to build the package.

The generated Debian package:
- installs Mathematica in `/opt/mathematica`
- adds links to executables in `/usr/bin`
- adds icons, mimes and desktop menu entries in the corresponding directory in `/usr/share`
- adds license file if provided

A license file `mathpass` has to be provided to use Mathematica either next to the installer in order to be included in the package or need to be added in `/opt/mathematica/Configuration/Licensing/` after the package is installed. To use a network license server the `mathpass` is simply:

    !hostname-or-ip-of-license-server


Inspired by [Mathematica Arch Linux PKGBUILD](https://aur.archlinux.org/packages/mathematica).

## Package build

1. Define the desired version:

        export VERSION=13.2.0

2. Clone the git repository containing the packages rules in an empty directory:

        git clone -b $VERSION https://github.com/guillod/deb-mathematica.git mathematica-$VERSION
        cd mathematica-$VERSION

3. Put the Mathematica installer `Mathematica_$VERSION_BNDL_LINUX.sh` (if you want to include the documentation) or `Mathematica_$VERSION_LINUX.sh` (if you want online documentation only) in the current directory (`mathematica-$VERSION`).
4. Optionally, put a `mathpass` file (network license server) in the same directory in order to include it in the package.
5. Generate the package for example with:

        debuild --no-lintian -i -b -uc -us

    or `sbuild` (note you can speed up the creation of the source archive using `--dpkg-source-opts="-Zgzip -z1"`).

## Installation

Once generated, the package `mathematica_$VERSION_amd64.deb` can be installed for example with:

    sudo apt install ../mathematica_$VERSION_amd64.deb


## Contact

For comments, issues, bug-reports and requests, please use the issue tracker of the current repository. Otherwise the principal author can be reached at:

    Julien Guillod
    julien.guillod CHEZ sorbonne-universite.fr
    https://guillod.org/
    Department of Mathematics
    Sorbonne University
    France
