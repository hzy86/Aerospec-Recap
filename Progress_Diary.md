## Dweetio, Lambda, Cloudwatch, S3 
*7-13-19 Ditched*

Use HTTP GET and params to post data to Dweetio from the LTE shield. Then use Lambda to get data from Dweetio and insert into the database. Schedule Lambda trigger using Cloudwatch.

Lambda deployment package included all required packages and a .py file that defined a ```handler(event, context)``` function. The package was uploaded to S3 and linked to Lambda. Two aws CLI commands were written for copy-pasta to speed up the process.

Note
- packages and the .py file have to be at the same level in the deployment .zip, otherwise Lambda could not find them
- be sure to modify the Handler in Function codes of of the Lambda setup to match the function name, otherwise Lambda coud not find the main function

Codes - Repo AerospecUsedCodes/Dweet-Lambda-Cloudwatch-S3
- LambdaPacakge37
  Deployed Lambda codes. To use them, CTRL+A to select all, right click on aerospeclambdards.py to zip them, run aws CLI command #1 in its parent folder to upload to S3, and finally run aws CLI command #2 to update Lambda codes.
- AWSCLIcommands-Lambda.txt
  Two AWS CLI command to script uploading package to S3 and linking it to Lambda.
