# Distributed System – Parameter Passing Semantics in RPC

A Distributed System is a Network of Machines that can exchange information with each other through Message-passing. It can be very useful as it helps in resource sharing.

## Parameter Passing Semantics in RPC:
The parameter passing is the only way to share information between clients and servers in the Remote Procedure Call (RPC).
The following are the various semantics that is used in RPC for passing parameters in distributed applications:
1. Call-by-Value:  The client stub copies and packages the value from the client into a message so that it can be sent to the server through a network.
   * Parameter marshaling is the process of wrapping up parameters into a message. Consider the remote procedure add(x, y), which returns the addition of two integer parameters.
