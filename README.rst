NOTE
====

This is a fork, not the main repo.

Please don't submit issues or pull requests here.

Main repo is at https://github.com/xdissent/ievms

Installation
=============

    * Get this repository::

        git clone git@github.com:4moms/ievms
        cd ievms
        git checkout add-argument
        mkdir -p ~/bin
        ln -s $(pwd)/ievms.sh ~/bin/

    * Mount the fileserver::

        sudo mkdir -p /storage01/4moms
        sudo chown $LOGNAME $_
        mount -t smbfs //$LOGNAME@storage01.thorleyindustries.com/4moms /storage01/4moms

    * Get the VMs::

        rsync -PzrtvR --modify-window=10 /storage01/4moms/Software\ Development/./.ievms ~

    * Installation for each version (version = 6, 7, 8, or 9) e.g. 7 and 9::

        ievms.sh 7 9

Overview
========

Microsoft provides virtual machine disk images to facilitate website testing 
in multiple versions of IE, regardless of the host operating system. 
Unfortunately, setting these virtual machines up without Microsoft's VirtualPC
can be extremely difficult. The ievms scripts aim to facilitate that process using
VirtualBox on Linux or OS X. With a single command, you can have IE6, IE7, IE8
and IE9 running in separate virtual machines.

(Removed Pledgie link since this is not the main repo)

Requirements
============

* VirtualBox (http://virtualbox.org)
* Curl (Ubuntu: ``sudo apt-get install curl``)
* Linux Only: unrar (Ubuntu: ``sudo apt-get install unrar``)
* Patience


Installation
============

1. Install VirtualBox.

2. Download and unpack ievms:

   * Install IE versions 6, 7, 8 and 9.

         curl -s https://raw.github.com/xdissent/ievms/master/ievms.sh | bash

   * Install specific IE versions (IE7 and IE9 only for example):

         curl -s https://raw.github.com/xdissent/ievms/master/ievms.sh | IEVMS_VERSIONS="7 9" bash

3. Launch Virtual Box.

4. Choose ievms image from Virtual Box.

5. Install VirtualBox Guest Additions (pre-mounted as CD image in the VM).

6. **IE6 only** - Install network adapter drivers by opening the ``drivers`` CD image in the VM.

.. note:: The IE6 network drivers *must* be installed upon first boot, or an
   activation loop will prevent subsequent logins forever. If this happens, 
   restoring to the ``clean`` snapshot will reset the activation lock.

The VHD archives are massive and can take hours or tens of minutes to 
download, depending on the speed of your internet connection. You might want
to start the install and then go catch a movie, or maybe dinner, or both. 

Once available and started in VirtualBox, the password for ALL VMs is "Password1".


Recovering from a failed installation
-------------------------------------

Each version is installed into a subdirectory of ``~/.ievms/vhd/``. If the installation fails
for any reason (lost Internet connection, for instance), delete the version-specific subdirectory
and rerun the install.

If nothing else, you can delete ``~/.ievms`` and rerun the install.


Specifying the install path
---------------------------

To specify where the VMs are installed, use the INSTALL_PATH variable:

    curl -s https://raw.github.com/xdissent/ievms/master/ievms.sh | INSTALL_PATH="/Path/to/.ievms" bash


Features
========

Clean Snapshot
    A snapshot is automatically taken upon install, allowing rollback to the
    pristine virtual environment configuration. Anything can go wrong in 
    Windows and rather than having to worry about maintaining a stable VM,
    you can simply revert to the ``clean`` snapshot to reset your VM to the
    initial state.

    The VMs provided by Microsoft will not pass the Windows Genuine Advantage
    and cannot be activated. Unfortunately for us, that means our VMs will
    lock us out after 30 days of unactivated use. By reverting to the 
    ``clean`` snapshot the countdown to the activation apocalypse is reset,
    effectively allowing your VM to work indefinitely.


License
=======

None. (To quote Morrissey, "take it, it's yours")
