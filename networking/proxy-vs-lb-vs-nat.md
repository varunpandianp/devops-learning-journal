Basic Doubts -regarding forward and reverse proxy

1. Forward Proxy vs NAT Gateway
   Many beginners confuse these because both can hide private IP addresses.
   The main difference:
   Forward Proxy works at the application level (HTTP/HTTPS).
   NAT Gateway works at the network level (IP translation).

2. Reverse Proxy vs Load Balancer
   This is another common confusion.
   The relationship:
   A Load Balancer can act as a Reverse Proxy.
   But every reverse proxy is not necessarily a load balancer.

4. AWS NAT Gateway vs Internet Gateway
   Very important AWS networking concept.

Internet Gateway (IGW)
Purpose:
Allow public resources to communicate with the internet.
NAT Gateway
Purpose:
Allow private resources to access the internet.
Architecture:
Private EC2
|
|
NAT Gateway
|
|
Internet Gateway
|
|
Internet
Private EC2:
Forward Proxy:
Client → Proxy → Internet
Controls users.

NAT Gateway:
Private Server → NAT → Internet
Allows outbound internet.

Reverse Proxy:
User → Proxy → Backend
Protects servers.

Load Balancer:
User → LB → Multiple Servers
Distributes traffic.

Nginx:
Common reverse proxy tool.

Internet Gateway:
Public subnet ↔ Internet.

NAT Gateway:
Private subnet → Internet only.
