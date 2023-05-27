# MSS/MTU/PMTUD

> - TCP layer 4 unit is segment 
> - The segment slides into an IP packet in layer 3
> - The IP packet now has the segment + headers 
> - The IP packet slides into a layer 2 frame 
> - The frame has a fixed size based on the networking configuration
> The size of the frame determines the size of the segment

# Hardware MTU 
> - Maximum transmission Unit (MTU) is the size of the frame
> - It is a network property default 1500
> - some network have jumbo frames up to 9000 bytes 
> - are there networks with larger MTUs?
>
>> well we can say yes , for example, amazon can have more that 1500 bytes of MTU internally, if you own all the hardware and everything why not.. so you need really beefy network interfaces that handles that, but the larger the frame , lower the latency because you are going to shove more content in your frame then you dont have to send more IP packets and that goes if it reaches in one piece , but there is limitation , you wont know if that IP packet is not corrupted , but if it's network is unstable , then sending larger IP packet is probably a bad idea because in this case any bit is flipped that IP packet is invalid 

# IP packets and MTU
> - The IP MTU is usually equals the hardware MTU (which is low level network interface MTU) 
> - One IP packet **should** fit a single frame 
> - Unless IP fragmentation is in place 
> - Larger IP packets will be fragmented into a multiple frames 

# MSS 
> - Maximum segment size is determined based on MTU 
> - Segment must fit in an IP packet which should fit in a frame 
> - MSS = MTU - IP Address - TCP Headers = 1460
> - 1460 bytes can only be fit nicely into a single MSS
> - which fits in a single frame 

# Path MTU Discovery (PMTUD)
> - MTU is network interface property each host can have different value 
> - You really need to use the smallest MTU in the network 
> - Path MTU help determine the MTU in the network path 
> - Client sends a IP packet with its MTU with DF(dont fragment) flag 
> - The host that their MTU is smaller will have to fragment but can't (with a DF flag)
> - The host sends back an ICMP message fragmentation needed which will lower the MTU
>> for example we have a network with different MTUs at different hosts which is MTU: 9000 =>  MTU: 1500 => MTU: 512 => MTU: 1500 , now in this example user is send ing the frame of size 9000 and with a DF flag which means dont fragment if you encounter, if my frame is bigger than your MTU then fail and let me know (inform me ) but how do you tell me , through ICMP , usually the one thich has smaller MTU will have to fragment but can't because of DF flag, so the host sends back ICMP message fragmentation neeeded which will lower the MTU 

1. MTU is the maximum transmission unit on the device 
2. MSS is the maximum segment size at layer 4 
3. if you can fit more data into a single segment you lower latency
4. It lowers overhead from header and processing 
5. path MTU can discoverthe network lowest MTU with ICMP 
6. Flow control/congestion control still allows sending multiple segments with ack
