## Transport Layer Security (TLS)

### Intro
***
- It is designed to facilitate privacy and data security for communications over the Internet.
- A primary use case of TLS is encrypting the communication between web applications and servers, such as web browsers loading a website.


### Difference Between TLS and SSL
*** 
- TLS was evolved from a previous protocol called Secure Sockets Layer (By Netscape)
- SSL 3.1 was TLS its name was changed to indicate that it was no longer associated with Netscape


### HTTPS and TLS
*** 
- HTTPS is an implementation of TLS encryption on top of HTTP protocol, which is used by all websites as well as some other web service.
- Any website that uses HTTPS is therefore employing TLS encryption.

### what does it do ?
*** 
#### TLS accomplishes three main components
- Encryption: hides the data being transferred from third parties.
- Authentication: ensures that the parties exchanging information are who they claim to be.
- Integrity: verifies that the data has not been forged or tampered with.


### How does TLS work 
***
- It is initiated using a sequence known as the TLS handshake
- when a user navigates to a website that uses TLS, the TLS handshake begins between the user's device (also known as the client device) and the web server
- During the TLS handshake the user's device and webserver:
  - Specify which version of TLS (TLS 1.0, 1.2, 1.3, etc.) they will use
