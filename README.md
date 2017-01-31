DUNE/SBND Cold Electronics Test-stand Documentation
===================================================

Setting up your Linux computer to run a test-stand (Ubuntu 14.04/16.04)
-----------------------------------------------------------------------

Computer IP Address for communicating with FEMB: 192.168.121.50 Mask:
255.255.255.0 (192.168.121.50/24)

First, connect your computer to the board using ethernet and power on the board
(use a normal, not "cross-over" cable).

Make sure your computer's firewall is disabled. On Ubuntu, run `sudo ufw disable`.
On Scientific Linux 7, run `systemctl disable firewalld`.

On Ubuntu, click on the network manager applet in the task bar and go to edit
connections.  Click on wired connection and click edit. Go to the IPv4 Settings
tab. Change method to Manual. Click Add and set the Address to 192.168.121.50
and the Netmask to 24. Then click save and close the network manager window.

On Scientific Linux 7, click on the button in the upper right hand corner of
the desktop, then click on wired and then wired settings. Click on the gear
icon. Now click on IPv4 on the left side. Now you can enter the ip address and
mask.

Network connection debugging commands
-------------------------------------

Use the `ip address` command. One of the interfaces should have a line:

inet 192.168.121.50/24 .....

That is the ethernet interface we're using. If no interface has that IP, then
go back to the previous section. (Newer versions of Linux use a naming scheme
where ethernet devices start with the letter "e")

You should check that your interface supports gigabit ethernet:

```
ethtool <interface name> | grep Speed
```

should print "Speed: 1000Mb/s"

This command should tell you that the interface is connected:

```
nmcli dev
```

Finally, this command:

```
arp -a
```

Should have an entry that looks like:

```
? (192.168.121.1) at aa:bb:cc:dd:ee:10 [ether] on <interface name>
```

That means you are able to connect to the board.

