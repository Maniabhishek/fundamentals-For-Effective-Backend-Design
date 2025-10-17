<img width="1411" height="777" alt="image" src="https://github.com/user-attachments/assets/3fc88627-ac05-4e9f-b4e0-da43239e54d9" />

- once we have data inside the data lake , this is completely unstructured data, now to make sense out of these data , and before passing it to downstream services we will first make sensible filter , will do logical mapping of the data , and also if necessary sort the data
- now when the downstream services like machine learning system , analytics services or anomaly detection system can use these data more efectively and efficiently
- no single point of failure , even if one of the boxes fails , then only data relevant to that box will be lost


### Fault tolerance 
- in the above image we can see we have many boxes and dependencies , what we can do is we can create intermdiary table , instead of having only push architecture from one box to another we can have hybrid approach , where lets say from the first filter phase once any boxes are done it will push the data to intermediary table and then this data can be pulled from subsequent boxes
