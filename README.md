## Overview
This is a progress diary for recapping what was a major progress but replaced by something better later. Code repo AerosepcUsedCodes is private for now.

## Software

### Hologram Cloud, Lambda, API Gateway, S3
*7-13-19 Current Version [AerospecUsedCodes/Hologram-Lambda-APIGateway-S3(https://github.com/hzy86/AerospecUsedCodes/tree/master/Hologram-Lambda-APIGateway-S3*

### Dweetio, Lambda, Cloudwatch, S3 
*7-13-19 Ditched [AerospecUsedCodes/Dweet-Lambda-Cloudwatch-S3](https://github.com/hzy86/AerospecUsedCodes/tree/master/Dweetio-Lambda-Cloudwatch-S3)*

Use HTTP GET and params to post data to Dweetio from the LTE shield. Then use Lambda to get data from Dweetio and insert into the database. Schedule Lambda trigger using Cloudwatch.

To deploy, install all packages specified in ```requirements.txt```, and then place them in the same folder as aerospeclambdards.py file that defined a ```handler(event, context)``` function. CTRL+A to select all, right click on aerospeclambdards.py to zip, run ```aws CLI command #1``` in its parent folder to upload to S3, and finally run ```aws CLI command #2``` to update Lambda codes.

#### Note
- packages and the .py file have to be at the same level in the deployment .zip, otherwise Lambda could not find them
- be sure to modify the Handler in Function codes of of the Lambda setup to match the function name, otherwise Lambda coud not find the main function

#### Files Breakdown
*[AerospecUsedCodes/Dweet-Lambda-Cloudwatch-S3](https://github.com/hzy86/AerospecUsedCodes/tree/master/Dweetio-Lambda-Cloudwatch-S3)* (private repo for protection)
- requirements.txt

  Requried packages. Psycopg2 needs to be built. Someone had do it for us. Follow his instructions in this github [psycopg2 to Lambda](https://github.com/jkehler/awslambda-psycopg2).
  
- AWSCLIcommands-Lambda.txt

  Two AWS CLI command to script uploading package to S3 and linking it to Lambda.
  
- aerospeclambdards.py

  The main code that use requests library and Dweetio API to get data and use psycopg2 to query the database.
  
  
## Firmware
### SPS30 Particle Sensor
*6-18-19 Ditched (https://github.com/hzy86/AerospecUsedCodes/tree/master/sps30-LTE)*

Gather particle information using sps30 sensor and upload it to Dweetio using SIM7000 LTE module. This was only used as a small test.
