Script to automatically backup and restore installed apps in Ubuntu.

# Using apt-mark

apt-mark handles various settings for packages. We can separate our backup files in two files:

One will hold the packages installed automatically
Other file will hold the packages we install manually

# Create backup list
Creates backup using following commands:

## apt-mark showauto
showauto is used to print a list of automatically installed packages with each package on a new line. All automatically installed packages will be listed if no package is given. If packages are given only those which are automatically installed will be shown.

## apt-mark showmanual
showmanual can be used in the same way as showauto except that it will print a list of manually installed packages instead.
So we create these two files:

```shell
apt-mark showauto > pkgs_auto.lst
apt-mark showmanual > pkgs_manual.lst
```

# Restore apps
Then we restore the files in the target machine:

## apt-mark auto
auto is used to mark a package as being automatically installed, which will cause the package to be removed when no more manually installed packages depend on this package.

## apt-mark manual
manual is used to mark a package as being manually installed, which will prevent the package from being automatically removed if no other packages depend on it.


```shell
sudo apt-mark auto $(cat pkgs_auto.lst)
sudo apt-mark manual $(cat pkgs_manual.lst)
```

# Installation
Place /etc/rc.local file from this project to systems /etc/rc.local.
Script will automatically run at the start of system.
