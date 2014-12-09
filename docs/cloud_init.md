## Installing Cloud-Init for Linux

_**This is pending some fixes for config-drive in Openstack around the networking before it will work properly.**_

Deb Based Distros:

    apt-get update
    apt-get install cloud-init

RPM Based:

    yum update
    yum install cloud-init

For more information about what Cloud-Init is and how it works, please reference these documents:

[Cloud-Init in Ubuntu](https://help.ubuntu.com/community/CloudInit)

[Cloud-Init Examples](http://bazaar.launchpad.net/~cloud-init-dev/cloud-init/trunk/files/head:/doc/examples/)

Cloud-Init can get its data from Rackspace Cloud via several sources:

[Config Drive (working today)](http://docs.openstack.org/trunk/openstack-compute/admin/content/config-drive.html)

[Metadata Service (dev in progress)](http://docs.openstack.org/trunk/openstack-compute/admin/content/metadata-service.html)

