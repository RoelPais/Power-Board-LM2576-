# Power-Board-LM2576-
PCB design of a power board made using LM2576.

The board uses the LM2576 IC series to provide two 3.3V, two 5V, one 12V, one 15V and two adjustable outputs from a 11.1V (3 cell) and a 22.2V (6 cell) battery source. A max current rating of 3A and provided with 8 fuses for each individual input to a channel. 

From the 11.1V source, the available channels are 3.3V, 5V and an adjustable output.
From the 22.2V source, the available channels are 3.3V, 5V, 12V, 15V and an adjustable output.
The adjustable output can provide a voltage between 1.23 and 37V +-4%.

The components used for each circuit consist of an input capacitor, a catch diode, an inductor and an output capacitor, chosen according to the instructions given in the datasheet.

The configuration of the ICs in general are as follows:
Vin - The supply input pin to the IC is connected to the input screw terminal and the input capacitors.
OUTPUT - The output pin of the IC is connected to the inductor and catch diode and to the output screw terminal.
GROUND - The ground pin of the IC is connected to the GND of the output terminal and the input terminal via the copper pour.
FEEDBACK - The feedback pin of the IC is directly connected to the inductor and the output capacitor in case of the fixed output voltage version and whereas in the adjustable output voltage versions the feedback is connected to a voltage divider formed by the potentiometer and the resistor to set the Vout.
ON/OFF - The ON/OFF trigger pin for the IC is connected to the GND via the copper pour and hence the ICs are permanently enabled, with no delay.

Input Capacitor:
To maintain stability, a 100uF, 35V aluminum electrolytic capacitor near the regulator input pin provides sufficient bypassing. The value remains the same for the adjustable output and fixed output versions. 

Inductor Selection:
According to the inductor value selection guides mentioned in the datasheet 8.4 through 8.8, the inductor value is chosen and an appropriate inductor of 52khz switching frequency and current rating of 1.15 times the load (1.15*3A = 3.45A), is used.

For 11.1V input,
68uH for 3.3V output
68uH for 5V output
100uH for Adjustable output

For 22.2V input,
100uH for 3.3V output
100uH for 5V output
150uH for 12V output
150uH for 15V output
100uH for Adjustable output


Output Capacitor:
The output capacitor is required to filter the output voltage and is needed for loop stability. Since low ESR type capacitors are recommended for low output ripple voltage and good stability, a larger value electrolytic capacitor (1000uF) than what is required, is used, as lower capacitor values allow typically 50mV to 150mV of output ripple voltage, while the larger value capacitor is capable of reducing the ripple to approximately 20mV to 50mV. The voltage rating of the capacitor is 35V as it satisfies the condition of being at least 1.5 times greater than the output voltage, but once again higher voltage electrolytic capacitors generally have lower ESR numbers, and for this reason a capacitor rated for a higher voltage than would normally be needed is chosen.

Catch Diode:
Since buck regulators require a diode to provide a return path for the inductor current when the switch is off, the diode is placed close to the IC and the GND connection between the anode of the diode, the 3rd pin of the IC and the output capacitor is made as short as possible as mentioned in the datasheet. A 1N5822 diode is used as it works for both the input voltages, a 3A current and the reverse voltage rating is greater than 1.25 times the max input voltage (40V > 1.25*22.2V = 27.75) according to the diode selection table in the datasheet. Being a Schottky diode, it has a fast switching speed and low forward voltage drop and hence provides the best efficiency especially for the low output voltage versions of the IC.

Feedback Connection:
The feedback pin is directly connected to the output capacitor in case of the fixed output voltage versions but incase of the adjustable output voltage versions, the feedback pin is connected to the voltage divider as a feedback driver, and the programming resistors are physically placed close to the regulator to protect the sensitive feedback wiring from noise.

ON/OFF trigger:
Since the ICs are to be used in normal operation, the ON/OFF pin is grounded and not kept as a floating value or pulled to a high logic level.
