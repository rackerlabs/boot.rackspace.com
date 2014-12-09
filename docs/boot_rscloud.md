### Rackspace Cloud Servers

Launch a _**Performance Cloud Server**_ from the [API](http://docs.rackspace.com/servers/api/v2/cs-gettingstarted/content/section_gs_install_nova.html) with the Image UUID of:

    9aa0d346-c06f-4652-bbb1-4342a7d2d017

_Note: Standard, Compute Optimized, and Memory Optimized are currently not supported._

Once the server starts pinging on IPv4, it's ready to access via the console.  

Once in the console, you should see the boot.rackspace.com menu.  From there, you can select your OS and install it the way you want to.  You can follow this guide [here](image_creation.md).

Once the installation has completed and the instance reboots, reconnect to the console and you'll be back at the menu.  If you boot from local disk, that will then boot you into the OS.  From there you'll set up the Xentools, Agent, etc.  Once you're ready, you can take a snapshot of that image.  

Before redeploying that image, you'll want to set the metadata on the image as specified in the guide for the mode you desire.  If you don't take a snapshot of the image, the boot.rackspace.com ISO will always boot first.  The server should be used to get the OS disk the way you want so that you can snapshot it and redeploy without the boot.rackspace.com tool.
