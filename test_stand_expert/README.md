General Test-stand Expert Info
==============================

Changing the FEMB_CONFIG
------------------------

Whenever a test stand is switched from one kind of test to another (ADC to or
FEMB or FE, and **warm to cold**), the FEMB_CONFIG environmental variable must
be updated. To do so, change the value exported in the oper accounts .bashrc.
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

Building and Distributing a New Release to the hothdaqs
-------------------------------------------------------

If Brett has given you access to the "inst" account, then you can

```
ssh inst@hothstor2
```

You can then run 

```
make-release.sh 1.0.19
```

to build an distribute a release (like 1.0.19) to the hothdaqs. **This does not
enable it for the oper account by default**.
