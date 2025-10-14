### compresion and costing 
- when we are storing the content of documents we can do few things inorder to save the cost
- to save the costs we can think of saving the storage
- while saving the content of the data we compress and then store it there are many compression algorithm (in this case we will go with lossless algorithm) like huffman compression alg.
- when storing compressed data this will affect the get documents api call, computation will go high as when document is fetched we also need to decompress it and then this document will be sent back to user
- so to improve this we will compress the versioning documents and not the one which is latest document this document will remain as is
- can this be extended further yes , lets say there is an update to document "ABC" add YZ and remove BC the resultant is AYZ
- instead of immediately saving it in document , we will take the operation add YZ and remove BC, now for every get operations
- we take the current document in db and will do the operations and return the final result , now although we have increased the computation for get api , but we have saved a lot on write operations , so write load is moved to read , this will be eentually consitent with db 
