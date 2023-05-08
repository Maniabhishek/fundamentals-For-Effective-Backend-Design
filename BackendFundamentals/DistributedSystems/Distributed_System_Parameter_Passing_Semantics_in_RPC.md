# Distributed System – Parameter Passing Semantics in RPC

A Distributed System is a Network of Machines that can exchange information with each other through Message-passing. It can be very useful as it helps in resource sharing.

## Parameter Passing Semantics in RPC:
The parameter passing is the only way to share information between clients and servers in the Remote Procedure Call (RPC).
The following are the various semantics that is used in RPC for passing parameters in distributed applications:
1. **Call-by-Value**:  The client stub copies and packages the value from the client into a message so that it can be sent to the server through a network.
   * Parameter marshaling is the process of wrapping up parameters into a message. Consider the remote procedure add(x, y), which returns the addition of two integer parameters.
   * The client stub stores its two parameters in a message, along with the name or number of the called method.
   * The stub evaluates the message when it arrives at the server to determine which method is required, and then performs the necessary call.
   * The client puts the server’s result into a message after the execution has been completed by the server. Then this message is received by the client stub and 
      its unpacking is carried out before returning the value to the client procedure.
   * This parameter parsing semantic works well as long as the client and server computers are similar and all parameters and outcomes are scalar types like Booleans, characters,
      and integers.
2. **Call-by-Reference**: Call-by-Reference simply means that pointers to the parameters are transferred from the client to the server. In some RPC techniques, parameters can be
     passed by reference. Employed in closed systems in which multiple processes share a single address.
   * Parameters can be passed by reference in distributed systems with distributed shared memory techniques, for example.
     If on the client-side, the second parameter is the buffer’s address, suppose 100 then one cannot simply provide 100 to the server and expect it to function as address 100 may
     be in the middle of the program text on the server. In some systems, it is managed by sending the pointer to the server stub and implementing special pointer-specific logic 
     in the server function.
   * A pointer can be followed by saving it in a register and then following it indirectly through the register (dereferenced). When this technique is used, a pointer is
     dereferenced by sending a message back to the client stub telling it to fetch and deliver the item pointed to (reads) or save a value at the address pointed to (writes). 
     While this method is effective, it is inefficient most of the time.
   * Only within the address space of the process in which it is used does a pointer have any meaning. If the second parameter is the address of the buffer on the client, which is
     1000, one cannot simply provide 1000 to the server and expect it to function. On the server, address 1000 can be in the middle of the program text
   * In C, for example, in passing arrays, a variable’s address is supplied. Handling pointer-based data structures, such as pointers, lists, trees, stacks, graphs, and so on.
       * **Call-by-object-reference**: Here RPC mechanism uses object invocation. The value that holds a variable is used to refer to an object.
       * **Call-by-move**: A parameter is passed by reference, much like in the call-by-object reference method, but the parameter object is relocated to the target node during 
         the call (callee). It is termed call-by-visit if it remains at the caller’s node. It allows the argument objects to be packaged in the same network packet as the 
         invocation message, which in turn reduces network traffic and message count.
