Permissions for USB devices
===========================

If you plug in a signal generator, and you get permission denied errors trying
to talk to it over USB:

First, use "lsusb" to find the vendor and product code of your device. An
example line for a Rigol function generator:

Bus 002 Device 006: ID 1ab1:0641 Rigol Technologies 

Now, create a new file:

/etc/udev/rules.d/usbtmc.rules

and add this line to it:

SUBSYSTEMS=="usb", ATTRS{idVendor}=="1ab1", ATTRS{idProduct}=="0641", GROUP="<user group>", MODE="0666"

Make sure that the idvendor and idproduct codes match the ones you found by
running lsusb. Also, change the group to your user's group so that you can
access it.
