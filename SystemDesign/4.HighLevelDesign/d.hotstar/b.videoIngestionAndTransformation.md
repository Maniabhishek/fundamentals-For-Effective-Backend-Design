<img width=600 height=800 src="https://github.com/user-attachments/assets/d830db20-1111-4c59-9675-82fab87691a0">

- so what we are doing , we are going to be using RMTP to transfer live stream video to our transformation service
- from transformation service , we will publish message at its own pace to message queue
- and then we will have different workers subscribing to these messages in order to process the videos in multiple fomat vs different codecs, 360p 460p of DASH , HLS ABR
- once these videos are converted it will store these vides into DFS (distributed file system) , and will also publish these data to queue
- then we will have subscriber subscribing to these messages which then will sent to end users
- we can also do another thing once worker finishes their job we will let transformation service know that worker has completed one task you push message again to queue
