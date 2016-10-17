DUNE/SBND Cold Electronics Test-stand Documentation
===================================================

Setting up your Linux computer to run a test-stand (Ubuntu 14.04/16.04)
-----------------------------------------------------------------------

Computer IP Address for communicating with FEMB: 192.168.121.50 Mask:
255.255.255.0 (192.168.121.50/24)

First, connect your computer to the board using ethernet and power on the board.

Click on the network manager applet in the task bar and go to edit connections.
Click on wired connection and click edit. Go to the IPv4 Settings tab. Change
method to Manual. Click Add and set the Address to 192.168.121.50 and the
Netmask to 24. Then click save and close the network manager window.

Network connection debugging commands
-------------------------------------

Use the "ip address" command. One of the interfaces should have a line:

inet 192.168.121.50/24 .....

That is the ethernet interface we're using. If no interface has that IP, then
go back to the previous section.

You should check that your interface supports gigabit ethernet:

ethtool <interface name> | grep Speed

should print "Speed: 1000Mb/s"

This command should tell you that the interface is connected:

nmcli dev

Finally, this command:

arp -a

Should have an entry that looks like:

? (192.168.121.1) at aa:bb:cc:dd:ee:10 [ether] on <interface name>

That means you are able to connect to the board.

