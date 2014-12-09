## Nova Agent Install for Linux
The Nova Agent is used for configuration of the instance.  It handles detection of the Operating System type and sets the appropriate networking configuration.  It also handles password resets, configuration of any licensing for Red Hat and Windows, versioning, and the ability to handle updates of itself.  The XenTools are required in order for the Agent to work.  You can obtain the latest version here:

[Nova Agent 0.0.1.39 - Linux](http://boot.rackspace.com/files/nova-agent/nova-agent-Linux-x86_64-1.39.0.tar.gz)

[Nova Agent 0.0.1.39 - FreeBSD](http://boot.rackspace.com/files/nova-agent/nova-agent-FreeBSD-amd64-1.39.0.tar.gz)

##### To install nova-agent:

Download the agent to the / directory:

    cd ~/ 
    mkdir nova-agent 
    cd nova-agent 
    wget http://url/nova-agent-Linux-i686-0.0.1.39.tar.gz

Extract the tar and run the installer script:

    tar xzf nova-agent-Linux-i686-0.0.1.39.tar.gz
    ./installer.sh

Inject the LSB-Headers into the init Script (If NOT already there)

    sed '1i### BEGIN INIT INFO\n# Provides: Nova-Agent\n# Required-Start: $remote_fs $syslog\n# Required-Stop: $remote_fs $syslog\n# Default-Start: 2 3 4 5\n# Default-Stop: 0 1 6\n# Short-Description: Start daemon at boot time\n# Description: Enable service provided by daemon.\n### END INIT INFO\n' /usr/share/nova-agent/1.39.0/etc/generic/nova-agent > /usr/share/nova-agent/1.39.0/etc/generic/nova-agent.lsb

Move the init script in place and make it executable:

    cp -av /usr/share/nova-agent/1.39.0/etc/generic/nova-agent.lsb /etc/init.d/nova-agent
    chmod +x /etc/init.d/nova-agent 

Finally, set the script to start automatically in the event of a reboot.
For RHEL, CentOS, Fedora, OpenSuse:

    chkconfig nova-agent on

For Debian, Ubuntu:

    update-rc.d -f nova-agent defaults 

After installation, ensure that the init script works properly and that the agent fires up on restarting of the init script.  Check to make sure the nova-agent is running and check the logs here /var/log/nova-agent.log to ensure that the nova-agent has started up.  If the image is captured without nova-agent installed, the next boot will failure to configure the instance. 

The agent source is available here:
[Openstack Nova Guest Agent](https://github.com/rackerlabs/openstack-guest-agents-unix)

