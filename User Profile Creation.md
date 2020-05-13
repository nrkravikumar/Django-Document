## User Profile Creation by using OneToOneField
  - Creation of Model
  - Creation of Form
  - Creation of Function
  - Creation of URL
  - Creation of .html
---
### Creation of Model:
  - After logging into **User Welcome page** we need to update some more fields that is not existing in the User model(i.e., when user is registering into our site) so for that purpose we are creating another model to update user profile when user is authenticated to login.
  - In previous topics we are aware of how to create a model and how to access it but for user logging we didn't created any model to register because we are migrating the default admin models to database.
  - So first step is to open the models.py in our app and then we need to import the default User model from admin so we are implementing some code to access the models <br/>
    #### ```models.py```
    ``` python
    from django.db import models
    from django.contrib.auth.models import User
    ```
   - By Default the models is accessed when migrate is done by user here ```django.db``` defines a models that is accessing from ```.db``` so we are not importing that line. Then we need to access default admin model by implementing ```django.contrib.auth.models``` in that we are accessing only the models class.
  
