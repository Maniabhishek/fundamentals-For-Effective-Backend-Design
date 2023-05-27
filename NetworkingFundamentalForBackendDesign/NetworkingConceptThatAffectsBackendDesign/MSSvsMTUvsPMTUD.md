# MSS/MTU/PMTUD

> TCP layer 4 unit is segment 
> The segment slides into an IP packet in layer 3
> The IP packet now has the segment + headers 
> The IP packet slides into a layer 2 frame 
> The frame has a fixed size based on the networking configuration
> The size of the frame determines the size of the segment

# Hardware MTU 
> Maximum transmission Unit (MTU) is the size of the frame
> It is a network property default 1500
> some network have jumbo frames up to 9000 bytes 
> are there networks with larger MTUs?
>
>> well we can say yes , for example, amazon can have more that 1500 bytes of MTU internally, if you own all the hardware and everything why not.. so you need really beefy network interfaces that handles that, but the larger the frame , lower the latency because you are going to shove more content in your frame then you dont have to send more IP packets and that goes if it reaches in one piece , but there is limitation , you wont know if that IP packet is not corrupted , but if it's network is unstable , then sending larger IP packet is probably a bad idea because in this case any bit is flipped that IP packet is invalid 

# IP packets and MTU
> The IP MTU is usually equals the hardware MTU 
> One IP packet should fit a single frame 
> Unless IP fragmentation is in a place 
> Larger IP packets will be fragmented into a multiple frames 

