Advanced Package Tool
=====================

Various tips on debian's *apt* utilities like `apt-get`, `apt-cache`, `apt-file`, `dpkg`, etc.

/etc/apt/sources.list
---------------------

- `netselect`:
  A program which determines the fastest server from a list of hosts given on the command line.

- `netselect-apt`:
  A program which generates a sources.list file using the best debian mirror.

The `netselect-apt` program can be found in the `netselect` source package.
To install the `netselect` source package,
add appropriate `deb-src` lines to `/etc/apt/sources.list`, for example:

    deb-src http://http.us.debian.org/debian testing main contrib non-free
    deb-src http://non-us.debian.org/debian-non-US testing/non-US main contrib non-free

and then after:

    apt-get update
    apt-get source netselect

The above procedure will generate a directory with the netselect source, named for example `netselect-0.3.ds1`.

To generate a `sources.list` file for the testing distribution,
run `./netselect-0.3.ds1/netselect-apt testing`.

Install/remove
--------------

Example commands:

    # Install pkg1 and remove pkg2.
    apt-get install pkg1 pkg2-
    
    # Remove pkg1 and install pkg2.
    apt-get remove pkg1 pkg2+

    # Install pkg from distribution dist. 
    apt-get -t dist install pkg
    
    # Install a specific version of a package.
    apt-get install package=version
    
The `-u` flag causes APT to show the complete list of packages which will be upgraded
(when doing `apt-get upgrade` or `apt-get dist-upgrade`).

Search
------

Example commands:

    apt-cache search regexp
    apt-cache show pkg
    apt-cache showpkg pkg
    COLUMNS=132 dpkg -l pattern
    
    # Search for a filename in installed packages.
    dpkg -S file
    
    # List files installed from package.
    dpkg -L package
    
    # Update the database of files all packages contain.
    apt-file update
    
    # Search for a filename in all packages.
    apt-file search file

Using source packages
---------------------

Example commands:

    apt-get source pkgname
    
    # Automatically build the downloaded package.
    apt-get -b source pkgname
    
    # Build the package later, do this from within the directory
    # that was created after downloading the source package.
    dpkg-buildpackage -rfakeroot -uc -b
    
    dpkg -i file.deb
    
    # Install the packages required for pkg to be built. 
    # (Sources must be installed separately by apt-get source.)
    apt-get build-dep pkg

Miscellaneous
-------------

Example commands:

    # Lists available package versions with distribution.
    apt-show-versions
    
    # Display a list of upgradeable packages.
    apt-show-versions -u
    
    apt-cache depends pkgname
    
    apt-cache rdepends pkgname

Speeding up apt-get install:

  [apt-fast](https://github.com/ilikenwf/apt-fast) is a shell wrapper around apt-get (and aptitude) and utilizes aria2 to speed-up apt-get installs. You can use PPA for ubuntu and/or install manually by referring to [README](https://github.com/ilikenwf/apt-fast/blob/master/README.md).

Resources
---------

- `apt-cache search -n ^apt-`
- [Debian Documentation Project][1]
- [APT HOWTO][2]

[1]: http://www.debian.org/doc/ddp
[2]: http://www.debian.org/doc/manuals/apt-howto/index.en.html
