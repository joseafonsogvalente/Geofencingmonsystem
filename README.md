#  Geo-Fencing and Monitoring System
As IT Support for Douro Azul we solve various support tickets dealing with all the IT for all the vessels across the fleet. One of the recurring problems we face is the loss of connection on the 4G routers onboard the vessels at specific points of the river due to bad network coverage. The problem is, sometimes even after the ship gets through those bad spots, the routers don't automatically reconnect to 4G.
The goal of this project is to automatically reboot the routers when the vessel passes those specific areas on the river. 

**THE BOARD**

 - The NEO-6M GPS module captures the GPS signal and sends it to the ATMega328P microcontroller who processes the data. If the GPS position is inside the area of action, a signal is sent to activate the relay to reboot the routers physically. On newer routers, SSH is used to reboot the routers by command line instead.
   
 - Every X seconds a string is transmitted using the serial port with all the information needed for the monitoring system.
 
 - The board is powered by 5V but a 12 V voltage regulator was implemented. It can be powered by ICSP pins or by a 5V-12V transformer with a 2.1mm DC jack plug.

![Image description](https://lh3.googleusercontent.com/gkULRNrXTlCRl-sECvO1PZlxQUmdB3ob-PnjRudqhanWrs0V277JFcivkpHrjQRYmABhGUYu7bqMIVsYm2HTjhYzRpC3d8_gThc_HO1WST-cO4cmCS5vIJX1exBYmYcSo32D5RCWf7cFHrf4bHrmf7STwiEQYpzOaGJB_yvDtTopTCNEQG_cHNi3EdMVoVl6Mv7OBt0SHT4ddS-0ZDlqCIP8xcZg5IYenVK1o4cGEAYFbz9RxzDLTaoC0MFnt7XSuR0-aiwCr3NJmWlQHKQoK5WikbH8x9_-g_tZwHu3ca76F-PqB3icltxIoG0kz8vwNsbJ0J071140nXfVEinwljH6549EflRAXuEMELSV2Q6WwDK5VOzOt3FzgYbLMBkirByf8Ka-C4gNTfFWgZFMk3Dxezsn6Utphrb92xkh1Mnqj9NacvAk4lvXGODnrgpwwlJG3JqdpMMB2hHZagMAPt73Xd_OLBbrGdVxpgybPNkF4fDkS1BixEH8gdVfsqAY4VdZmzyC82Rl7yX4UHTCWjbfutBKfAu14jYdrIfRK2q7eeGuIZ3HjuI-QCfl_X2AQkblP5iKkum10Uii73shnt73xIzHEKL0YAM-hVsbd0QNwE0quUicHT35uw7fVS7ZRvd21NYpiNxWleScpw3_a772FGdJXNuZkvdD2ESptI7GPV_4lmik6A=w1258-h943-no)

**MONITORING SYSTEM**

The monitoring system consists of capturing the data from the serial port and displaying it. The simplest way is to plug a DB9- USB adapter and open a session with PuTTy, or another SSH client.
However, to display the data, WampServer (or similar) and the python script needs to be running.
This script listens to the serial port, parses the data when it arrives and stores it in a MySQL database.
The PHP page will then automatically refresh when new data arrives and it will display the ship location on the map.

![Image description](https://lh3.googleusercontent.com/pMz8r10eKBv2Ru-ECiwmkAkGmldAUCP3DucgZE-Qk6rZ4ZomT1yKZ2oMPImMLDQFtGnjbKe9A8TrDZLIuq74m2Ij7Iq00iRTthbkql6XwjuFVA0klQmNdXUex7Y8O-8Iei5gmWXrqskq-Y4ATiEYwAvQKy_-FZYdacKFo7-nPdBFHaVlSkd21gKwGMXvrmkc8oE9g8u-ekTM7li5TFDIVhTVxvhTCT_7IZ_HyYGe49QGhI7SRx4mXAbdrTaz5fY1W5hk8lnhohD5qA_cMeg9BhZdKVUvBCi0EQ8GSwDeHXa9Z7rF84yoBYfzsC0g66Vdi7Um2Q4ZNYzStq_5VLpkiGJEyLKz6GEOPzcioaGmNu9EN8I0dNbPo70ve4yAvsuHOEcUABljdS83jem4fqFEKYR2yiDdG5xJkuTbV5ymg7FKvLxHh9DfijlvTWVn9Dv2u7KdQJXDNjkbX6SsKRdJyZU1JCGnP103d3YbALler-NeIfPD8ph-DfWzi88L7q5IcRV_yMgc6iQe6Ic6Z0xu-pcU_2pLCmIbzetZP9ir__28YmcBEiQhAgBDl5Bwfq6cqLkqR06rl5e1PYRfh4q1uzi15tm-em95MmfeqCi6wccm8MVXtgudGlxKA1Zi1kwMo-C6Kqg4ENWSxjZUSe24gwbBz7QeCqBV1VRLq-ZlRPwPkzytlrdqyQ=w1024-h624-no)
