The goal of this lab was to practice the topic of Static Routing and the OSPF routing protocol. I wanted to build a simple network that had multiple routers to practice configuring them and getting two networks to speak to each other. The way I set it up was having:
- two PCs
- three routers

This made it so that I would need to setup the routes to not only the host router of each network but also the router to connect the network routers to challenge myself. I started by first configuring the routers and ensuring that the routes we set up so that the PCs could talk to each other.

Challenges:
At first I had set up the ip addresses for the PCs and the router interfaces completely wrong. I mistakenly put each interface and PC on a different subnet which caused none of the interfaces to be able to communicate with each other and the routes to be unreachable. Originally I had the network topology set up like in figure 1.
