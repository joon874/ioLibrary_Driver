# ioLibrary Driver
The ioLibrary means “Internet Offload Library” for WIZnet chip. It includes drivers and application protocols.
The driver (ioLibrary) can be used for the application design of WIZnet TCP/IP chips as [W5500](http://wizwiki.net/wiki/doku.php?id=products:w5500:start), W5300, W5200, W5100 [W5100S](http://wizwiki.net/wiki/doku.php?id=products:w5100s:start).

## ioLibrary
This driver provides the Berkeley Socket type APIs.
- Directory Structure
<!-- ioLibrary pic -->
![ioLibrary](http://wizwiki.net/wiki/lib/exe/fetch.php?media=products:w5500:iolibrary_bsd.jpg "ioLibrary")

- Ethernet : SOCKET APIs like BSD & WIZCHIP([W5500](http://wizwiki.net/wiki/doku.php?id=products:w5500:start) / W5300 /  W5200 / W5100 / [W5100S](http://wizwiki.net/wiki/doku.php?id=products:w5100s:start)) Driver
- Internet :
  - DHCP client
  - DNS client
  - FTP client
  - FTP server
  - SNMP agent/trap
  - SNTP client
  - TFTP client
  - HTTP server
  - MQTT Client
  - Others will be added.

## How to add an ioLibrary in project through github site.
  - Example, refer to https://www.youtube.com/watch?v=mt815RBGdsA
  - [ioLibrary Doxygen doument](https://github.com/Wiznet/ioLibrary_Driver/blob/master/Ethernet/Socket_APIs_V3.0.3.chm) : Refer to **TODO** in this document
    - Define what chip is used in **wizchip_conf.h**
    - Define what Host I/F mode is used in **wizchip_conf.h**

## Revision History
  * ioLibrary V4.0.0 Released : 29, MAR, 2018
    * New features added: Library for W5100S added.
  * ioLibrary V3.1.1 Released : 14, Dec, 2016
    * Bug fixed : In Socket.c Fixed MACraw & IPraw sendto function.
  * ioLibrary V3.1.0 Released : 05, Dec, 2016
    * Internet application protocol add to MQTT Client (using paho MQTT 3.11)
  * ioLibrary V3.0.3 Released : 03, May, 2016
    * In W5300, Fixed some compile errors in close(). Refer to M20160503
    * In close(), replace socket() with some command sequences.
  * ioLibrary V3.0.2 Released : 26, April, 2016
    * Applied the erratum #1 in close() of socket.c (Refer to A20160426)
  * ioLibrary V3.0.1 Released : 15, July, 2015
    * Bug fixed : In W5100, Fixed CS control problem in read/write buffer with SPI. Refer to M20150715.
  * ioLibrary V3.0 Released : 01, June, 2015
    * Add to W5300
    * Typing Error in comments
    * Refer to 20150601 in sources.

  * Type casting error Fixed : 09, April. 2015
    In socket.c, send() : Refer to M20150409

  * ioLibrary V2.0 released : April. 2015
    * Added to W5100, W5200
    * Correct to some typing error
    * Fixed the warning of type casting.

  * Last release : Nov. 2014


# ioLibrary Issues
Organize the various opened issues raised by users and take action to address them, as shown below.

| #num | Summary of content | Possible solutions | Applicability |
|:----:|--------------------|--------------------|---------------|
| [#84](https://github.com/Wiznet/ioLibrary_Driver/issues/84) | Constant value error defining the maximum number of sockets | decrease _WIZCHIP_SOCK_NUM_ value depending on Chip sockets | [X] |
| [#92]() | Error due to wizchip_close() function not being called between DNS example behaviors | Add to wizchip_close() and check it is called | [O] |
| [#94]() | Infinite loop in while() function for checking socket status due to no break behavior on status abnormality | Timeout by a TIMER on the user's MCU or timeout behavior based on socket state | [X] |
| [#107]() | SPI BURST Function Implementation Issues | no issue(already exist that function) | [O] |
| [#115]() | SNTP function does not retransmit when the NTP retransmission value is 0. | Workaround with separate conditional processing when NTP retransmission value is 0 | [O] |
| [#117]() | W5300 users using TI MCUs are experiencing behavioral errors due to lack of bit masking for MCUs operating at 16 bits. | Need to modify and test bit masking on W5300 to work with 16 bits | [X] |
| [#128]() | Request for countermeasures when network information and socket information are init by unintentional hardware reset while using Wiznet chips such as W5500. | Need to find a software way to notify users on hardware reset | [X] |
| [#129]() | Requesting a fix for a running part of an HTTP application with a fixed buffer size of 2K | Tested and fixed an inconsistency about limiting to 2K in a function even if the socket buffer is larger than 2K. | [X] |
| [#135]() | An inter-functional error occurs when the size of the BUFPUB variable in the Http parser function is limited to 256. | Looks like testing should come first | [X] |
| [#103]() | During the RECV() function operation, a forced socket close operation instead of a disconnection occurs for the other party's FIN packet, causing the other party's socket to be closed abnormally. | Add a processor for a healthy termination of the other party's FIN packets during the RECV() function operation. | [X] |
| [#104]() | Index error in function to read W5300 MAC address | Resolved with correct index modification | [X] |
| [#119]() | W5300 Variable declaration found to be declared as 32-bit for an 8-bit variable | Redefine that variable as uint8_t | [X] |
| [#123]() | An error in the flag behavior when receiving a packet in the MQTTClient application. This error is not yet resolved by the PAHO MQTT library. | There is no way to fix this. | [X] |
| [#130]() | Issue with W5500 and HUB being set to 100HDX when set to auto-nego. In the link behavior, the link of the device is forcibly set to 100HDX when the hub and device are auto-nego. | Normal operation | [X] |
