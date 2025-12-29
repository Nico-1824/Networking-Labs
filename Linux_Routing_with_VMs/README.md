Goal

The goal of this lab was to apply rouitng knowledge to real machine and get used to working with Virtual Machines. The topology consists of:
  - 2 end host Linux Ubuntu Machines with subnets 10.0.1.0/28 and 10.0.2.0/28
  - 1 routing Linux Ubuntu Server

The virtual machines were run in a containerized Docker environment that is outlined in the compose.yaml file to make everything easy to run and reproducable.

Challenges

1. Inter-subnet Ping Failure

After SSHing into one end host, I attempted to ping the other host in the opposite subnet. The ping failed, although both hosts could successfully ping the router’s interfaces.

This suggested that Layer 3 connectivity to the router was working, but traffic was not being forwarded between subnets. I first checked the router’s routing table using:

ip r

The router showed connected routes for both 10.0.1.0/28 and 10.0.2.0/28 out different interfaces, indicating that its routing table was correct.

Next, I inspected the routing tables on both end hosts. This revealed the issue: Docker had automatically configured the default gateways as 10.0.1.1 and 10.0.2.1. However, the router’s actual interface addresses were 10.0.1.2 and 10.0.2.2. As a result, packets destined for the other subnet were being sent to the wrong next hop.
To fix this, I replaced the default routes on each end host:

ip route replace default via 10.0.1.2
ip route replace default via 10.0.2.2

After correcting the gateways, end-to-end connectivity between the two hosts was restored.

Conclusion

I learned how to write container yaml to quickly and repeatly create virtual machines to simulate real networks. I also learned how to accurately debug and diagnose a network 
when communication is failing between end hosts. I also learned how to prepare new machines, install libraries to help debugging, and reconfigure a network when machines are 
misconfigured. Most importantly, I learned how small misconfigurations at Layer 3 can completely break communication, and how to methodically trace and fix such issues.
