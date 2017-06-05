ADC ASIC Test-stand Checklist
=============================

Get Software Going on a New Login
---------------------------------

1) Log into the "CE Test Operator" account.

2) Open a new terminal (Press windows key, type terminal, and press enter)

3) In the terminal, type "femb_adc_gui" and press enter

Test Procedure
--------------

Assumes GUI is already running. Try the steps in the previous section to get it going.

1. Make sure you have the anti-static bracelet on your wrist and it is plugged into 
   the green ground terminal on the power supply (device labeled RIGOL DP832).

2. Click "Reset & Power Off" button.

3. Confirm that on/off buttons on power supply are *NOT* lit. This means the power 
   to the board is off and it is safe to remove ASICs. If they are still lit, try 
   step 2 again a few times. Talk to the shift leader if the power won't turn off.

4. Remove the already tested ASIC from the socket, and replace it with the one to 
   be tested. Note the ASIC ID number (the nuber in marker on the top of the ASIC)
   before closing the socket.

5. Put your name, the test board ID (in marker on the circuit board with the socket),
   and the ASIC ID number in the GUI fields.

6. Press "Power-up Board".

7. Enter the CH2 current in the GUI. This is the current on the 2nd channel of the
   power supply. It is on the center column of the display with an "A" by it.

8. Click "Start Test".

9. Write the Run ID displayed on the GUI in the notebook and wait for the test to run.

10. When the test completes, write Pass, Fail, or Error in the notebook.

