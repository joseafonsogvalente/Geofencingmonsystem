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

![Image description](https://lh3.googleusercontent.com/p4E9bdJ7pCCEHOVXiaI6RCZ4DGsMGeYN8n06bhMtkJrcyjySJbOGMXS9IS361VJnpjJ_iwD3aL-A9ZrCvm25Yuv09s27HD53SSdBGaY6-4iUR50TiPIB6eNMQF1RZm14w_ZS1plqQv9yoWlKOkuPHMWG6nrplMt7Z8uxRv_1eLRdp98FjTZTkpCg17lIgt5pRTKSTuShKMkg38Rj2gJnQDGUlaejkwKk-rSWTxdI41QqiRvjv00mK8WRNVM5WnFCvdWxqPMdYCiRIEOZNEX_vzjPJg1myOONt-HQ2Vl35EVaNNPtrOlZUL9CZ02xqEhDltvCYWU1l5T9rLCv08C8BoBYcH6ZSUr_S8j7KBhl5V5mGSh-F7A2RefaglkdpaybRyqFi0U0VY7iDaxG4n2rJjHfiEkhSQFN0pLgMi4_cQCnXTOt-7kGlu1Dz6cC0FQ_hpkJzV30uDztJcplZ22ml_vmLrkuhiSzpd1N0LDLKjbw6qZy4eUZCSbxaO6FdNCrXxJJkDZnnfSqflx1PX19rW-eV6cbqnOUVj14glxeCIAlLAorq1_EgRsQ-yTGEqh2uoqxeVLPeQkIM2xN8uQTpgRNGSBnBn82v_4ZrQlG4G3_VCulVNAr4dQNT29My3XEL6WX26L1Ea42AjFGg6m1jAeUSpDunuM=w1024-h624-no)
