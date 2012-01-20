SDRAM Hardware Development Platforms
====================================

The XDK (3V0 version) is the only XMOS development kit currently capable of interfacing to an SDRAM. This option is provided via a plug in module that attaches to the Xcore 1 IO expansion connector on the left side of the XDK housing. 

Setting Up The XDK for the Demo App
-----------------------------------

First, open the back of the XDK hosuing and ensure the DIP jumpers are configured as follows:

+-----+-----+
| OFF | ON  |
+-----+-----+
|     | *   |
+-----+-----+
|     | *   |
+-----+-----+
|     | *   |
+-----+-----+
|     | *   |
+-----+-----+
| *   |     |
+-----+-----+
| *   |     |
+-----+-----+
|     | *   |
+-----+-----+
| *   |     |
+-----+-----+
|     | *   |
+-----+-----+
|     | *   |
+-----+-----+
|     | *   |
+-----+-----+
| *   |     |
+-----+-----+
|     | *   |
+-----+-----+
| *   |     |
+-----+-----+
|     | *   |
+-----+-----+
|     | *   |
+-----+-----+
|     | *   |
+-----+-----+
|     | *   |
+-----+-----+
|     | *   |
+-----+-----+
|     | *   |
+-----+-----+
|     | *   |
+-----+-----+
|     | *   |
+-----+-----+
|     | *   |
+-----+-----+


Then follow the steps below.

   #. Insert the SDRAM module into the XCore1 IO connector.
   #. Connect power to the XDK and a UDB cable between the XDK USB(JTAG) connector and the PC.
   #. Compile and run the demo app. The test progress and results should appear in the console window.

 


