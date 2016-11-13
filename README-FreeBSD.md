# FreeBSD #

This file documents the setup and configuration of a FreeBSD CI Builder
for use in the KDE CI System.

## Setup ##

 - Install FreeBSD 11-STABLE (e.g. 11.0 [1]). The base system installation
   doesn't need to have ports installed, nor system sources.
 - Enable ssh access:
     echo 'sshd_enable="YES"' >> /etc/rc.conf
     service sshd start
 - Install Java:
     pkg install openjdk8-jre
 - Install Git, CMake, GNU Make. As an *accident* this may install
   Python 2.7 as well, which is something we'll need later.
     pkg install git cmake gmake
 - Install rsync. This isn't really needed right now, since we'll
   patch out rsync for FreeBSD as long as it's not getting the 
   dependencies via rsync anyway.
     pkg install rsync
 - Install ECM (older version), which will pull in current Qt5 packages;
   then delete ECM because an up-to-date version will be built by CI.
     pkg install extra-cmake-modules # Soon kf5-extra-cmake-modules
     pkg delete extra-cmake-modules
 - Install other Qt bits:
     pkg install qt5
 - Install needed python packages:
     pkg install py27-lxml
 - Add a user (we'll call it kde):
     echo "kde::::::KDE Jenkins::sh:" | adduser -w no -f -
 - Add a private ssh key to the user:
     su - kde
     mkdir .ssh
     chmod 700 .ssh
     ssh-keygen -N '' -f .ssh/id_jenkins
     cat .ssh/id_jenkins.pub >> .ssh/authorized_keys
 - Create a directory where Jenkins can write stuff (as the user just created)
     mkdir -p /srv/jenkins/install/FreeBSD
     chown kde:kde /srv/jenkins/install/FreeBSD


## Jenkins ##

When setting up the Jenkins node for this machine:
 - Add the private key as ssh access method to the node.
 - Add an environment variable, JENKINS_SLAVE_HOME=/home/kde/scripts
   (if it's blank, some of the tools will fall over; it must be
   equivalent to ~/scripts because of assumptions in update-setup-sandbox.py)



[1] https://www.freebsd.org/releases/11.0R/announce.html


## Configuration ##

