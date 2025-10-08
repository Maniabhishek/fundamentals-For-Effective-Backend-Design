- To design it we can follow the approach of creating data required to be stored in each services (i.e., ER diagrams) and then figuring out services how each of the services will communicate and what will they serve , and finally we will think how user will connect to our services
- The other approach is doing the same stuff but from opposite way , first think from the user perspectives about the application what features are requirement , think about the requirement, and then fit these requirement to the services think aobut the service what services will they be offering , and finally you can think about the data that need to be stored

### Requirements of Tinder Architecture 
1. Store Profiles
2. Recommend matches 
3. Note matches
4. direct messaging

### Can we think of few question that is coming to our mind for each of the requirements
1. Store Profiles (images per users -> lets take 5 images per user)
2. Recommend matches (No. of active users)
3. Note matches (lets say 0.1% of total active users that means 0.1/100 * (total active users))
