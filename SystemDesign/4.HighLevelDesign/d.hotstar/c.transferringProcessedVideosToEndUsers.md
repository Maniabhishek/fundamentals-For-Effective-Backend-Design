### Transferring Processed videos to end users
- lets think it the backwards way , how you are going to transport the video to end user
- when you are sending video or images to end users you are doing it over CDNs , which take your videos and publish it to the end users
- sometime its also called edge server
- now users most likely going to be connecting over HTTP because they are connecting through browser
- what kind of protocol we will end up using here, if you have an iPhone you will be using HLS (HTTP Live Streaming) and if you have any other operating system you are probably using DASH
- Why DASH or HLS , because these protocols have adaptive bitrate with which , these protocols judiciously utilizes netwrok bandwidth
- in case if some users doesnt have good network then there is no point in serving high quality video , video quality will be decreased , basically browser will understand users network speed and then server will send the video accordingly


<img width=600 height=400 src="https://github.com/user-attachments/assets/38acbd23-617d-4913-bfbe-f12bac69be1d">

- now the question arises is that how are we going to send the processed video to end users
- we will setup multiple servers in different locations as shown in image below
- why different servers and directly , well the speed of propagation of video might not be fast , to speed things up we will be using severs in different countries locations
- processed video will be transferred using **RTMP** , cannot use DASH or HLS as RTMP gurantees the video quality and everything , and at user side we are using DASH or HLS just because we may have to compromise with the quality and reliable transfer
- from servers to CDNs also we will use RTMP to transfer the videos
- in case of directly sending the video from server to users we will be using HLS or DASH (HLS and DASH HTTP based (works via TCP) maintains orderly transfer)
- another thing we can use is WebRTC (peer to peer based (works via UDP might send unordered chunks))
- DASH HLS is mostly designed for live streaming 

<img width=600 height=800 src="https://github.com/user-attachments/assets/ac7f170e-d43d-463b-9450-6d94c74ebdd8">

<img width=600 height=800 src="https://github.com/user-attachments/assets/73477474-1c24-434d-b97c-cc9128ab2164">

<img width=600 height=800 src="https://github.com/user-attachments/assets/38be3dcc-9006-47aa-abf7-7ccf35da4bcb">

<img width="1445" height="816" alt="image" src="https://github.com/user-attachments/assets/7a4a798f-d01c-4bcc-8c10-95f59262e714" />


<img width="1820" height="1037" alt="image" src="https://github.com/user-attachments/assets/21a3244a-d797-4a77-bc23-61cba7aff4d5" />
