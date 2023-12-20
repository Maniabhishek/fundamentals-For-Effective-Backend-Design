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
  - Decide on which cipher suites they will use
  - Authenticate the identity of the server using the server's TLS certificate
  - Generate session keys for encrypting messages between them after the handshake is complete
- The TLS handshake establishes a cipher suite for each communication session
- The cipher suite is a set of algorithm, which specifies the details such as which shared encryption key or session keys, will be used for that particular session.
- TLS is able to set the matching session keys over an unencrypted channel thanks to a technology known as public key cryptography.
- The handshake also handles authentication, which usually consists of the server proving its identity to the client. This is done using **public keys**.
- Public keys are encryption keys that use one-way encryption, meaning that anyone with the public key can unscramble the data encrypted with the server's private key to ensure its authenticity, but only the original sender can encrypt data with the private key. The server's public key is part of its TLS certificate.
- Once data is encrypted and authenticated, it is then signed with a message authentication code **(MAC)**. The recipient can then verify the MAC to ensure the integrity of the data.
