# Solid-Python-Development-Web-Server  
###Logistic Regression Service, Web Server and Application  
  
## Technology Used  
#### Python  
#### MongoDB  
#### Redis  
#### CherryPy  
#### Celery  
#### cURL  
#### Excel  
  
  
### Initialize database MongoDB  
  
$ mongodb  
$ mongoimport -d datasets -c bank --type csv --file bank-full.csv —headerline  
$ mongo  
$ use datasets  
$ show collections  
  
    
## Interact with MongoDB through Python using the pymongo client  
   
from pymongo import MongoClient  
>>> MONGODB_HOST = 'localhost'  
>>> MONGODB_PORT = 27017  
>>> DBS_NAME = 'datasets'  
>>> COLLECTION_NAME = 'bank'  
>>> connection = MongoClient(MONGODB_HOST, MONGODB_PORT)  
>>> collection = connection[DBS_NAME][COLLECTION_NAME]  
>>> customers = collection.find(projection=FIELDS)  
  
  
