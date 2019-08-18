## Device firmware

**Sensor Driver in C/C++**

Used I2C protocol or digital/analog pins to transmit/receive data from sensors. Used C++ classes, objects, and member functions to group readings from a sensor.

**LTE Modem Driver in C/C++**

Used UART protocol to communicate with the module and used AT commands to configure a range of supported functions. Worked with provided technical documents to implement functions that are not provided in its library.

**General C/C++ Programming**

Strings handling - ```dtostr()```, ```sprintf```, etc. Null-terminator, char buffer, and Arduino String type. Specified buffer length in TCP/IP transportation.

## IoT Networking
- setup cellular connection from the LTE modem
- authenticated with Cloud platform using sim key
- configured TCP server and client, designated data segment length, and transported data programmatically
- setup software webhook receiver API and configure webhook route from Hologram Cloud Platform to enable real-time data processing

## Full-stack cloud software
### Django MTV Basics
* Models
  * models - queries, migrations, model fields
  * usage of makemigrations and migrate, involving ```--fake```, ```--fake-initial```
* Templates
  * serve data to the template - ```{{ data|safe }}``` syntax 
  * template inheritances - ```{% extends base.html %}```
  * template tags and decorators
* Views
  * HTTPResponse to make a REST API
  * render
  * using models
* Management
  * requirements.txt
  * settings.py for static url, media url, hosts, database, etc
  * deploy to Heroku - Gunicorn for running server, Whitenoise for serving static files, psycopg2 for database engine
### Django REST Framework
**ViewSet**

Compared to view and generic views, viewset reduces codes by integrating multiple APIView classes into one
  
  viewset sub classes
  - filters
    - reduce the need of regex url matching or ```self.request.data``` to access query params
    - customized filter class to alias lookup expressions
      - alias can be the same as field_name ??? (seems to work for now, need further proof)
    - ordering
  - pagination - support limit and offset
  - serializer
  
**Router**
  - works with viewset
  - auto-generate a range of urls that bind to basic CRUD functions like list, retrieve, update, etc
  
**Authentication**
- CORS
  - use django-cors-headers packages
- token

### NodeJS
### AWS
* CLI and CLI scripts
* Lambda, API Gateway, S3, RDS (main responsibility)
* Elastric Beanstalk, CloudWatch

**Backend General Knowledge**
* database connection - schema design and db programmatically query
* build a REST API
* route frontend pages
* communicate with other services via REST API
  
**Frontend General Knowledge**
* JavaScript
* Google API
* responsive UI design

## Soft skills
* Learning from source codes, sample codes, documentations, ...
* Unit debugging
