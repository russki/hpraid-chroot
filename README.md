hpraid-chroot
=============
HP Array hpacucli chroot to use in kickstarts

# Why
hpacucli is a CLI tool that allows you to configure HP Arrays.

Unfortunately it cannot be used in kickstarts as it requires bunch of libraries and binaries that are not available in %pre part of kickstart 

This is a self-contained Centos 6 x86_64 hpacucli so you can use it your %pre of kickstarts to configure arrays

# How to use it in your %pre script

* cd /tmp;
* wget --no-check-certificate -O hpraid.tar.gz https://github.com/russki/hpraid-chroot/blob/master/hpraid.tar.gz;
* tar xzf hpraid.tar.gz;
* mount -t proc proc hpraid/proc;
* mount -t sysfs sysfs hpraid/sys;
* mount --bind /dev hpraid/dev;
* CLI='chroot hpraid /usr/sbin/hpacucli'
* $CLI "controller slot=0 show"

# Build a newer version on your own Centos 6 x86_64 box

### Get new rpm

Go to http://h18000.www1.hp.com/products/servers/proliantstorage/software-management/acumatrix/

Get HP Array Configuration Utility CLI for Linux, 64bit RPM

### Run the script to generate the new hpraid.tar.gz

* wget ftp://ftp.hp.com/pub/softlib2/software1/pubsw-linux/p1257348637/v77370/hpacucli-9.30-15.0.x86_64.rpm
* ./mk_chroot_hpacucli hpacucli-9.30-15.0.x86_64.rpm

Upload this new hpraid.tar.gz to wherever you want to use it later in your kickstart

# Changelog
12/14/12 hpraid.tar.gz is built with hpacucli-9.30-15.0.x86_64.rpm
