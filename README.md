## boot.rackspace.com

### What is boot.rackspace.com?

boot.rackspace.com is a collection of iPXE scripts that allow you to rapidly network boot Operating Systems, Utilities and other tools very easily.  It allows you the flexibility of booting installations without having to go download the entire installation media.  It's especially useful for environments when you don't want to utilize a Virtual CD in a Dell DRAC, HP iLO or some other type of remote tool.  It's a quick installation menu available anywhere on any system.  

### Getting started
#### NIC with Embedded iPXE

If your system has iPXE integrated in your network cards ROM, you can enter iPXE's CLI by entering CTRL-B when prompted and then load boot.rackspace.com by doing:

    dhcp
    chain http://boot.rackspace.com/menu.ipxe

If you don't have DHCP on your network, you can manually set your network information:

    set net0/ip <IP>
    set net0/netmask <netmask>
    set net0/gateway <gateway>
    set dns <nameserver>
    ifopen net0
    chain http://boot.rackspace.com/menu.ipxe

#### Boot from Rackspace Cloud Servers

Each region in Rackspace Cloud Servers contains an image called "boot.rackspace.com".  When creating a new instance, specify this image as the image to boot from, select the size of the instance you want, and then boot.  The instance creation will attach a small 1MB iPXE iso to the instance and boot from it.  

Because the iPXE iso doesn't have an agent, the instance will remain in build until the system times out and flips it to active.  You don't have to wait for the instance to go active however to begin working with iPXE.  Once you've booted the instance, you can attach to it with the console.  You'll need to input the address of the instance into the console so that the instance can access the network.

Once you've inputted the correct IP and DNS information, the instance should chainload onto boot.rackspace.com where you can begin customizing the instance.  This method is ideal for image builders and people who love to tinker.

#### Boot from iPXE ISO

Obtain ISO image here: 

    wget http://boot.rackspace.com/ipxe/ipxe.iso

To create a bootable CD-ROM, burn the ISO image ipxe.iso (1MB in size) to a blank CD-ROM.  You can also use this ISO file as a virtual CD device in Citrix XenServer, VMware ESXi, VMware Fusion, VirtualBox, or even in a Dell DRAC or HP iLOs virtual CD drive.

#### Boot from iPXE USB

Obtain DSK image here:

    wget http://boot.rackspace.com/ipxe/ipxe.dsk

*Warning: Backup your important data before using USB as it will overwrite anything on the USB key.*

Insert a USB disk, find it's device name of USB. Then use following command: 

    cat ipxe.dsk > /dev/sdX 

or
    
    dd if=ipxe.dsk of=/dev/sdX 

where sdX is your usb drive.  Substitute /dev/sdX for /dev/fd0 in the case of using a floppy.

#### Updates to boot.rackspace.com menus

Pull requests are welcome and encouraged.  Feel free to issue a pull request for new versions or tools that you might find useful.  boot.rackspace.com will be deployed automatically with the latest github changes once they've been accepted.

#### iPXE Images

All iPXE boot images are regenerated every time a commit occurs to the [iPXE project on Github](https://github.com/ipxe/ipxe) so that the images always have the latest and greatest updates.  It's merged with the [osimages branch](https://github.com/osimages/ipxe/tree/osimages) with the only deviations right now being the menu [color scheme](https://github.com/osimages/ipxe/blob/osimages/src/config/colour.h).  The images are generated and embedded with these [scripts](https://github.com/amesserl/rackspace.com/tree/master/ipxe).

* [boot.rackspace.com-main](https://github.com/boot_rax/rackspace.com/tree/master/ipxe/boot.rackspace.com-main) - Uses DHCP
* [boot.rackspace.com-static](https://github.com/boot_rax/rackspace.com/tree/master/ipxe/boot.rackspace.com-static) - Uses Static only
* [boot.rackspace.com-prompt](https://github.com/amesserl/rackspace.com/tree/master/ipxe/boot.rackspace.com-prompt) - Prompts what type of network you want to boot. [ TODO ]

#### What Operating Systems are currently available on boot.rackspace.com?

* ArchLinux
* CentOS
* Debian
* Fedora
* Gentoo
* OpenSUSE
* TinyCoreLinux
* Ubuntu
* Windows 2012 Preinstallation Environment [Experimental, not of use to anyone except me yet]

#### What Utilities are currently available on boot.rackspace.com?

* [Clonezilla](http://www.clonezilla.org/)
* [HDT](http://www.hdt-project.org/)
* [Memtest](http://www.memtest.org/)

#### Updates to boot.rackspace.com menus

Pull requests are welcome and encouraged.  Feel free to issue a pull request for new versions or tools that you might find useful.  boot.rackspace.com will be deployed automatically with the latest github changes once they've been accepted.
