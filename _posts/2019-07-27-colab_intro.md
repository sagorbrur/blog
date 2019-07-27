---
title: A Gentle Introduction to Google Colaboratory
---


You are an enthusiastic learner on Machine Learning but you have no capability to purchase a big machine to train and test your model.

## Don't worry! 

Google Colab is a perfect solution for you. Google Colab(Colaboratory) is a free cloud service to encourage machine learning research.

Here is a simple introduction how you start google colaboratory. 

# STEPS

## Account

* Create a google account(Hope you all have a gmail)
* Log in to your gmail
* Goto [https://colab.research.google.com](https://colab.research.google.com) and sign in with your gmail account

## Opening a new Notebook

* Now you can create a jupyter Notebook with python 2 or 3 just clicking 'New Notebook'
* To run any cell click shift+enter

## Download anything from web and cloning git

* To Download anything from web just run the following command inside notebook

```!wget url```

You can download dataset from website with no time(12mbps or more google speed)

You can unzip anything just running the following command

```!unzip file.zip```  [Here file is your filename]

* To clone a git just run the following command

```!git clone git_url```

## Download google drive data from colab

For downloading your drive data from colab you have to run the following code from colab notebook. After running the code you will get a verification link from where you will get a code to paste in notebook. after finishing it will download the file in colab.

```py

#drive data download code
!pip install -U -q PyDrive
from pydrive.auth import GoogleAuth
from pydrive.drive import GoogleDrive
from google.colab import auth
from oauth2client.client import GoogleCredentials
auth.authenticate_user()
gauth = GoogleAuth()
gauth.credentials = GoogleCredentials.get_application_default()
drive = GoogleDrive(gauth)
downloaded = drive.CreateFile({'id':"file id"})   # replace the id with id of file you want to access
downloaded.GetContentFile('file_name.csv') #Replace the name with your file name

```

## Changing Working Directory

```
%cd Directory_Name

```

To check 

```
!pwd

```

Swtiching back to root folder:

```
!cd ..
```

## Installing libraries
Although google colab has all the dependencies library installed, you can install any library just running the command you run on bash

```!pip install library_name```

## Activating GPU
* You can activate GPU from ```Edit>Notebook Settings>Hardware Accelerator>GPU```

## Upload local file

* You can upload local file by clicking the upload button which exist in your left side inside Files
* Check and upload your local file

```NB: file will automatically deleted after you closing the browser```

## Run full project as python scripts
Suppose we have directory with files, data , config

```
----Contents

    ------train.py
    
    ------test.py
    
    ------data
    
          -----train.csv
          
          -----test.csv
          
    ------config
    
          ------config.config
          
    -------logs
```

Our config.config looks like

```
train_data = "data/train.csv"
test_data = "data/test.csv"
log_dir = "logs"
epoch = 10
mode = train

```

Our train command is 

```python train.py --config_file config/config.config```

and Test command is 

```python test.py --config-file config/config.config```

To train the project in colab write the commnad inside notebook

```!python train.py --config_file config/config.config```

It will train the model and save the checkpoint inside logs directory. From where you can download the checkpoint. 

To test the project in colab write the command inside notebook

```!python test.py --config-file config/config.config```

That's the easiest way to train model from project scripts. 


## Some Extra Points
* After training download the logs or trained checkpoint file. Because when you close the browser it will automatically delete all files. 
* The Ipython file will automatically saved inside your google drive. You can download the notebook from

```File>Download .ipython or Download .py```

* To save a code cell as python script

```
%%workfile myfile.py
class myclass(object):
    def __init__(self, a, b):
        self.a = a
        self.b = b
        
    def add_num(self):
        return self.a+self.b
        
```



