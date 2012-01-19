SDRAM Programming Guide
=======================

The component is divided into a server component which runs in a single thread and receives requests for SDRAM refresh, server shutdown, burst read and burst write. A separate function to initialise the required ports and clock blocks and perform initial setup of the SDRAM is also provided. A client library is provided for the basi functions which communicates with the sdram server thread over a single channel end. Only one client is supported.

Key Files
---------

-------------------------------------- ----------------------------------------------------------------------
File                                   Description
====================================== ======================================================================
module_sdram_burst/src/sdram_burst.h   Header File for sdram server API.
module_sdram_burst/src/sdram_burst.xc  sdram init and server functionalit
app_sdram_burst_example/src/client.c   Client API. Includes sdram_burst.h
app_sdram_burst_example/src/test.xc    XC program that runs a simple series of read and write tests
-------------------------------------- ----------------------------------------------------------------------


Ports and Clocks Setup
----------------------

 Two clock blocks are used for the main SDRAM driver. Clkblk b_sdram_clk outputs a 12.5 MHz clock on port 1A. Clkblk b_sdram_io creates a delayed version of the sdram_clk (via p_sdram_clk) to drive the IO while meeting required setup and hold timings. 

All the ports besides clk, bank address and cke are buffered ports clocked by the delayed sdram clock and operating in strobed slave mode, slaved to a single 1 bit port, p_sdram_gate. When the latter is 0 all the buffered ports will be stalled.
 

-------------- -------------- ------------ -------------------------------------------------------------------
Signal         Port Name      ports        Notes
============== ============== ============ ===================================================================
clk            p_sdram_clk     1A           25 MHz
IO strobe      p_sdram_gate    1I           slaved perts below will update output each clk cycle
delayed clock  p_sdram_io      -            Delayed version of clk
cke            p_sdram_cke     1B
data           p_sdram_dq      16B          32b transfer reg for word aligned access 
dqm0/1         p_sdram_dqm0/1  1E/1F
cmd            p_sdram_cmd     4D           {CAS_N,RAS_N,WE_N,CE_N}. 32b transfer reg holds a 8 command cycles
bank address   p_sdram_ba0/1   1C/1D       
addr[12:1]     p_sdram_addr    32A          drives bits 12:1 of address
addr[0]        p_sdram_addr0   1G           drives bit 0 on port 1G. 4b transfer reg for 4 cycles of address


API 
---

Client API
++++++++++

.. doxygenfunction:: sdram_read
.. doxygenfunction:: sdram_write

Server Functions
++++++++++++++++

.. doxygenfunction::  sdram_init
.. doxygenfunction::  sdram_server
.. doxygenfunction::  sdram_shutdown
.. doxygenfunction::  sdram_refresh


SDRAM Init
----------

The initialisation process (sdram_init() in sdram_burst.xc) configures the ports as above and then executes the specified initialisation sequence (see page 43 of the datasheet) on the memory.

SDRAM Write
-----------

The sdram_write function uses a timstamped output to the p_sdram_gate port which in turn enables a precise number of cycles of output to the command, address and data ports. 

 


 
