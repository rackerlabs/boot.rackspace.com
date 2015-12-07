## Rackspace Cloud Image Creation

This guide will walk you through utilizing the boot.rackspace.com tool to create an instance with an Operating System the old fashioned way so that you can fully customize the image as you see fit.

### Getting started

Launch an instance with the boot.rackspace.com image.  Because we're utilizing the virtual CD device to boot via iPXE, the instance has to be booted in HVM mode.  Once the instance goes Active, connect to the console.  If prompted for IP information, enter in the IP, netmask, gateway, and DNS and that should launch you into the main boot.rackspace.com menu.  (note, we're currently working on the automation to bypass networking entry) Once you're in the menu, select the OS you want to install.  That will load up the installer kernels from mirror.rackspace.com and boot you into the installer.

**Note:** When making an image, it's usually best to create the image on the smallest flavor.  This allows you the flexibility to deploy the image to any other flavor type.

### Installing the Operating System
#### Partitioning

By default Performance Cloud Servers receive an OS volume and up to four data volumes.  In some cases you may also have a config drive attached.

    OS Volume: /dev/xvda (PV) or /dev/sda (HVM)
    Config Drive (Read Only): /dev/xvdd (PV) or /dev/sdd (HVM)
    Ephemeral Drives (drives 'e' and on): /dev/xvde (PV) or /dev/sde (HVM) 

Make sure to install the OS to the appropriate OS volume.

#### GRUB
Because the instance is in HVM mode at this point, it will attempt to set up GRUB and generate an MBR on the virtual disk.  Make sure that Grub is installed to the OS Volume.  

#### Reboot
Once the installation has completed, the server will reboot.  The instance will attempt to load iPXE again.  At this point, you can press CTRL-C to bypass the menu if it's prompting for the networking information or  select Local Boot to boot from the newly installed OS.  The OS should boot at this point.  The timeout on the menu is currently set to five minutes.

### Preparing the Instance for Snapshotting
### Install XenTools
The XenTools are needed for communication between the host and the guest for configuration via the xenstore. You can grab the latest versions of XenTools Rackspace uses here:

* [XenServer 6.0.0 Tools](http://boot.rackspace.com/files/xentools/xs-tools-6.0.0.iso)
* [XenServer 6.1.0 Tools](http://boot.rackspace.com/files/xentools/xs-tools-6.1.0.iso)
* [XenServer 6.2.0 Tools](http://boot.rackspace.com/files/xentools/xs-tools-6.2.0.iso)
* [XenServer 6.5.0 Tools](http://boot.rackspace.com/files/xentools/xs-tools-6.5.0-20200.iso)

##### To install the tools on Linux:

    mkdir tmp
    mount -o loop xs-tools-6.0.0.iso tmp
    cd tmp/Linux
    ./install.sh
    cd ../..
    umount tmp

#### Instance Configuration Services

Select the appropriate configuration service you want to use:

[Using Nova Agent for Linux](nova_agent.md)

[Using Cloud Init for Linux](cloud_init.md)

#### Cleaning up files on the instance
Typically you'll want to remove log files from the instance, remove history, remove ssh_host keys and etc before taking the snapshot.  This leaves you with a clean, pristine image to start from.

#### Taking a Snapshot
Once you've configured the instance, you can then initiate a snapshot of the instance.  The snapshot only includes the disk and doesn't include the iPXE ISO so deploying the snapshot will boot right into the instance without intervention being needed from the console.

#### Applying Metadata to Image

    nova image-meta <image> <action> <key=value> [<key=value> ...]

* Set vm_mode to:
  * "xen" for a Paravirtualized (PV) Instance.  For most Linux VMs, PV is typically the best option.
  * "hvm" for HVM Mode, typically used for FreeBSD, Linux PVHVM and Windows.  When using with Linux, make sure you're using one of the newer 3.x kernels for the best experience.
* If using Nova Agent:
  * Set xenapi_use_agent=true
* If using Cloud-Init exclusively, the Agent isn't needed, so make sure to disable it so that the build isn't actively polling for responses from the Nova Agent:
  * set xenapi_use_agent=false

### Deploying Image
At this point you should be able to boot from the snapshot once it completes its save to Cloud Files and goes Active.

**Note**: _If using Cloud-Init make sure to specify the config-drive on boot._

    nova boot --config-drive=true --image <image-uuid> --flavor <flavor> instance-name
