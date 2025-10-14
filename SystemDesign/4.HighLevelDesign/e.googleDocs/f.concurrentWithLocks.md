### points we have covered till now 
- storing the documents in db (content in noSQL)
- version history
- compressions + file storage
- Log of operations (fast writes, serves read)

### now we will discuss the concurrent writes
<img width="428" height="303" alt="image" src="https://github.com/user-attachments/assets/12807874-c6e6-4b31-b7c7-c213882384fb" />

- as in the image we can see , user A wants to write (add D) to document and user B also wants to write (remove C) to document concurrently 
- there are couple of ways we can do it without any conflict
- first is pessimistic lock or exclusive lock , lets say A started writing it will take a lock and add D , in the meanwhile if B user comes and tries to edit , it will fail as it is in lock mode , so user B can only write if there is no lock once lock is removed document is changed to ABCD and now user B comes edits the document to ABC, this lock is also not so efficient and we are not even doing concurrent writes , this lock is actually removing the idea of concurrency 
- another one is optimistic writes where user A take a lock on document to write , then user B comes to write at the same memory location, it will allow to write or edit the document , now once both of them have completed only one of them is going to win , the one which failed will be retired or completely fail, in this case there is lot of wastful processing ,  to take the copy of document from the optimistic lock is not a greate idea
- so lock is not something we will have to acieve it
- instead we need some better algorithm to have it
- what will have we have a document with ABC where user A with operation add D
- and user B with operation del C what we are going to take the copy of current document ABC - > and 

<img width="723" height="440" alt="image" src="https://github.com/user-attachments/assets/644418b2-8406-43e0-a501-d4d98c2d3129" />

- we are not exactly taking the copies this is just conceptual
- two copies have to eventually merge
- while merging we can see it is quiet similar to log operation we saw in compression and costing
- what will be the ordering of the operations, in above case doing any order might not affect but these operations can be very complex
- you need a reconcile algorithm here , one of the famous reconcile alg. used by goodle docs as well, it is operational transform, another one is CRDT

<img width="323" height="288" alt="image" src="https://github.com/user-attachments/assets/1b777579-04da-43ca-8893-fbc68c8d05d8" />

- as above you can see to reconcile we will do opposing operation to both the final outputs , but again this can get very very complex , so we will be using operation transform alg. which is being used by google docs
