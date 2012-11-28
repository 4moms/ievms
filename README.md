# Note

This is a fork, not the main repo.

Please don't submit issues or pull requests here.

Main repo is at https://github.com/xdissent/ievms

# Installation

## Get this repository

    git clone git@github.com:4moms/ievms
    cd ievms
    git checkout add-argument

## (Optional) Add ievms.sh into your PATH

    mkdir -p ~/bin
    ln -s $(pwd)/ievms.sh ~/bin/

## Get the cached copies of the VMs

### Mount the fileserver

    sudo mkdir -p /storage01/4moms
    sudo chown $LOGNAME $_
    mount -t smbfs //$LOGNAME@storage01.thorleyindustries.com/4moms /storage01/4moms

### Get the VMs

    rsync -PzrtvR --modify-window=10 /storage01/4moms/Software\ Development/./.ievms ~

## Install each version

Available: 6, 7, 8, or 9.  Run `ievms.sh $version(s)`, e.g. to install 7 and 9:

    ievms.sh 7 9
