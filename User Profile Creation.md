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
    #### ```models.py```
    ``` python
    from django.db import models
    from django.contrib.auth.models import User
    
    class Profile_details(models.Model):
          age = models.IntegerField()
          phone = models.CharField(max_length = 10)
          salary = models.FloatField(max_length = 10)
          user = models.OneToOneField(User,on_delete=models.CASCADE)
    ```
   - We are aware of types in **ORM** like IntegerField,CharField etc., for age we are not considering any max_length but we can restrict for max_length = 2 so for user requirement it is to be changes and in phone we are not defining IntegerField type because for that we need to access only integers with some limit upto 10 digits so to print the phone number in admin page in string format so for that purpose we are defining CharField for phone. salary consists with some decimal values so we are implementing it in FloatField. Last Field we are implementing in our model is user so here we are assigning OneToOneField so here the relation is single user access for single time insertion to his/her profile. Suppose user has to delete from our site for that we need to remove all record values so here we are using on_delete = models.CASCADE this can deletes the linking to particular user field values are to be deleted from the table.
   
   > **OneToOneField**: single user has to insert his/her details for single time insertion in a table

   > **on_delete=models.CASCADE**: Here we are removing entire record of a particular user from a table that should not exist in a table after removing a user. Suppose we are not using on_delete then the record in only User table is to be removed remaining table consisting of particular user values are exists so for that rectification we are using on_delete for removing not existing users values in tables.
   
   #### ```models.py screenshot```
   <img src="models.JPG" alt="manage.py" height="280px" width="100%">
   
   - After implementing model fields in models.py we need to do ```makemigrations``` because the fields we are creating for a particular table that can be viewed in the migrations folder with 0001.py files or how many times the migrations are done that can be increased with some numbering in it. If we need to check the fields with types that can be viewed in it.
   - Making migrations it can't effects database for creating a table with fields. So we need to do ```migrate``` here the table and fields are to be created in database that is implemented in models by user.
   - Here we are using model as **Profile_details** as tablename but the table name can be created as **database_modelclassname** it can be created like databasename with modelclassname.
     #### ```Command Prompt```
     ``` python
     python manage.py makemigrations 
     python manage.py migrate
     ```
     #### ```Screenshot of migrations and migrate```
     <img src="modelcreation.JPG" alt="migration command" height="280px" width="100%">
     <img src="migrate.JPG" alt="migrate command" height="280px" width="100%">
     
   - After making migrations and migrate we can observe the tablenames with fields in **phpmyadmin** as shown below 
     #### ```Screenshot of model class with field names```
     <img src="modelinxampp.JPG" alt="model creation in xampp" height="280px" width="100%">
   - In above figure it shows tablenames and fields but in field structure we are not creating id with type. while creating a model by default it creates **id** for all the tables here we are linking the first table to this specified table by using OneToOneField.
   - The last field we are assuming is user in userdefined model but in mysql the filed is created as **user_id**. 'underscroll id' will attaches to every oneToOneField structure in models. 
 
---
### Creation of Form:
   - While model creation is done in mysql then we are proceeding for ```form creation``` whatever the fields that we are going to display and to enter the values to the tables in particular field.
   - We are aware of creating a form in our app that is created previously so in that we are going to create a new class (i.e., as userdefined names here we are creating the form name as **ProfileForm**) for our newly created model class.
   - Before proceeding to create a class for userdefined form first we need to import the created model class to here for importing the model from model to form we are using ```from django.models import ModelForm``` so here whatever the model we are giving for that we are creating a form so we need to import the ```ModelForm```
   - After importing we need to import the model class also for which model we are going to create a form. so for accessing that model we are importing as ```from userapp.models import modelname``` here the userapp is your app name whatever we had created previously and the model class name is just created in the ```models.py``` file.
   - Finally the importing in forms.py looks like below.
     #### ```forms.py``` 
     ``` python
     from django.models import ModelForm
     from userprofile.models import Profile_details
     ```
   - So we need to create a userform class for inputting the specified values to models.
     #### ```forms.py```
     ``` python
     class ProfileForm(ModelForm):
         class Meta:
             model = Profile_details
             fields = ['age','phone','salary']
     ```
   - In above code implementation we are not using **id** and **user_id** because it ishould be automatically set to their default states such as **id** is primary key in the table and **user_id** is foreign key that should be inserted automatically when specific user is logged into their profile. 
   - We are not using **__ all __** because we should not enter the id and user_id field values if we are assiging as **__ all __** in fields we need to select the user when the form is displaying. so it creates a duplicates for all the users so we can't specify user details when searching in database tables.
   - Finally the forms.py looks like below shown figure
     #### ```forms.py```
      
    
  
