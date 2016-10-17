DUNE/SBND Cold Electronics Test-stand Documentation
===================================================

Setting up your Linux computer to run a test-stand
--------------------------------------------------

Computer IP Address for communicating with FEMB: 192.168.121.50 Mask:
255.255.255.0 (192.168.121.50/24)

Use the "ip address" command to find the network device without an assigned IP.
That is the interface name you want to try using. To give it the static IP we want:

sudo ip address add 192.168.121.50/24 dev <interface name>
