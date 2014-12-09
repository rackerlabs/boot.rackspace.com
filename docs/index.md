## What is boot.rackspace.com?

boot.rackspace.com is a collection of iPXE scripts that allow you to rapidly network boot Operating Systems, Utilities and other tools very easily.  It allows you the flexibility of booting installations without having to go track down and download installation media.  It's especially useful for remote access environments when you don't want to utilize remote attach CD in a Dell DRAC, HP iLO or some other type of remote tool.  It's also a great tool for bootstrapping your own custom installation on a Cloud Server from scratch!

### Getting started

Each region in Rackspace Cloud Servers contains an [image](image_uuids.md) named "iPXE Boot (boot.rackspace.com)".  When creating a new Performance Flavor instance (does not currently work on Standard Flavors, coming soon!), specify this image as the image to boot from, select the size of the instance you want, and then boot.  The instance creation will attach a small 1MB iPXE iso to the instance and boot from it.  

Once you've booted the instance, you can attach to it with the console.  The networking information of the instance is automatically set so you should drop right into the menu.  In the event automation fails, you'll be prompted for the networking information of the instance.

The instance should chainload onto boot.rackspace.com where you can begin customizing the instance.  This method is ideal for image builders and people who love to tinker.  For more information on building a Rackspace custom image, see the [image creation document](image_creation.md).

### Booting Methods
#### NIC with Embedded iPXE

If your system has iPXE integrated in your network cards ROM, you can enter iPXE's CLI by entering CTRL-B when prompted and then load boot.rackspace.com by doing:

    dhcp
    chain http://boot.rackspace.com/menu.ipxe

If you don't have DHCP on your network, you can manually set your network information:

    set net0/ip <ip>
    set net0/netmask <netmask>
    set net0/gateway <gateway>
    set dns <nameserver>
    ifopen net0
    chain http://boot.rackspace.com/menu.ipxe

#### Boot from iPXE ISO

Obtain ISO image here: 

    wget http://boot.rackspace.com/ipxe/boot.rackspace.com-main.iso

To create a bootable CD-ROM, burn the ISO image ipxe.iso (1MB in size) to a blank CD-ROM.  You can also use this ISO file as a virtual CD device in Citrix XenServer, VMware ESXi, VMware Fusion, VirtualBox, or even in a Dell DRAC or HP iLOs virtual CD drive.

#### Boot from iPXE USB

Obtain DSK image here:

    wget http://boot.rackspace.com/ipxe/boot.rackspace.com-main.dsk

*Warning: Backup your important data before using USB as it will overwrite anything on the USB key.*

Insert a USB disk, find it's device name of USB. Then use following command: 

    cat ipxe.dsk > /dev/sdX 

or
    
    dd if=ipxe.dsk of=/dev/sdX 

where sdX is your usb drive.  Substitute /dev/sdX for /dev/fd0 in the case of using a floppy.

### iPXE Images

All iPXE boot images are regenerated every time a commit occurs to the [iPXE project on Github](https://github.com/ipxe/ipxe) so that the images always have the latest and greatest updates.  It's merged with the [osimages branch](https://github.com/amesserl/ipxe/tree/osimages) with the only deviations right now being the menu [color scheme](https://github.com/amesserl/ipxe/blob/osimages/src/config/colour.h).

* [boot.rackspace.com-main](https://github.com/rackerlabs/boot_rax/blob/master/ipxe/boot.rackspace.com-main) - Uses DHCP
* [boot.rackspace.com-static](https://github.com/rackerlabs/boot_rax/blob/master/ipxe/boot.rackspace.com-static) - Uses Static only

### Operating Systems

#### What Operating Systems are currently available on boot.rackspace.com?

* [ArchLinux](https://www.archlinux.org)
* [CentOS](https://centos.org)
* [Debian](https://debian.org)
* [Fedora](https://fedoraproject.org)
* [FreeBSD](https://freebsd.org)
* [Gentoo](https://gentoo.org)
* [OpenBSD](http://openbsd.org)
* [OpenSUSE](http://opensuse.org)
* [Scientific](http://scientificlinux.org)
* [TinyCoreLinux](http://distro.ibiblio.org/tinycorelinux/)
* [Ubuntu](http://www.ubuntu.com/)

#### Experimental Operating Systems

* [boot2docker](https://github.com/boot2docker/boot2docker)
* [CoreOS](https://coreos.com/)

### Utilities

#### What Utilities are currently available on boot.rackspace.com?

* [Clonezilla](http://www.clonezilla.org/)
* [HDT](http://www.hdt-project.org/)
* [Memtest](http://www.memtest.org/)

### Contributing

Pull requests are welcome and encouraged.  Feel free to issue a pull request for new versions or tools that you might find useful.  boot.rackspace.com will be deployed automatically with the latest github changes once they've been accepted.

Feel free to open up an issue on github or contact us via <bootrax@rackspace.com>.
