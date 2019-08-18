# Overview
This is a progress diary for recapping what was a major progress but replaced by something better later. 

Code repo AerosepcUsedCodes is private to protect our products in production. Please send me a message if you would like to see it via [Linkedin](https://www.linkedin.com/in/ziyi-huang86/) or Email hzy066@gmail.com.

# Current versions
## Django API Backend
### Django REST Framework
**ViewSet**

Compared to view and generic views, viewset reduces codes by integrating multiple APIView classes into one
  
  *viewset sub classes*
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

## LambdaPackages
### [World Pollution Data Lambda Requests and DB Insertion](https://github.com/hzy86/AerospecUsedCodes/tree/master/LambdaPackages/worldPollutionLambda)
*8-7-19*

Make GET requests to WAQI API and insert them into the database. Converted time strings into UTC.

Updated exceptions handling so that:
- end execution if any field is not formatted correctly, esepcially geolocation, station id, and time.
- print error station id and corresponding error messages.
- print success message and station count


### [Device Data Webhook with Lambda and API Gateway REST API](https://github.com/hzy86/AerospecUsedCodes/tree/master/LambdaPackages/deviceWebhookLambda)
*7-13, 7-27, 8-7-19*

8-8 added hour round down and re-formatted multi-line strings

8-7 modified round down function to accept the resolution as a parameter and changed device_name to integer field.

7-27-19 updated the Lambda codes to round time_created to the nearest 5 min and and insert into the db table new column ```time_label```. Also inserted device name and inserted into new column ```device_name```.

## Firmware - [TCP/IP Send & Receive](https://github.com/hzy86/AerospecUsedCodes/tree/master/TCP-Full-Duplex-8-10)
*8-10, 8-11, 8-12-19*

Supported SIM module control by messaging commands from the Hologram Dashboard.

Setup a TCP server on the device that listens to a port and polls data constantly.

8-12 added server responses after receiving a command. Separated LTE codes to another file for better readabilitiy. Removed noise sensor stuff.

8-11 updated polling logic and added software commands to reset module, enable/disable data sending, and specifying upload frequency.



# Software

## Dweetio, Lambda, Cloudwatch, S3 
*7-13-19* [Outdated](https://github.com/hzy86/AerospecUsedCodes/tree/master/Dweetio-Lambda-Cloudwatch-S3)

Use HTTP GET and params to post data to Dweetio from the LTE shield. Then use Lambda to get data from Dweetio and insert into the database. Schedule Lambda trigger using Cloudwatch.

To deploy, install all packages specified in ```requirements.txt```, and then place them in the same folder as aerospeclambdards.py file that defined a ```handler(event, context)``` function. CTRL+A to select all, right click on aerospeclambdards.py to zip, run ```aws CLI command #1``` in its parent folder to upload to S3, and finally run ```aws CLI command #2``` to update Lambda codes.

* **Note**
  - packages and the .py file have to be at the same level in the deployment .zip, otherwise Lambda could not find them
  - be sure to modify the Handler in Function codes of of the Lambda setup to match the function name, otherwise Lambda coud not find the main function

* **Files Breakdown**
  - requirements.txt

    Requried packages. Psycopg2 needs to be built. Someone had do it for us. Follow his instructions in this github [psycopg2 to Lambda](https://github.com/jkehler/awslambda-psycopg2).
  
  - AWSCLIcommands-Lambda.txt

    Two AWS CLI command to script uploading package to S3 and linking it to Lambda.
  
  - aerospeclambdards.py

    The main code that use requests library and Dweetio API to get data and use psycopg2 to query the database.
  
  
# Firmware

## Plantower, VMA309, SIM7000, Hologram Cloud, TCP/IP, Average data
*7-26, 8-7-19* [Outdated](https://github.com/hzy86/AerospecUsedCodes/tree/master/Hologram-TCP-Sensor-Average)

8-7-19 read and sent battery level instead of noise.

Sample data every xxx seconds, upload the average of the samples every 5 mins. 

Solved a fun problem - consecutive ```dtostr(data, length, precision, buffer)``` might be using consecutive memory for buffers! We observed that if the buffer size of the last called ```dtostr``` equals to ```length``` (not enough space for the terminator char), the terminator would be stored in index 0 of the buffer used by the 2nd last ```dtostr```. As a result, Serial.print(the 2nd last buffer) would print nothing.

## Twilio, T-mobile Narrowband SIM
*7-17-19* [Currently exploring](https://github.com/hzy86/AerospecUsedCodes/tree/master/twilio-prototype)

Try to use Twilio for our product for its compactness.

### Plantower, VMA309, SIM7000, Hologram Cloud, TCP protocol
*7-13,7-25-19*[Outdated](https://github.com/hzy86/AerospecUsedCodes/tree/master/Hologram-Plantower-Noise-TCP)

Also gather GPS info via SIM7000. 7-25 fix corrected GPS read.

## SPS30 Particle Sensor
*6-18-19* [Outdated](https://github.com/hzy86/AerospecUsedCodes/tree/master/sps30-LTE)

Gather particle information using sps30 sensor and upload it to Dweetio using SIM7000 LTE module. This was only used as a small test.


