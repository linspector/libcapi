# Modular libcapi20

## Configuration

libcapi20 features autodetection of connected CAPI
devices. In case you need to select a special device
use the remote configuration file:

 > ~/.capi20rc

if it doesn't exist look for

 > /etc/capi20.conf

To set the remote machine, the above file need to have
the following line
 > REMOTE <driver> <remote hostname|ip-address> <remote port>

Drivers:
* fritzbox	- Remote CAPI via FRITZ!Box
* rcapi		- Melware Remote CAPI

If this doesn't exist, the library tries the old, normal way
of using the local /dev/isdn/capi20.
