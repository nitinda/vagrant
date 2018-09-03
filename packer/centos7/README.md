# Packer

These are the packer.io templates and associated code to generate Vagrant
boxes and other images such as AWS AMI. 

There is a script included in each platform called `watch` which is used to
simply monitor if a kernel update exists for that platform. In case one does,
a new `packer build` is initiated.

The Atlas post processor is included in the builds to upload each new build to
Atlas after a successful build. In order to use this, you will need to obtain
an Atlas key and populate it in your .bashrc file -- or the relevant one for
your environment.

Internet access is required to build the boxes as the installation installs
the latest versions of the packages. If the metadata is not available, the
installation will fail.

Following software are required for this:

- VirtualBox 5.2.* (Install VirtualBox https://www.virtualbox.org/wiki/Downloads)
- Packer 1.2.* (Install Packer http://www.packer.io/downloads.html)
- Vagrant  2.1.* (Install Vagrant http://www.vagrantup.com/downloads)
- Internet access is required to build the boxes as the installation installs the latest versions of the packages. If the metadata is not available, the installation will fail.

## CentOS7
The CentOS7 Vagrant box is a minimal CentOS7 installation with Virtualbox
Guest Additions 5.1.x or the latest version of Virtualbox available at the
time of build.