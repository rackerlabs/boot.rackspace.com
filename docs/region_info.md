## Rackspace Local Mirror

Our globally load balanced mirror is:

    mirror.rackspace.com

As it's local to the region, this is the fastest way to obtain files needed for the instance.  You can use this as a local mirror for most distributions.

### IP Addressing

The public interface of an instance gets assigned from a /24 block.  When setting up network make sure to use:

    IP: Public IP of instance (e.g. 55.54.23.23)
    Netmask: 255.255.255.0 
    Gateway: First three octets of instance with a .1 (e.g. 55.54.23.1)

### DNS IPs

#### DFW
    72.3.128.240 (cachens1.dfw1.rackspace.com)
    72.3.128.241 (cachens2.dfw1.rackspace.com)
#### ORD
    173.203.4.8 (cachens1.ord1.rackspace.com)
    173.203.4.9 (cachens2.ord1.rackspace.com)
#### IAD
    69.20.0.164 (cachens1.iad1.rackspace.com)
    69.20.0.196 (cachens2.iad1.rackspace.com)
#### LON
    83.138.151.80 (cachens1.lon.rackspace.com)
    83.138.151.81 (cachens2.lon.rackspace.com)
#### SYD
    119.9.60.62 (cachens1.syd2.rackspace.com)
    119.9.60.63 (cachens2.syd2.rackspace.com)
#### HKG
    120.136.32.62 (cachens1.hkg1.rackspace.com)
    120.136.32.63 (cachens2.hkg1.rackspace.com)