1. How much video will need to be processed per live stream?
- Let us assume 8k footage being captured in the event. We can assume that the highest resolution devices consuming it will be 4K devices (2160p). But we can restrict ourselves to serve upto HD for live streams.
- Let us assume that the resolutions we want to serve are 1080p, 720p, 480p and 360p. Let us also assume that the encoding of these videos is h.264.
- A cricket match lasts for approximately 10 hours. A 2 hour HD movie is about 2 GB in size.
- We assume that a cricket match will be about 10 GB in size.
- => 720p footage will be about 10 / 2 = 5 GB.
- => 480p footage will be about 10 / 4 = 2.5 GB.
- => 360p footage will be about 10 / 8 = 1.25 GB.
- That's roughly 18.75 GB considering all resolutions.
- The raw video will be broken into segments, and each segment will be processed into multiple resolutions and codecs. Let us assume we have 4 codecs. That's roughly 18.75 * 4 = 75 GB.

2. How much data will be transferred from a CDN to users in a single live stream?
- Assume the number of users watching a match = 10 million.
- Assume 50% having HD devices, and 50% having mobile 480p devices.
- Assume that a user watches 50% of a live stream on average.
- For a 10 hour match, that's 10 GB in HD. It's 10 / 4 = 2.5 GB in 480p.
- Total data transfer = SUM(size_of_video_type * number_of_users_for_type) *
average_watch_percentage = (10 GB * 50/100 * 10^6 + 2.5 GB * 50/100 * 10^6) * 50/100 = 3.125 * 10^6 GB = 3.125 PB.

3. How much time would it take to send data from the event to a users' device?
- Amount of data being consumed by a user every second = 10 GB/10 hours
- 1 GB / 3600 seconds = 300 KB per second.
- Refer below numbers at : http://highscalability.com/numbers-everyone-should-know
- Assume the time to transfer 300 KB of data from the nearest CDN server to a user's device is 1 second.
- Assume that the time it takes to transfer 300 KB of data from our nearest geographical server to the CDN server is also 150 ms.
