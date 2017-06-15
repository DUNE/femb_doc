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
   or clipped onto the green ground terminal on the power supply (device labeled 
   RIGOL DP832).

2. Click the "Reset & Power Off" button.

3. Confirm that on/off buttons on power supply are *NOT* lit. This means the power 
   to the board is off and it is safe to remove ASICs. If they are still lit, try 
   step 2 again a few times. Talk to the shift leader if the power won't turn off.

4. Remove the already tested ASIC from the socket and replace it with the one to 
   be tested. Orient the ASIC so that the corner with the dot on it is nearest to 
   the marked corner of the socket. Note the ASIC ID number (the number in marker 
   on the top of the ASIC) before closing the socket.

5. Put your name, the test board ID (in marker on the circuit board with the socket),
   and the ASIC ID number in the GUI fields.

6. Press "Power-up Board".

7. Enter the CH2 current in the GUI. This is the current on the 2nd channel of the
   power supply. It is on the center column of the display with an "A" by it. It 
   is normally between 0.08 and 0.12 A. Immediately alert the shift leader if it 
   is more than 0.25 A.

8. Click "Start Test".

9. Write the Run ID displayed on the GUI in the notebook and wait for the test to run.

10. When the test completes, write Pass, Fail, or Error in the notebook.

11. If the test results in an error, leave the chip in the socket and try running
   the test again (go through the steps again). Alert the shift leader if there is an
   error again. Otherwise, go back to step one and proceed normally.
