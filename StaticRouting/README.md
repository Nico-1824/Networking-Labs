Goal

The goal of this lab was to practice configuring Static Routing and the OSPF routing protocol. I created a simple network consisting of:

- Two PCs
- Three routers

This required configuring routing not only for each host network, but also between routers to allow end-to-end communication. I began by assigning IP addresses and verifying interface connectivity before configuring any routing.

Challenges:
1. Incorrect IP Addressing

   I had set up the ip addresses for the PCs and the router interfaces completely wrong. I mistakenly put each interface and PC on a different subnet which caused none of the interfaces to be able to communicate with each other and the routes to be unreachable. Originally I had the network topology set up like in figure 1. The ips were all seperate and when I would run the ping command to the PCs all the packets were dropped. I figured out that the problem was with the ip configuration when I tried to ping the default gateway for PC0 and it still was dropping packets. I solved this issue by putting the PCs on the same subnet as there respective router (e.g. for PC0 the network range was 192.168.10.0 - 192.168.10.255 and PC1 the network range was 192.168.40.0 - 192.168.40.255). This allowed me to ping my default gateway from both PCs. I then configured the router interfaces by running these series of command in the CLI: "configure terminal", "interface fa0/0", "ip route destination_ip 255.255.255.0 next_hop_ip". I did this for each router until each router directed traffic to the correct next hop.
2. Incorrect Next-Hop Configuration

   My second challenge was setting up the routes correctly which is where traceroute gave useful insight to the network topology. I was having an issue with router 0 getting to PC1. To solve this I ran a traceroute command from PC0 to PC1 ip address 192.168.40.10 and noticed it got out the default gateway but then dropped. This is where I realized the routing from router0 to router1 was misconfigured with the wrong next hop and needed to be updated to the correct ip as shown in figure 2. 

OSPF:
The next part of the lab was to setup a single area OSPF network so I enabled OSPF on all the routers by running "ip ospf 1 area 0" in the interface configuration mode for all the routers. I then ensured that the configuration was correct by running "show ip ospf neighbors" to see the neighbors table. I then added a switch so that another PC could be added to the network to test if the network could be added to without issues.

Conclusion:
In this lab I learned how to accurately troubleshoot a network, how routers forward traffic using static and dynamic routes, and how OSPF builds its Link-State Database (LSDB) using hello messages. Using traceroute allowed me to follow packet paths and pinpoint exactly where routing failures occurred, simulating the type of diagnostic work done by network technicians in the field. Overall, this lab strengthened my understanding of routing fundamentals and OSPF operations.
