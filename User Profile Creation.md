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
  - By Default the models is accessed when migrate is done by user here ```django.db``` defines a models that is accessing from ```.db``` so we are not importing that line. Then we need to access default admin model by implementing ```django.contrib.auth.models``` in that we are accessing only the models class(i.e., User).
  - Next step is to implement whatever the fields we need to create for a user when he/she is logged in. So here we are creating some more fields that are not existing in ```User``` model class with another class name(i.e., userdefined classnames). We are implementing the class name as **Profile_details** with age,phone,salary,user etc., fields names in it.
  - Profile_details model class consisting of three fields i.e., 
    - age with IntegerField 
    - phone with CharField consisting of max_length = 10
    - salary with FloatField consisting with max_length = 10
    - user with OneToOneField consisting of User model class involving on_delete=models.CASCADE
  - Finally we created a model class with some fields as shown below
    ``` python
    from django.db import models
    from django.contrib.auth.models import User
    
    class Profile_details(models.Model):
          age = models.IntegerField()
          phone = models.CharField(max_length = 10)
          salary = models.FloatField(max_length = 10)
          user = models.OneToOneField(User,on_delete=models.CASCADE)
    ```
   - We are aware of types in **ORM** like IntegerField,CharField etc., for age we are not considering any max_length but we can restrict for max_length = 2 so for user requirement it is to be changes and in phone we are not defining IntegerField type because for that we need to access only integers with some limit upto 10 digits so to print the phone number in admin page in string format so for that purpose we are defining CharField for phone. salary consists with some decimal values so we are implementing it in FloatField. Last Field we are implementing in our model is user so here we are assigning OneToOneField the purpose is single user should update his/her fields in one time so here the relation is single user access for single time insertion to his/her profile. Suppose user has to delete from our site for that we need to remove all record values so here we are using on_delete = models.CASCADE this can deletes the linking to particular user field values are to be deleted from the table.
   > **OneToOneField**: single user has to insert his/her details for single time insertion in a table
   > **on_delete=models.CASACDE**: Here we are removing entire record of a particular user from a table that should not exist in a table after removing a user 
    
  
