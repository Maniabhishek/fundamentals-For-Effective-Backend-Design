-  we are designing calling app where basically a mobile app sends signal to another app , establish a connection and maintains the connection once call is picked up , and then finally terminate , this is similar to how we create connection and connect to a server

<img width="649" height="729" alt="image" src="https://github.com/user-attachments/assets/7a28d127-3927-41d5-bd33-02f21193e9c0" />

- there are two major protocols for voice call
    - VOIP (free) 
    - PSTN (Paid)

- Advantages of VOIP
    - Free, easy hardware and code setup
    - Data send in demand 
- disadvantage
    - needs internet connectivity
    - call quality depends on network strength

- In case VOIP , when there is no voice no packets will be sent , but in case of PSTN it blocks certain amount of bandwidth for for both the user , it continuously sends data from A to B



- in the image we can see if a user B wants to make a call over PSTN, lets say B has its number and A has its own number , to establish a call, you neeed some bandwidth allocated for you and some bandwidth allocated for other whom you want to call in the switch
- In case of VOIP (when A wants to connect to B) it first make request to call manager where it validate the user id , whether the user is valid , and the requesting user is valid, or the other has blocked it, several validation which happens in call manager , and then request goes to session service to get the connection ID of user B , this connection ID , will be on any of the boxes on switch, once the connection ID is fetched by call manager , now the two user can connect on the switch and share voice, well these call cna termed as state , connected , validated , ringing , Answered , Terminated, and these can be represented by CODE very similar to HTTP code , here in this case very perfect protocol is SIP  (Session initiation protocol)

<img width="679" height="565" alt="image" src="https://github.com/user-attachments/assets/4898d3e2-b64e-48b0-9c22-a10fcc7a0497" />

- how does the app start charging , well everytime the switch changes its state , it will notify the call manager , and call manager when it see the state call started it can save the infor and start coutning and from there on , once call is disconnected and get the new state , they can find out how long the call went through , then they can send this info to payment service 


### Charging users , have a billing service , which will just return whether the call can go through , we will have things stored in another service already , maxtime duration a caller can have this way it will be simpler

<img width="1720" height="1046" alt="image" src="https://github.com/user-attachments/assets/24f2d19d-795d-4a4a-aef7-3ec8420971dc" />
