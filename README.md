# Two-switch-network
Designed and configured a basic Local Area Network (LAN) using Cisco Packet Tracer, connecting multiple devices through a network switch, assigning IP addresses, and verifying connectivity

Objective - investigate how devices on  a two switch network communicate.

Tasks: 

- Connect 4 PCs across 2 switches.
    
- Configure IP addresses within the same subnet.
    
- Verify communication between PCs on different switches using `ping`.
    
- Examine the switches' MAC address tables.
    
- Understand how Ethernet frames travel between switches.
    



I investigated how PC's connected to different switches were able to communicate with one another.


<img width="372" height="427" alt="image" src="https://github.com/user-attachments/assets/c4c1808b-0a79-4a04-a1c6-c36a14e61dee" />


Where PC1 is connected to switch 0 where its IP is 128.8.01.01 whereas PC2 is of an IP address of 128.8.01.03. We can successfully ping PC3 from PC1 as is shown below. 


<img width="952" height="502" alt="image" src="https://github.com/user-attachments/assets/049bbb5f-700c-4c52-a21f-e0ab2f4f20ed" /> *Please note IP incorrectly formatted on first attempt resulting in request timing out*

<img width="930" height="277" alt="image" src="https://github.com/user-attachments/assets/b16b215f-1a04-4dc7-b25f-89a03416a2c8" /> In the above MAC address table for switch0 we can see how switch0 uses port Fa0/1 to communicate with both devices PC2 and PC3. 

<img width="312" height="395" alt="image" src="https://github.com/user-attachments/assets/5207151f-367b-4a57-a065-0a5991a25fbd" />

When communicating with another device on a different switch, the process is similar to a single-switch network. If PC0 is to communicate with PC3, it must first know PC3's IP address. PC0 will then use its subnet mask to determine whether PC3 belongs to the same network.

If PC0 does not already have PC3's MAC address in its ARP cache, it will send out an ARP request to find the MAC address associated with said IP address. Switch0 will forward this ARP request to PC1 and Switch1, where Switch1 will forward the ARP request to both PC2 and PC3.

PC3, which possesses the relevant IP address, will then send back an Ethernet frame containing an ARP reply with its MAC address to Switch1. Switch1 will then store the MAC address of PC3 with the port number Fa0/3 in its MAC address table.

This Ethernet frame is then forwarded to Switch0. Switch0 will associate the MAC address of PC3 with Fa0/1, and the ARP reply is forwarded to PC0. PC0 now stores PC3's IP-to-MAC address association in its ARP cache after receiving the reply.

To communicate with PC3, PC0 will now send an Ethernet frame with the destination MAC address of PC3 to Switch0. Switch0 will consult its MAC address table and forward it through port Fa0/1 to Switch1. After receiving the Ethernet frame, Switch1 will consult its own MAC address table to determine that PC3 is reachable through Fa0/3, then forward the frame through this port to PC3.

<img width="170" height="447" alt="image" src="https://github.com/user-attachments/assets/662ab161-91f3-489f-a4d4-6bfe651d958d" />


What was learnt:


- How multiple switches can operate together within the same LAN.
    
- How subnet masks distinguish the network and host portions of an IP address.
    
- How ARP resolves IP addresses to MAC addresses.
    
- How switches learn MAC addresses and associate them with physical ports.
    
- Why multiple MAC addresses can be associated with a single switch port.
    
- How switches use MAC address tables to forward Ethernet frames between devices.
    
- How physical connection failures affect network connectivity and how to troubleshoot them.

