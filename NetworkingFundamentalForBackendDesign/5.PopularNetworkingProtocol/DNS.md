### Popular Networking Protocols

> Every time you type in a URL , the first that happens is query to DNS , DNS resolvers will find out the IP address, that is matching that domain so that we can turn around and use TCP IP in order to establish TCP IP handshake to that IP address

DNS: (Domain Name System)

Why DNS 
> - people can't remember IPs
> - A domain is a text points to an IP or a collection of IPs
> - Additional layer of abstraction is good 
> - IP can change while the domain remain
> - We can serve the closest IP to a client reqeusting the same domain 
> - Load Balancing 

www.abc.com

www => subdomain 
abc => actual domain
com => top level domain

> - A new addressing system means we need a mapping. Meet DNS 
> - If You have an IP and you need the MAC , we use ARP 
> - But if you have the name and you need the IP , we use DNS to map name to the IP
> - Built on top of UDP
> - Port 53 , (reserved port for DNS)
> - Many records (MX, TXT, A, CNAME)

How DNS Works 
# DNS resolver - frontend and cache 
# ROOT server - Hosts IPs of the ANS (this will not know but it will redirect to the one who will know is TLD )
# TOP level domain server - Hosts IPs of the ANS (after root server it will ask the TLD of the .com or .org whatever , then get me Authoritative name server that might have the answer, this is where you registered your domain)
# Authoritative Name server -  hosts the IP of the target server 
