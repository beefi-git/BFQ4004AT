**BFQ4004 AT Instruction**

**Version 1.0.0**

Version Notes：

========== ======= ================================
Date       Version Description
========== ======= ================================
2020/05/12 1.0.0   Phase-1 AT commands, first draft
\                  
========== ======= ================================

**Table of Contents**

1 Command Description 1

2 Basic AT Commands 2

2.1 Overview 2

2.2 Commands 2

2.2.1 AT - Test AT 2

2.2.2 ATE - Configure echo of AT commands 2

2.2.2 AT+RST - Restart module 2

2.2.3 AT+GMR – Check version information 3

2.2.4 AT+RESTORE - Restore factory default setting 3

2.2.5 AT+UART_CUR - Current UART configuration, not save in Flash 3

2.2.6 AT+UART_DEF - Default UART configuration, save in Flash 4

2.2.7 AT+SYSRAM - Check the available RAM size 5

3 Wi-Fi AT Commands 5

3.1 Overview 5

3.2 Commands 6

3.2.1 AT+CWMODE_CUR - 6

4 TCP/IP AT Commands 6

4.1 Overview 6

4.2 Commands 6

4.2.1 AT+CIPSTATUS - Get Connection Status 6

4.2.2 AT+CIPDOMAIN - DNS Function 7

4.3.3 AT+CIPSTART - Establish TCP/UDP Connection 7

4.4.4 AT+CIPSEND - Send Data 8

4.4.5 AT+CIPCLOSE - Close TCP/UDP Connection 9

4.4.6 AT+CIPMUX - Enable/Disable Multiple Connection 10

4.4.7 AT+CIPSERVER - Create/Delete TCP server 10

4.4.8 AT+SERVERMAXCONN - Set Max Connection Allowed By Server 11

4.4.9 AT+CIPMODE - Set Transmission Mode 11

4.4.10 +IPD - Receive Network Data 11

1 Command Description
=====================

Each command set contains four types of AT commands：

+-----------------+--------------+-----------------------------------+
| type            | format       | description                       |
+=================+==============+===================================+
| Test Command    | AT+<x>=?     | Queries the Set Command’s         |
|                 |              | internal parameters and their     |
|                 |              | range of values.                  |
+-----------------+--------------+-----------------------------------+
| Query Command   | AT+<x>?      | Return the current value of       |
|                 |              | parameters.                       |
+-----------------+--------------+-----------------------------------+
| Set Command     | AT+<x>=<...> | Sets the value of user-defined    |
|                 |              | parameters in commands,           |
|                 |              |                                   |
|                 |              | and runs these commands.          |
+-----------------+--------------+-----------------------------------+
| Execute Command | AT+<x>       | Runs commands with no             |
|                 |              | user-defined parameters.          |
+-----------------+--------------+-----------------------------------+

Notes：

1. Not all AT commands support all four variations mentioned above.

2. Square brackets [ ] designate the default value; it is either not
   required or may not appear.

3. String values need to be included in double quotation marks, for
   example: AT+CWSAP="BFQ756290","21030826", 1,4

4. The default baud rate is 115200

5. AT commands have to be capitalized, and must end with a new line (CR
   LF)

2 Basic AT Commands
===================

2.1 Overview
------------

=========== =============================================
commands    description
=========== =============================================
AT          Test AT
ATE         Configure echo of AT commands
AT+RST      Restart module
AT+GMR      Check version info
AT+RESTORE  Restore factory default setting
AT+UART_CUR Current UART configuration, Not save in Flash
AT+UART_DEF Default UART configuration, save in Flash
AT+SYSRAM   Check the available RAM size
=========== =============================================

2.2 Commands
------------

2.2.1 AT - Test AT
~~~~~~~~~~~~~~~~~~

=============== ==
Execute Command AT
=============== ==
Response        OK
Parameters      \-
=============== ==

2.2.2 ATE - Configure echo of AT commands
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

=============== ==
Execute Command AT
=============== ==
Response        OK
Parameters      -
=============== ==

2.2.2 AT+RST - Restart module
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

=============== ======
Execute Command AT+RST
=============== ======
Response        OK
Parameters      -
=============== ======

2.2.3 AT+GMR – Check version information
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

=============== ==================
Execute Command AT+GMR
=============== ==================
Response        <AT version info >
                
                <SDK version info>
                
                <compile time>
                
                OK
Parameters      -
example         AT+GMR
=============== ==================

2.2.4 AT+RESTORE - Restore factory default setting
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+-----------------+---------------------------------------------------+
| Execute Command | AT+RESTORE                                        |
+=================+===================================================+
| Response        | OK                                                |
+-----------------+---------------------------------------------------+
| Parameters      | -                                                 |
+-----------------+---------------------------------------------------+
| Note            | The execution of this command will reset all      |
|                 | parameters saved in flash and restore the factory |
|                 | default settings of the module. The chip will be  |
|                 | restarted when this command is executed。         |
+-----------------+---------------------------------------------------+

2.2.5 AT+UART_CUR - Current UART configuration, not save in Flash
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+----------+----------------------------+----------------------------+
| Command  | Query Command:             | Set Command：              |
|          |                            |                            |
|          | AT+UART_CUR?               | AT+UART                    |
|          |                            | _CUR=<baudrate>,<databits> |
|          |                            | ,<stopbits>,<parity>,<flow |
|          |                            | control>                   |
+==========+============================+============================+
| Response | +UART                      | OK                         |
|          | _CUR:<baudrate>,<databits> |                            |
|          |                            |                            |
|          | ,<stopbits>,<parity>,<flow |                            |
|          | control>                   |                            |
|          |                            |                            |
|          | OK                         |                            |
+----------+----------------------------+----------------------------+
| Example  | AT+UART_CUR?               | AT+UART_CUR=115200,8,1,0,3 |
+----------+----------------------------+----------------------------+
| Note     | <baudrate>：UART baud rate |                            |
|          |                            |                            |
|          | <databits>：data bits      |                            |
|          |                            |                            |
|          | 5： 5-bit data             |                            |
|          |                            |                            |
|          | 6： 6-bit data             |                            |
|          |                            |                            |
|          | 7： 7-bit data             |                            |
|          |                            |                            |
|          | 8： 8-bit data             |                            |
|          |                            |                            |
|          | <stopbits>：stop bits      |                            |
|          |                            |                            |
|          | 1： 1-bit stop bit         |                            |
|          |                            |                            |
|          | 2： 1.5-bit stop bit       |                            |
|          |                            |                            |
|          | 3： 2-bit stop bit         |                            |
|          |                            |                            |
|          | <parity>：parity bit       |                            |
|          |                            |                            |
|          | 0： None                   |                            |
|          |                            |                            |
|          | 1： Odd                    |                            |
|          |                            |                            |
|          | 2： Even                   |                            |
|          |                            |                            |
|          | <flow control>：flow       |                            |
|          | control                    |                            |
|          |                            |                            |
|          | 0：disable                 |                            |
|          |                            |                            |
|          | 1：enable RTS              |                            |
|          |                            |                            |
|          | 2：enable CTS              |                            |
|          |                            |                            |
|          | 3：enable both RTS and CTS |                            |
+----------+----------------------------+----------------------------+

2.2.6 AT+UART_DEF - Default UART configuration, save in Flash
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+----------+----------------------------+----------------------------+
| Command  | Query Command:             | Set Command：              |
|          |                            |                            |
|          | AT+UART_DEF?               | AT+UART                    |
|          |                            | _DEF=<baudrate>,<databits> |
|          |                            | ,<stopbits>,<parity>,<flow |
|          |                            | control>                   |
+==========+============================+============================+
| Response | +UART                      | OK                         |
|          | _DEF:<baudrate>,<databits> |                            |
|          |                            |                            |
|          | ,<stopbits>,<parity>,<flow |                            |
|          | control>                   |                            |
|          |                            |                            |
|          | OK                         |                            |
+----------+----------------------------+----------------------------+
| Example  | AT+UART_DEF?               | AT+UART_DEF=115200,8,1,0,3 |
+----------+----------------------------+----------------------------+
| Note     | <baudrate>：UART baud rate |                            |
|          |                            |                            |
|          | <databits>：data bits      |                            |
|          |                            |                            |
|          | 5： 5-bit data             |                            |
|          |                            |                            |
|          | 6： 6-bit data             |                            |
|          |                            |                            |
|          | 7： 7-bit data             |                            |
|          |                            |                            |
|          | 8： 8-bit data             |                            |
|          |                            |                            |
|          | <stopbits>：stop bits      |                            |
|          |                            |                            |
|          | 1： 1-bit stop bit         |                            |
|          |                            |                            |
|          | 2： 1.5-bit stop bit       |                            |
|          |                            |                            |
|          | 3： 2-bit stop bit         |                            |
|          |                            |                            |
|          | <parity>：parity bit       |                            |
|          |                            |                            |
|          | 0： None                   |                            |
|          |                            |                            |
|          | 1： Odd                    |                            |
|          |                            |                            |
|          | 2： Even                   |                            |
|          |                            |                            |
|          | <flow control>：flow       |                            |
|          | control                    |                            |
|          |                            |                            |
|          | 0：disable                 |                            |
|          |                            |                            |
|          | 1：enable RTS              |                            |
|          |                            |                            |
|          | 2：enable CTS              |                            |
|          |                            |                            |
|          | 3：enable both RTS and CTS |                            |
+----------+----------------------------+----------------------------+

2.2.7 AT+SYSRAM - Check the available RAM size
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

================ ==================================================
Query Command    AT+SYSRAM?
================ ==================================================
Response         +SYSRAM:<remain RAM size>
                 
                 OK
Example          AT+SYSRAM?
Response Example +SYSRAM:30000
                 
                 OK
Note             <remain RAM size>：remain space of RAM, unit: Byte
================ ==================================================

3 Wi-Fi AT Commands
===================

.. _overview-1:

3.1 Overview
------------

+----------------+----------------------------------------------------+
| Commands       | Description                                        |
+================+====================================================+
| AT+CWMODE_CUR  | Set Wi-Fi mode, configuration not save in Flash.   |
+----------------+----------------------------------------------------+
| AT+CWMODE_DEF  | Set Wi-Fi mode, configuration save in Flash.       |
+----------------+----------------------------------------------------+
| AT+CWJAP_CUR   | Connect to an AP, configuration not save in Flash. |
+----------------+----------------------------------------------------+
| AT+CWJAP_DEF   | Connect to an AP, configuration save in Flash.     |
+----------------+----------------------------------------------------+
| AT+CWLAPOPT    | Set the configuration of command AT+CWLAP.         |
+----------------+----------------------------------------------------+
| AT+CWLAP       | List available APs.                                |
+----------------+----------------------------------------------------+
| AT+CWQAP       | Disconnect from an AP.                             |
+----------------+----------------------------------------------------+
| AT+CWSAP_CUR   | Set softAP configuration, configuration not save   |
|                | in flash.                                          |
+----------------+----------------------------------------------------+
| AT+CWSAP_DEF   | Set softAP configuration, configuration save in    |
|                | flash.                                             |
+----------------+----------------------------------------------------+
| AT+CWLIF       | Get stations IP which connect to BFQ4004 softAP.   |
+----------------+----------------------------------------------------+
| AT+CWDHCP_CUR  | Enable/disable DHCP, configuration not save in     |
|                | Flash.                                             |
+----------------+----------------------------------------------------+
| AT+CWDHCP_DEF  | Enable/disable DHCP, configuration save in Flash.  |
+----------------+----------------------------------------------------+
| AT+CWDHCPS_CUR | Set IP range of the DHCP server, configuration not |
|                | save in Flash.                                     |
+----------------+----------------------------------------------------+
| AT+CWDHCPS_DEF | Set IP range of the DHCP server, configuration     |
|                | save in Flash.                                     |
+----------------+----------------------------------------------------+
| AT+CWAUTOCONN  | Connect to an AP automatically when power on.      |
+----------------+----------------------------------------------------+

.. _commands-1:

3.2 Commands
------------

3.2.1 AT+CWMODE_CUR - 
~~~~~~~~~~~~~~~~~~~~~

4 TCP/IP AT Commands
====================

.. _overview-2:

4.1 Overview
------------

=================== =====================================
Commands            Description
=================== =====================================
AT+CIPSTATUS        Get the connection status.
AT+CIPDOMAIN        DNS function.
AT+CIPSTART         Establish TCP/UDP/SSL connection.
AT+CIPSEND          Send data.
AT+CIPCLOSE         Close TCP/UDP/SSL connection.
AT+CIFSR            Get local IP address.
AT+CIPMUX           Enable/disable multiple connections.
AT+CIPSERVER        Create/delete tcp server.
AT+CIPSERVERMAXCONN Set max connection allowed by server.
AT+CIPMODE          Set transmission mode.
AT+CIPSTO           Set tcp server timeout
+IPD                Receive network data.
=================== =====================================

.. _commands-2:

4.2 Commands
------------

4.2.1 AT+CIPSTATUS - Get Connection Status
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+-----------------+---------------------------------------------------+
| Execute Command | AT+CIPSTATUS                                      |
+=================+===================================================+
| Response        | STATUS:<stat>                                     |
|                 |                                                   |
|                 | +CIPSTATUS:<link ID>,<type>,<remote IP>,<remote   |
|                 | port>,<local port>,<tetype>                       |
+-----------------+---------------------------------------------------+
| Note            | <stat>: status of BFQ4004 station interface       |
|                 |                                                   |
|                 | 2: BFQ4004 is connected to an AP and it’s IP      |
|                 | obtained.                                         |
|                 |                                                   |
|                 | 3: BFQ4004 has create a TCP/UDP transmission.     |
|                 |                                                   |
|                 | 4: TCP/UDP transmission of BFQ4004 is             |
|                 | disconnected.                                     |
|                 |                                                   |
|                 | 5: BFQ4004 not connect to an AP.                  |
|                 |                                                   |
|                 | <link ID>: ID of connection(0 ~ 4), used for      |
|                 | multiple connections.                             |
|                 |                                                   |
|                 | <type>: string parameter, “TCP” or “UDP”.         |
|                 |                                                   |
|                 | <remote IP>: string, remote IP address.           |
|                 |                                                   |
|                 | <remote IP>: number, remote port.                 |
|                 |                                                   |
|                 | <local port>: number, BFQ4004 local port.         |
|                 |                                                   |
|                 | <tetype>:                                         |
|                 |                                                   |
|                 | 0: BFQ4004 run as a client.                       |
|                 |                                                   |
|                 | 1: BFQ4004 run as a server.                       |
+-----------------+---------------------------------------------------+

4.2.2 AT+CIPDOMAIN - DNS Function
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+-----------------+---------------------------------------------------+
| Execute Command | AT+CIPDOMAIN=<domain name>                        |
+=================+===================================================+
| Response        | +CIPDOMAIN:<IP address>                           |
|                 |                                                   |
|                 | OK                                                |
|                 |                                                   |
|                 | Or                                                |
|                 |                                                   |
|                 | DNS Fail                                          |
|                 |                                                   |
|                 | ERROR                                             |
+-----------------+---------------------------------------------------+
| Note            | <domain name>: string, domain name, length must   |
|                 | be less than 64 bytes.                            |
+-----------------+---------------------------------------------------+

4.3.3 AT+CIPSTART - Establish TCP/UDP Connection
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**TCP Connection:**

+-------------+--------------------------+--------------------------+
| Set Command | Single TCP               | Multiple TCP             |
|             | Connection(AT+CIPMUX=0): | Connection(AT+CIPMUX=1): |
|             |                          |                          |
|             | AT                       | AT+CIPSTART=<link        |
|             | +CIPSTART=<type>,<remote | ID>,<type>,<remote       |
|             | IP>,<remote port>[,<TCP  | IP>,<remote port>[,<TCP  |
|             | keep alive>]             | keep alive>]             |
+=============+==========================+==========================+
| Response    | OK                       |                          |
|             |                          |                          |
|             | Or                       |                          |
|             |                          |                          |
|             | ERROR                    |                          |
|             |                          |                          |
|             | If TCP connection is     |                          |
|             | already established, the |                          |
|             | response is:             |                          |
|             |                          |                          |
|             | ALREADY CONNECTED        |                          |
+-------------+--------------------------+--------------------------+
| Note        | <link ID>: ID of network |                          |
|             | connection (0~4), used   |                          |
|             | for multiple             |                          |
|             | connections.             |                          |
|             |                          |                          |
|             | <type>: string parameter |                          |
|             | indicating the           |                          |
|             | connection type: "TCP",  |                          |
|             | "UDP" or "SSL".          |                          |
|             |                          |                          |
|             | <remote IP>: string      |                          |
|             | parameter indicating the |                          |
|             | remote IP address.       |                          |
|             |                          |                          |
|             | <remote port>: the       |                          |
|             | remote port number.      |                          |
|             |                          |                          |
|             | [<TCP keep alive>]:      |                          |
|             | detection time interval  |                          |
|             | when TCP is kept alive,  |                          |
|             | this function is         |                          |
|             | disabled by default.     |                          |
|             |                          |                          |
|             | 0: disable TCP           |                          |
|             | keep-alive.              |                          |
|             |                          |                          |
|             | 1 ~ 7200: detection time |                          |
|             | interval, unit: second   |                          |
|             | (s).                     |                          |
+-------------+--------------------------+--------------------------+
| Example     | AT+CIPSTART="TCP         |                          |
|             | ","192.168.101.110",1000 |                          |
+-------------+--------------------------+--------------------------+

**UDP Connection:**

+-------------+--------------------------+--------------------------+
| Set Command | Single connection        | Multiple connections     |
|             | (AT+CIPMUX=0):           | AT+CIPMUX=1):            |
|             |                          |                          |
|             | AT                       | AT+CIPSTART=<link        |
|             | +CIPSTART=<type>,<remote | ID>,<type>,<remote       |
|             | IP>,<remote port>[,(<UDP | IP>,<remote port>[,(<UDP |
|             | local port>),(<UDP       | local port>),(<UDP       |
|             | mode>)]                  | mode>)]                  |
+=============+==========================+==========================+
| Response    | OK                       |                          |
|             |                          |                          |
|             | or                       |                          |
|             |                          |                          |
|             | ERROR                    |                          |
|             |                          |                          |
|             | If the UDP transmission  |                          |
|             | is already established,  |                          |
|             | the response is:         |                          |
|             |                          |                          |
|             | ALREADY CONNECTED        |                          |
+-------------+--------------------------+--------------------------+
| Note        | <link ID>: ID of network |                          |
|             | connection (0~4), used   |                          |
|             | for multiple             |                          |
|             | connections.             |                          |
|             |                          |                          |
|             | <type>: string parameter |                          |
|             | indicating the           |                          |
|             | connection type: "TCP",  |                          |
|             | "UDP" or "SSL".          |                          |
|             |                          |                          |
|             | <remote IP>: string      |                          |
|             | parameter indicating the |                          |
|             | remote IP address.       |                          |
|             |                          |                          |
|             | <remote port>: remote    |                          |
|             | port number.             |                          |
|             |                          |                          |
|             | [<UDP local port>]:      |                          |
|             | optional; UDP port of    |                          |
|             | QCA4004.                 |                          |
|             |                          |                          |
|             | [<UDP mode>]: optional.  |                          |
|             | In the UDP transparent   |                          |
|             | transmission, the value  |                          |
|             | of this parameter has to |                          |
|             | be 0.                    |                          |
|             |                          |                          |
|             | 0: the destination peer  |                          |
|             | entity of UDP will not   |                          |
|             | change, this is the      |                          |
|             | default setting.         |                          |
|             |                          |                          |
|             | 1: the destination peer  |                          |
|             | entity of UDP can change |                          |
|             | once.                    |                          |
|             |                          |                          |
|             | 2: the destination peer  |                          |
|             | entity of UDP is allowed |                          |
|             | to change                |                          |
|             |                          |                          |
|             | To use <UDP mode> , <UDP |                          |
|             | local port> must be set  |                          |
|             | first                    |                          |
+-------------+--------------------------+--------------------------+
| Example     | AT+CIPSTART="UDP","192.  |                          |
|             | 168.101.110",1000,1002,2 |                          |
+-------------+--------------------------+--------------------------+

4.4.4 AT+CIPSEND - Send Data
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+----------+----------------------------+----------------------------+
| Command  | Set Command:               | Execute Command:           |
|          |                            |                            |
|          | 1. Single connection:      | AT+CIPSEND                 |
|          | (+CIPMUX=0)                |                            |
|          |                            | Function: to start sending |
|          | AT+CIPSEND=<length>        | data in transparent        |
|          |                            |                            |
|          | 2. Multiple connections:   | transmission mode.         |
|          | (+CIPMUX=1)                |                            |
|          |                            |                            |
|          | AT+CIPSEND=<link           |                            |
|          | ID>,<length>               |                            |
|          |                            |                            |
|          | 3. Remote IP and ports can |                            |
|          | be set in UDP              |                            |
|          |                            |                            |
|          | transmission:              |                            |
|          |                            |                            |
|          | AT+CIPSEND=[<link          |                            |
|          | ID>,]<length> [,<remote    |                            |
|          |                            |                            |
|          | IP>,<remote port>]         |                            |
|          |                            |                            |
|          | Function: to configure the |                            |
|          | data length in normal      |                            |
|          |                            |                            |
|          | transmission mode.         |                            |
+==========+============================+============================+
| Response | Send data of designated    | Wrap return > after        |
|          | length.                    | executing this command.    |
|          |                            |                            |
|          | Wrap return > after the    | Enter transparent          |
|          | Set Command. Begin         | transmission, with a 20-ms |
|          |                            |                            |
|          | receiving serial data.     | interval between each      |
|          | When data length defined   | packet, and a maximum of   |
|          | by                         |                            |
|          |                            | 2048 bytes per packet.     |
|          | <length> is met, the       |                            |
|          | transmission of data       | When a single packet       |
|          | starts.                    | containing +++ is          |
|          |                            | received,                  |
|          | If the connection cannot   |                            |
|          | be established or gets     | QCA4004 returns to normal  |
|          |                            | command mode.              |
|          | disrupted during data      |                            |
|          | transmission, the system   | Please wait for at least   |
|          |                            | one second before          |
|          | returns:                   |                            |
|          |                            | sending the next AT        |
|          | ERROR                      | command.                   |
|          |                            |                            |
|          | If data is transmitted     | This command can only be   |
|          | successfully, the system   | used in transparent        |
|          |                            |                            |
|          | returns:                   | transmission mode which    |
|          |                            | requires single            |
|          | SEND OK                    |                            |
|          |                            | connection.                |
|          | If it failed, the system   |                            |
|          | returns:                   | For UDP transparent        |
|          |                            | transmission, the value of |
|          | SEND FAIL                  |                            |
|          |                            | <UDP mode> has to be 0     |
|          |                            | when using AT+CIPSTART.    |
+----------+----------------------------+----------------------------+
| Note     | <link ID>: ID of the       |                            |
|          | connection (0~4), for      |                            |
|          | multiple                   |                            |
|          |                            |                            |
|          | connections.               |                            |
|          |                            |                            |
|          | • <length>: data length,   |                            |
|          | MAX: 2048 bytes.           |                            |
|          |                            |                            |
|          | [<remote IP>]: remote IP   |                            |
|          | can be set in UDP          |                            |
|          | transmission.              |                            |
|          |                            |                            |
|          | [<remote port>]: remote    |                            |
|          | port can be set in UDP     |                            |
|          | transmission.              |                            |
+----------+----------------------------+----------------------------+

4.4.5 AT+CIPCLOSE - Close TCP/UDP Connection
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+----------+----------------------------+----------------------------+
| Command  | Set Command (used in       | Execute Command (used in   |
|          | multiple connections):     | multiple                   |
|          |                            |                            |
|          | AT+CIPCLOSE=<link ID>      | connections):              |
|          |                            |                            |
|          | Function: close the        | AT+CIPCLOSE                |
|          | TCP/UDP Connection.        |                            |
+==========+============================+============================+
| Response | OK                         |                            |
+----------+----------------------------+----------------------------+
| Note     | <link ID>: ID of the       |                            |
|          | connection to be closed.   |                            |
|          | When ID                    |                            |
|          |                            |                            |
|          | is 5, all connections will |                            |
|          | be closed. (In server      |                            |
|          | mode, the                  |                            |
|          |                            |                            |
|          | ID 5 has no effect.)       |                            |
+----------+----------------------------+----------------------------+

4.4.6 AT+CIPMUX - Enable/Disable Multiple Connection
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+------------+---------------------------+---------------------------+
| Command    | Query Command:            | Set Command:              |
|            |                           |                           |
|            | AT+CIPMUX?                | AT+CIPMUX=<mode>          |
|            |                           |                           |
|            |                           | Function: to set the      |
|            |                           | connection type.          |
+============+===========================+===========================+
| Response   | +CIPMUX:<mode>            | OK                        |
|            |                           |                           |
|            | OK                        |                           |
+------------+---------------------------+---------------------------+
| Parameters | <mode>:                   |                           |
|            |                           |                           |
|            | 0: single connection      |                           |
|            |                           |                           |
|            | 1: multiple connections   |                           |
|            |                           |                           |
|            | The default mode is       |                           |
|            | single connection mode.   |                           |
|            |                           |                           |
|            | Multiple connections can  |                           |
|            | only be set when          |                           |
|            | transparent transmission  |                           |
|            | is disabled               |                           |
|            | (AT+CIPMODE=0).           |                           |
|            |                           |                           |
|            | This mode can only be     |                           |
|            | changed after all         |                           |
|            | connections are           |                           |
|            | disconnected.             |                           |
|            |                           |                           |
|            | If the TCP server is      |                           |
|            | running, it must be       |                           |
|            | deleted (AT+CIPSERVER=0)  |                           |
|            | before the single         |                           |
|            | connection mode is        |                           |
|            | activated.                |                           |
+------------+---------------------------+---------------------------+

4.4.7 AT+CIPSERVER - Create/Delete TCP server
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+-------------+-------------------------------------------------------+
| Set Command | AT+CIPSERVER=<mode>[,<port>]                          |
+=============+=======================================================+
| Response    | OK                                                    |
+-------------+-------------------------------------------------------+
| Parameters  | <mode>:                                               |
|             |                                                       |
|             | 0: deletes server.                                    |
|             |                                                       |
|             | 1: creates server.                                    |
|             |                                                       |
|             | <port>: port number; 333 by default.                  |
+-------------+-------------------------------------------------------+
| Notes       | A TCP server can only be created when multiple        |
|             | connections are activated (AT+CIPMUX=1).              |
|             |                                                       |
|             | A server monitor will automatically be created when   |
|             | the TCP server is created.                            |
|             |                                                       |
|             | When a client is connected to the server, it will     |
|             | take up one connection and be assigned an ID          |
+-------------+-------------------------------------------------------+
| Example     |                                                       |
+-------------+-------------------------------------------------------+

4.4.8 AT+SERVERMAXCONN - Set Max Connection Allowed By Server
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+------------+---------------------------+---------------------------+
| Commands   | Query Command:            | Set Command:              |
|            |                           |                           |
|            | AT+CIPSERVERMAXCONN?      | AT+CIPSERVERMAXCONN=<num> |
|            |                           |                           |
|            | Function: obtain the      | Function: set the maximum |
|            | maximum number of clients | number of clients allowed |
|            | allowed to connect to the | to connect to the TCP     |
|            | TCP server                | server                    |
+============+===========================+===========================+
| Response   | +CIPSERVERMAXCONN:<num>   | OK                        |
|            |                           |                           |
|            | OK                        |                           |
+------------+---------------------------+---------------------------+
| Parameters | <num>: the maximum number |                           |
|            | of clients allowed to     |                           |
|            | connect to the TCP        |                           |
|            | server, range: [1, 5]     |                           |
+------------+---------------------------+---------------------------+
| Notes      | To set this               |                           |
|            | configuration, you should |                           |
|            | call the command          |                           |
|            | AT+CIPSERVERMAXCONN=<num> |                           |
|            | before creating           |                           |
|            |                           |                           |
|            | a server.                 |                           |
+------------+---------------------------+---------------------------+

4.4.9 AT+CIPMODE - Set Transmission Mode
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+------------+---------------------------+---------------------------+
| Commands   | Query Command:            | Set Command:              |
|            |                           |                           |
|            | AT+CIPMODE?               | AT+CIPMODE=<mode>         |
|            |                           |                           |
|            | Function: to obtain       | Function: to set the      |
|            | information about         | transmission mode.        |
|            | transmission mode.        |                           |
+============+===========================+===========================+
| Response   | +CIPMODE:<mode>           | OK                        |
|            |                           |                           |
|            | OK                        |                           |
+------------+---------------------------+---------------------------+
| Parameters | <mode>:                   |                           |
|            |                           |                           |
|            | 0: normal transmission    |                           |
|            | mode.                     |                           |
|            |                           |                           |
|            | 1: UART-Wi-Fi passthrough |                           |
|            | mode (transparent         |                           |
|            | transmission), which can  |                           |
|            | only be enabled in TCP    |                           |
|            | single connection mode or |                           |
|            | in UDP mode when the      |                           |
|            | remote IP and port do not |                           |
|            | change.                   |                           |
+------------+---------------------------+---------------------------+
| Notes      | The configuration changes |                           |
|            | will NOT be saved in      |                           |
|            | flash.                    |                           |
|            |                           |                           |
|            | During the UART-Wi-Fi     |                           |
|            | passthrough transmission, |                           |
|            | if the TCP connection     |                           |
|            | breaks, BFQ4004 will keep |                           |
|            | trying to reconnect until |                           |
|            | +++ is input to exit the  |                           |
|            | transmission. If it is a  |                           |
|            | normal TCP transmission   |                           |
|            | and the TCP connection    |                           |
|            | breaks, BFQ4004 will give |                           |
|            | a prompt and will not     |                           |
|            | attempt to reconnect.     |                           |
+------------+---------------------------+---------------------------+

4.4.10 +IPD - Receive Network Data
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+------------+---------------------------+---------------------------+
| Commands   | Single connection:        | multiple connections:     |
|            |                           |                           |
|            | (+CIP                     | (+CIPMUX=1)+IPD,<link     |
|            | MUX=0)+IPD,<len>[,<remote | ID>,<len>[,<remote        |
|            | IP>,<remote port>]:<data> | IP>,<remote port>]:<data> |
+============+===========================+===========================+
| Parameters | The command is valid in   |                           |
|            | normal command mode. When |                           |
|            | the module receives       |                           |
|            | network data, it will     |                           |
|            | send the data through the |                           |
|            | serial port using the     |                           |
|            | +IPD command.             |                           |
|            |                           |                           |
|            | [<remote IP>]: remote IP, |                           |
|            | enabled by command        |                           |
|            | AT+CIPDINFO=1.            |                           |
|            |                           |                           |
|            | [<remote port>]: remote   |                           |
|            | port, enabled by command  |                           |
|            | AT+CIPDINFO=1.            |                           |
|            |                           |                           |
|            | <link ID>: ID number of   |                           |
|            | connection.               |                           |
|            |                           |                           |
|            | <len>: data length.       |                           |
|            |                           |                           |
|            | <data>: data received     |                           |
+------------+---------------------------+---------------------------+

.. _section-1:
