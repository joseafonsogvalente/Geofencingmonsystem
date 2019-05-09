#  Geo-Fencing and Monitoring System
As IT Support for Douro Azul we solve various support tickets dealing with all the IT for all the vessels across the fleet. One of the recurring problems we face is the loss of connection on the 4G routers onboard the vessels at specific points of the river due to bad network coverage. The problem is, sometimes even after the ship gets through those bad spots, the routers don't automatically reconnect to 4G.
The goal of this project is to automatically reboot the routers when the vessel passes those specific areas on the river. 

**THE BOARD**

 - The NEO-6M GPS module captures the GPS signal and sends it to the ATMega328P microcontroller who processes the data. If the GPS position is inside the area of action, a signal is sent to activate the relay to reboot the routers physically. On newer routers, SSH is used to reboot the routers by command line instead.
   
 - Every X seconds a string is transmitted using the serial port with all the information needed for the monitoring system.
 
 - The board is powered by 5V but a 12 V voltage regulator was implemented. It can be powered by ICSP pins or by a 5V-12V transformer with a 2.1mm DC jack plug.

![Image description](https://lh3.googleusercontent.com/Eo_eSas-K5mA47Hlty8szivxUAyqNkMub4f4FXNr2_K5C7OO4cjvIfBdFveTNFGjSbcLZ_pRLzNHnoVpQ8SD6cNyVtmTVAqRy6nu0T_9XsMSQvYCikl99z_GTrYDKeZBNtszfS3sfkQz_HY8MgSB70XK15HP1YsexpKlu_8lfzwaHdOO5eUKpYH5WqJwlLBqKpfgLNSXFExdToxSa38SwwrfaP2iBH3LIyLDCcExP6f2qJB43UMfdMU7p-hXQhirhKjzq8vmkG8aKWnSzVLWMPRJPGw6CNhm0LHhN6eiIlEaaOhAG0xx9R7hLmJ8awyyHxS_EyoW3VBNpBkVD9OltxXqushkAP1QTDsRRt_LSjh5unxjPCgiNHLf1gDTwV0oae1999hLq2RbRy7ter7MV5G5QNZ9rrKowS7lcwFqnM51Zip_GivRL1insiAQutVcom43z_OKNXl0IsqVivldsr_sHlpq9FeKTnx3jV0ehsGfk1P3nhHVv6Ezhiyf5J4PPYD-XX3r667t-unDTqkUSnzmNAbDI0ZKA9JpSholfd_y9yXDONO6hpGQuSE0pzwhf0viZja3rSxzIV4wvfSljZNhlRhsTWVmYNFEPx5lkGtrw24irmg4HKT4qSkhvlLdH4y6JssUE_QRNPKJYjztht9OhUPCQAM=w1221-h915-no)

**MONITORING SYSTEM**

The monitoring system consists of capturing the data from the serial port and displaying it. The simplest way is to plug a DB9- USB adapter and open a session with PuTTy, or another SSH client.
However, to display the data, WampServer (or similar) and the python script needs to be running.
This script listens to the serial port, parses the data when it arrives and stores it in a MySQL database.
The PHP page will then automatically refresh when new data arrives and it will display the ship location on the map.

![Image description](https://lh3.googleusercontent.com/p4E9bdJ7pCCEHOVXiaI6RCZ4DGsMGeYN8n06bhMtkJrcyjySJbOGMXS9IS361VJnpjJ_iwD3aL-A9ZrCvm25Yuv09s27HD53SSdBGaY6-4iUR50TiPIB6eNMQF1RZm14w_ZS1plqQv9yoWlKOkuPHMWG6nrplMt7Z8uxRv_1eLRdp98FjTZTkpCg17lIgt5pRTKSTuShKMkg38Rj2gJnQDGUlaejkwKk-rSWTxdI41QqiRvjv00mK8WRNVM5WnFCvdWxqPMdYCiRIEOZNEX_vzjPJg1myOONt-HQ2Vl35EVaNNPtrOlZUL9CZ02xqEhDltvCYWU1l5T9rLCv08C8BoBYcH6ZSUr_S8j7KBhl5V5mGSh-F7A2RefaglkdpaybRyqFi0U0VY7iDaxG4n2rJjHfiEkhSQFN0pLgMi4_cQCnXTOt-7kGlu1Dz6cC0FQ_hpkJzV30uDztJcplZ22ml_vmLrkuhiSzpd1N0LDLKjbw6qZy4eUZCSbxaO6FdNCrXxJJkDZnnfSqflx1PX19rW-eV6cbqnOUVj14glxeCIAlLAorq1_EgRsQ-yTGEqh2uoqxeVLPeQkIM2xN8uQTpgRNGSBnBn82v_4ZrQlG4G3_VCulVNAr4dQNT29My3XEL6WX26L1Ea42AjFGg6m1jAeUSpDunuM=w1024-h624-no)
