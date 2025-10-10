### Transferring Processed videos to end users
- lets think it the backwards way , how you are going to transport the video to end user
- when you are sending video or images to end users you are doing it over CDNs , which take your videos and publish it to the end users
- sometime its also called edge server
- now users most likely going to be connecting over HTTP because they are connecting through browser
- what kind of protocol we will end up using here, if you have an iPhone you will be using HLS (HTTP Live Streaming) and if you have any other operating system you are probably using DASH
- Why DASH or HLS , because these protocols have adaptive bitrate with which , these protocols judiciously utilizes netwrok bandwidth
- in case if some users doesnt have good network then there is no point in serving high quality video , video quality will be decreased , basically browser will understand users network speed and then server will send the video accordingly
- 
