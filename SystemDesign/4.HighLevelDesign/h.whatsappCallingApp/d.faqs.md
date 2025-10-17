1. Can a call be made from a VOIP user to a PSTN user?
> Yes. The connection is 'bridged' on the switch. It's like taking data in two different languages and translating them for each side. If A is on VOIP and B on PSTN: VOIP data from A is translated to PSTN and sent to B. PSTN data from B is translated to VOIP and sent to A.
2. How are calls routed in PSTN?
> In comparison with the internet: PSTN is a set of telephone routers. The Internet is a set of IP routers. Your phone sends a request to your network provider, which uses spectrum. Whatsapp instead sends the request to your ISP, which uses fibre optic cables.
3. Will both the discussed approaches to designing a solution pass in an interview? 
> Yes. The first one is acceptable by an engineer with less than 10 years of experience. The interviewer can help them along the way. Topics like PSTN and VOIP calls are not dealt with by every engineer. The interviewer may explain the terms then. However, senior engineers are expected to be well versed with long running transactions, state machines and so on. They are also expected to know about networking protocols like SIP and VOIP.
4. Can I be expected to code some part of the system during the interview? 
> Although not likely, an engineer can be asked to code some parts of the system. This will be discussed further in the LLD videos of the series. 5. Does every component of the system need an explanation? Sometimes you can mention what a service does and treat it as an abstraction. Mentioning real-world implementation examples help: a) Service Discovery → Built using Zookeeper b) Recommendation Engine → Kafka can be used for data pipelines.(Hadoop is useful for batch processing. Spark for real time processing.) c) Telemetry and logging → ELK stack d) Gateway → Elastic Load Balancer e) Message Queue → Kafka

6. Is this extensible for video calls?
> A lot of the ideas can be extended to video calling. We will be talking about them in the coming videos.
7. What is the full form of PSTN? Which companies use it?
> It stands for Public Switched Telephone Network. The network is used to make phone calls across the globe, by multiple phone service providers.
8. Choice of databases? Can we use RDBMS at Whatsapp scale?
> An event driven system seems suitable here. That would require persistence of the log of events, and a view of the current state of each call. The log of events can be persisted in a file storage system like Hive (Cheap storage). The current/final state of ongoing calls can be stored in an RDBMS for fast queries. The reason for choosing RDBMS is possible transaction guarantees required for a long running call.
9. Any security issues or encryption to keep in mind?
> VOIP can be encrypted end-to-end using a secure transport protocol like SRTP. PSTN has been here for a long time, and listening in on a PSTN conversation requires physical access to the wires involved. That is difficult for anybody other than the government to do. Some governments make recording of calls from suspicious parties a mandate.
10. What if I want to add a caller-tune? Where should it go?
> We can store the audio files in the switch. If a user asks for a caller tune, we store a key-value pair of UserId -> mediaID. We then play the media file on the calling side when the receiver is called at the switch, till we hit the 'pickup' state. 
