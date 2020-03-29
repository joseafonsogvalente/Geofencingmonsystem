#  Geo-Fencing and Monitoring System
As IT Support for Douro Azul we solve various support tickets dealing with all the IT for all the vessels across the fleet. One of the recurring problems we face is the loss of connection on the 4G routers onboard the vessels at specific points of the river due to bad network coverage. The problem is, sometimes even after the ship gets through those bad spots, the routers don't automatically reconnect to 4G.
The goal of this project is to automatically reboot the routers when the vessel passes those specific areas on the river. 

**THE BOARD**

 - The NEO-6M GPS module captures the GPS signal and sends it to the ATMega328P microcontroller who processes the data. If the GPS position is inside the area of action, a signal is sent to activate the relay to reboot the routers physically. On newer routers, SSH is used to reboot the routers by command line instead.
   
 - Every X seconds a string is transmitted using the serial port with all the information needed for the monitoring system.
 
 - The board is powered by 5V but a 12 V voltage regulator was implemented. It can be powered by ICSP pins or by a 5V-12V transformer with a 2.1mm DC jack plug.

![Image description](https://lh3.googleusercontent.com/K2RRhuP8AZFWDdFi7bdW5HJYfSnlWtDOvijSbk2h6QBXGhZXsRm-g5Jv4K7TOdV0xWiemVqVD0QK0PJh7fg_nKX_HNn8GxVLIpteSaIDJjIEhzc_Xj7t8OEAwdG6A36Fhk9upN_nG0W6jCqin4ZIf8Hw7Hra_YKz8maM53szJo6tRGdXc0wTOuT-qjS0NBYJdtIo4HWdc8-5YUv6hd9pehnMjUdU640ReEJYXoOHxJrobMtjeG1Oetug07K40EhvwQkoOwdOLMDUSUIIgUhmh4phQPvOW5iufbzBG4V0TL1Vg0QW3e718gtu9IaF_1NXsdylpExDwaVLvxqppQjcHTW6kRf9wyoaxki7HxFjJDdGDDKxDFJ_hmRNjxpf5DNrdPDuXMsRF3U0bbL37l1z_pARhP0rim-nUZoYqO3LagE6HZT8zyngJrc2ibxVPUcVBiBml0dcuWGAYKcg5By3qbkHtXVnTWkZNurmaPYeZj_OvdB9NR6CXAjqpsI-6SbXa8WeNR7yNsVOtUbtv1qC8yCkxv1UPZYvz2IH0f4nPcFBpSjMsmwrAy58gNCwXniniBIBrLee72infHxYXFHUZXIFXIGz_q5vcb99tyaAW9s_LlqfUmriZ67Ceq98aW-qpXffEfPTMpW-z5iVyhJfwFFxNEryou_ZesgO64MZGhRFKbQPXaEb8ocUo1QH97xX6VU-_rDv_P2VeYBA1OGjJ5SgwPxzIttEqdO-4wyH1FuVJmSXRo7yUA=w804-h603-no)

**MONITORING SYSTEM**

The monitoring system consists of capturing the data from the serial port and displaying it. The simplest way is to plug a DB9- USB adapter and open a session with PuTTy, or another SSH client.
However, to display the data, WampServer (or similar) and the python script needs to be running.
This script listens to the serial port, parses the data when it arrives and stores it in a MySQL database.
The PHP page will then automatically refresh when new data arrives and it will display the ship location on the map.

![Image description](https://lh3.googleusercontent.com/1Z5YDJg2ZDS5AkYcBCamedLtsJ3uTK_lUsKBZGENQYW95DbKI9F2KGMFyGsJ6rNFHKIvvtBpEhN-DMUvLypbhE_lF1_Jocf5eSrKaKc-hyjJPBAIMa2JhSmtFrWtz6ZfOZPPzz15Rxt_BnmU-5cPas6B7GndypmY1HG7PCdh0tkIAHCGOqGrY8t1Ck3ff2ppqjBR2Lyd42DG1dgbDMcN0gBYmJA3uIgOkCXS_aQDKOG45YIWoqtauY4WCxhSJJhF5N4SwRM8cKQyx0BWFcn0i_igt5f98gb2z_kIOVKh9AXD4uzA_khKYzlSIzh6-3QeeLEDf7_0lj4uRDFdLNFtsvHv2Gc03qzx0KO1hZKfI1RqlcG0n2AfgHAtueqgeuMOPwsgdx2TIousWKxQBfn1Byd4xcdmFBY_meaq9xhD2HOOntc2N6FWr0EWdXMBz4zVD6vBVd5afHuDqIaWZPN6SvBBX3dTbDDDBJDYQLEFaqoEVkzIFeEr0qezrjF41QSHWqIETo0mQ0ZiBQRJO9MH19CZkCAfk8wM5OEY-k1iiLAfNTN3udPAiZGi55L8ifG7ecUNLlYQBWeeBRk81widn3lJ3fifm6rdAGjr_sLSbOQLztiwk5L5xIgZPlAnlD9MhLvULr1_lwhSSruEF5xf-YI9mwYOagIKac5JlP3HH9gfdIE_lz6GkZ49DXrB=w1024-h624-no)
