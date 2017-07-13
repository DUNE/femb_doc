General Test-stand Expert Info
==============================

[ADC Test Board Expert Page](ADC/README.md)

Changing the FEMB_CONFIG
------------------------

Whenever a test stand is switched from one kind of test to another (ADC to or
FEMB or FE, and **warm to cold**), the FEMB_CONFIG environmental variable must
be updated. To do so, change the value exported in the oper account's .bashrc.
Then log out and log back in.

For room temperature tests:

- Quad FE Tester: FEMB_CONFIG=quadFeAsic
- Single ADC Tester on hothdaq3: FEMB_CONFIG=adcTest_P1single
- Single ADC Tester on hothdaq4: FEMB_CONFIG=adcTest_P1single_hothdaq4

For cryogenic tests:

- Quad FE Tester: FEMB_CONFIG=quadFeAsic_cold
- Single ADC Tester on hothdaq3: FEMB_CONFIG=adcTest_P1single_cold
- Single ADC Tester on hothdaq4: FEMB_CONFIG=adcTest_P1single_hothdaq4_cold

The full list of available configurations can be listed by running 
`unset FEMB_CONFIG` and then a command that requires the configuration like
`femb_init_board`.

Viewing Log Files (Sumatra)
---------------------------

Sumatra sends the log files and other info about each run to a database. Brett
setup a nice interface on hothstor2 for viewing the database. From the hothdaqs
or inside the BNL network, you should be able to access it by pointing your
browser to `http://hothstor2.phy.bnl.gov:8942/`

From outside the firewall, you need to tunnel into hothstor2 with a command
like `ssh -L 8942:localhost:8942 hothstor2` then you can point your browser to
`http://localhost:8942` to access the page.

The "label" column is not necessarily the same as the timestamp, but you can
see the timestamp in the output data column. The executable column tells you
which executable (part of the test) the entry is for. If you click on the
label, it will take you to a page that has the log file at the bottom.

Change Test-stand Software Version (Temporary)
----------------------------------------------

You can change the software version a single operator account terminal uses by
running:

```
deactivate
source /opt/sw/releases/femb_python-1.0.19/sourceme
```

where you can replace 1.0.19 with any release avaliable in that directory.

You can check the current activated version by running the `which` command and
a femb command, e.g.

```
which femb_init_board
```

The pathname printed out will include the femb_python version.

Building and Distributing a New Release to the hothdaqs and Making Default
--------------------------------------------------------------------------

If Brett has given you access to the "inst" account, then you can

```
ssh inst@hothstor2
```

You can then run 

```
./make-release.sh 1.0.19
```

to build and distribute a release (like 1.0.19) to the hothdaqs. **This does
not enable it for the oper account by default**.

If you want to enable it for the oper account by default, then run:

```
./set-production.sh 1.0.19
```

Trouble Shooting the Ethernet Interface
---------------------------------------

If you think you are having trouble talking to the board, make sure the power
supply is on, and then run:

```
femb_read_reg 0
```

If that prints an error, then you are probably having trouble talking to the
board. If it just returns some numbers, then you are able to talk to he board.

To further diagnose the problem, run

```
arp -a
```

The result should look like:

```
? (192.168.121.1) at aa:bb:cc:dd:ee:10 [ether] on enp2s0
? (172.22.22.2) at 00:13:3b:0f:a6:60 [ether] on enp0s31f6
```

The entry with (192.168.121.1) is the one that talks to the board. It should be
there and should be at an address like the one shown above. If it isn't then
you need to restart the networking. You should be able to run from the operator
account (without putting in a password):

```
sudo restart-network
```

If that doesn't work, then you can try turning off the power to the board,
shutting down the computer, waiting a moment, then turning the computer back on
(restarting doesn't do it).
