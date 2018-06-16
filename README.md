# Solid-Python-Development-Web-Server  
###Logistic Regression Service, Web Server and Application  
  
## Technology Used  
##### Python 
##### Spark
##### MongoDB  
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
   
>>> from pymongo import MongoClient  
>>> MONGODB_HOST = 'localhost'  
>>> MONGODB_PORT = 27017  
>>> DBS_NAME = 'datasets'  
>>> COLLECTION_NAME = 'bank'  
>>> connection = MongoClient(MONGODB_HOST, MONGODB_PORT)  
>>> collection = connection[DBS_NAME][COLLECTION_NAME]  
>>> customers = collection.find(projection=FIELDS)  
  
  
### Redis key-value store to log the intermediate state of long-running tasks, and also to store the serialized output from training models in Spark  
  
    
##### Python interface for Redis in the redis-py package   
   
>>> import redis  
>>> r = redis.StrictRedis(host='localhost', port=6379, db=1)  
>>> r.get(key)  
>>> r.set(key,value)  

  
  
### The web server  
  
  the web server receives requests and forwards them to the web application  
    
     
>>>if __name__ == "__main__":  
       modelparameters = json.loads(open(sys.argv[1]).readline())  
       service = modelservice(modelparameters)  
       run_server(service)  
  
tree.graft command to attach the application (the model service itself) so that the object is called by the CherryPy modelserver whenever it receives an HTTP request.  
      
def run_server(app):  
    import paste  
    from paste.translogger import TransLogger # TransLogger class from the paste library passes requests between server & application  
    app_ = TransLogger(app)  
    cherrypy.tree.graft(app_, '/')  
    cherrypy.config.update({  
        'engine.autoreload.on': True,  
        'log.screen': True, #Log.screen directs the output of error and access message to the stdout  
        'server.socket_port': 5000,  
        'server.socket_host': '0.0.0.0'  
    })  
    cherrypy.engine.start()  
    cherrypy.engine.block()  
    
### Start the server in command line  
  
python modelserver.py parameters.json  
