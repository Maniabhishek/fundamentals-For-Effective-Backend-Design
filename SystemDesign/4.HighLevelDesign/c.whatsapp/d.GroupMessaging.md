- so in the image we can see we parser and unparser service , for parsing the message as per our service which is being used internally
- unparser service will convert the message into sensible messages , you have https to communicate from client to gateway then internally you can have something different like thrift used by facebook
- now this request will go session service and then group service this group service will store the groupId and userId , now once the message is being sent you can responsd back to user saying message was sent, same can be done once all the users in the group has received the message we can say delivered
- in case of any failure we will use queue for retry it will retry n number of times and then again if it fails then we can just inform user saying the message was not delivered


![image](https://github.com/user-attachments/assets/c9196e86-4364-4fbf-bc3e-cf9de3369c33)

