Relayd Wireless Bridge in OpenWRT
=================================

Sets up a wireless bridge in OpenWRT using relayd.

Steps:


Collect Info
------------

 * Router WIFI SSID & password
 * Router IP address, subnet mask: Example `192.168.100.1 / 255.255.255.0`
 * Choose an IP address in the router's subnet for the bridge: Example `192.168.100.4`
 * Choose an IP address in a different subnet for the bridge lan (used to configure the bridge itself): Example `192.168.8.1`


Set Bridge LAN IP Address
-------------------------

 * Menu -> Network -> Interfaces
 * LAN -> Click `Edit`
 * IPv4 address: Example `192.168.8.1`
 * DHCP Server -> General Setup -> Ignore Interface [X]
 * Click `Save & Apply`
 * Configure client PC to manually use 192.168.8.x address on ethernet and reconnect


Connect Bridge to Router WLAN
-----------------------------

 * Menu -> Network -> Wireless
 * Click `Scan`
 * Click `Join Network`
 * WPA passphrase: `your wifi password`
 * Click `Submit`
 * Click `Save & Apply`


Test Connection to Internet
---------------------------

 * Menu -> Network -> Diagnostics
 * Click `Ping`


Install Relayd
--------------

 * Menu -> System -> Software
 * Click `Update lists`
 * Filter: `relay`, Click `Find Package`
 * Look for `luci-proto-relay` and `relayd`
 * Check in installed packages - see if they're already installed.
 * Check in available packages - click `Install`


Add Bridge Interface
--------------------

 * Menu -> Network -> Interfaces
 * Click `Add new interface...`
 * Name of the new interface: `stabridge`
 * Protocol of the new interface: `Relay bridge`
 * Click `Submit`
 * Relay between networks: `lan:` and `wwan:`
 * Local IPv4 Address: Example `192.168.100.1`
 * Click 'Save and Apply'


Update LAN Interface
--------------------

 * Menu -> Network -> Interfaces
 * LAN -> Click `Edit`
 * IPv4 Gateway: Example `192.168.100.1`
 * Custom DNS: Example `192.168.100.1`
 * DHCP: Ignore Interface [X]


Add Firewall Zone
-----------------

 * Menu -> Network -> Firewall
 * Zones: Click `Add`
 * Name: `bridgezone`
 * Forward: `accept`
 * Covered networks: `lan:` and `wwan:`
 * Click 'Save and Apply'


Reboot bridge, change PC ethernet port back to automatic (DHCP)
