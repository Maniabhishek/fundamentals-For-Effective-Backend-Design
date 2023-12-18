### Popular Networking Protocols

> Every time you type in a URL , the first that happens is query to DNS , DNS resolvers will find out the IP address, that is matching that domain so that we can turn around and use TCP IP in order to establish TCP IP handshake to that IP address

DNS: (Domain Name System)

Why DNS 
> - people can't remember IPs
> - A domain is a text points to an IP or a collection of IPs
> - Additional layer of abstraction is good 
> - IP can change while the domain remain
> - We can serve the closest IP to a client reqeusting the same domain 
> - Load Balancing (client side load balancing with multiple IP address on a single domain nam)

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

How DNS Works (there are four servers invloved in loading a webpage)
> -  DNS resolver - frontend and cache 
> - ROOT server - Hosts IPs of the TLDs(top level domain servers) (this will not know but it will redirect to the one who will know is TLD )
> - TOP level domain server - Hosts IPs of the ANS (after root server it will ask the TLD of the .com or .org whatever , then get me Authoritative name server that might have the answer, this is where you registered your domain)
> - ANS (authoritative name server, it can be cloudflare , google , amazon etc.,) This final nameserver can be thought of as a dictionary on a rack of books, in which a specific name can be translated into its definition. The authoritative nameserver is the last stop in the nameserver query. If the authoritative name server has access to the requested record, it will return the IP address for the requested hostname back to the DNS Recursor (the librarian) that made the initial request.
> - Authoritative Name server -  hosts the IP of the target server
>> - The process of DNS resolution involves converting a hostname (such as www.example.com) into a computer-friendly IP address (such as 192.168.1.1)
>> - When a user wants to load a webpage, a translation must occur between what a user types into their web browser (example.com) and the machine-friendly address necessary to locate the example.com webpage.

### The 8 steps in a DNS lookup: 
> - A user types ‘example.com’ into a web browser and the query travels into the Internet and is received by a DNS recursive resolver.
> - The resolver then queries a DNS root nameserver (.).
> - The root server then responds to the resolver with the address of a Top Level Domain (TLD) DNS server (such as .com or .net), which stores the information for its domains. When searching for example.com, our request is pointed toward the .com TLD.
> - The resolver then makes a request to the .com TLD.
> - The TLD server then responds with the IP address of the domain’s nameserver, example.com.
> - Lastly, the recursive resolver sends a query to the domain’s nameserver.
> - The IP address for example.com is then returned to the resolver from the nameserver.
> - The DNS resolver then responds to the web browser with the IP address of the domain requested initially.
Once the 8 steps of the DNS lookup have returned the IP address for example.com, the browser is able to make the request for the web page:
> - The browser makes a HTTP request to the IP address.
> - The server at that IP returns the webpage to be rendered in the browser (step 10).
