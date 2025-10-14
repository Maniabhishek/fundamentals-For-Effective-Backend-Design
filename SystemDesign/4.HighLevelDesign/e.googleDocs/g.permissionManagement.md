- permission manager, we will have one seperate permission manager which will be handling the permissions of user whether the user is allowed to edit or not
- so user requesting to edit , comes to gateway , before anything happens , it will go to the permission manager ,
- inside permission manager will have the data shown below

| id   |  permissions                         |
|------|--------------------------------------|
| 1  | json object {123: owner, 124: read}    | 


<img width="1313" height="791" alt="image" src="https://github.com/user-attachments/assets/6bfe89ba-feb7-4354-9dad-1b1d187b7a67" />

