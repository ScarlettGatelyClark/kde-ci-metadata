# FreeBSD #

This file documents the setup and configuration of a FreeBSD CI Builder
for use in the KDE CI System.

## Setup ##

 - Install FreeBSD 11-STABLE (e.g. 11.0 [1]). The base system installation
   doesn't need to have ports installed, nor system sources.
 - Enable ssh access:
     echo 'sshd_enable="YES"' >> /etc/rc.conf
     service sshd start

[1] https://www.freebsd.org/releases/11.0R/announce.html


## Configuration ##

