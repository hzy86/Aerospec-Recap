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

### TCP/IP protocol
- as a client - connect to remote IP address via specified port
- as a server - configure local IP adress and port and allow remote client to connect in
- header contains
 - src and remote IP
 - packet size and data
 - etc
 
### MQTT protocol
[src](https://www.hivemq.com/blog/mqtt-essentials-part2-publish-subscribe/)
- pub/sub model, allow 
 - space decoupling: subscribers and publishers do not need to know each other
 - time decoupiling: subscribers and publishers do not need to be online at the same time
 - async processing
- different from message queue due to
 - do not need a message in queue to be consumed before the next one can
 - more than 1 client can consume a message
 - creating topics is flexible while queue must be existing
- connection
 - broker closes down after timeout or it receives a malformed connection packet
 - a good connection packet contains
  - clientID - broker uses this to identify a client and store its state. If empty, cleansession must be true for the broker to accept the connection. The broker would establish the connection without storing the states of the client.
  - username&passord - plain text if unencrypted and unhashed (by implementation or TLS certificate).
  - cleansession - if false, the session is persistent, meaning that the broker will store the subscriptions and missed messages for the client with QoS 1 or 2.
  - keep alive
  - topic, QoS, message, retain ???
 - upon connection established, the broker would send a CONNACK flag that contains
  - session present flag - allow users to know

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
* Deployment flow
  * have a ```.gitignore``` ready.
  * ```pip freeze > requirements.txt```
  * settings.py for static url, media url, hosts, database, etc. Have an empty ```static``` folder if needed.
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

## Git
```git revert <commit>``` to undo this commit and create a new commit for this, i.e. revert to its parent commit, avoiding detached head.

``` git reset <commit>``` to undo this commit by resetting both the HEAD and the branch ref.
- ```--hard``` to reset all staging index and working directory changes to match the state of the target commit
- ```--soft``` to save staging index and working directory changes, only resetting the commit history
- ```--mixed``` to save working directory changes and reset the commit history, not resetting the staging index
- makes commits after resetting diverge from the original branch
- ```git reset .``` to unstage files

```git checkout <commit>``` to change files previously without affecting current branch and head. Would be in a DETACHED HEAD state.
- ```git checkout -- file``` to revert changes to a file to match its last index. If index does not exist, revert to match HEAD.

```git stash``` to save local index and then clean them up. Stashes can be restored by ```git stash apply stash@{#}```, which can be seen from ```git stash list```
- ```-u``` to save untracked files as well, ```-a``` to save ignored files in addition.

```git push/pull origin <branch>``` to push/pull to/from a remote branch that is on remote *origin*.
- ```git pull --rebase origin <branch>``` to merge and move current commit to the tip of branch history
- if current commit is a history of another commit, git will fast-forward instead of creating merge conflicts

```git log --graph --oneline``` to view commit history and figure out parents

```git branch --set-upstream``` set the default remote branch for this local branch. ```git checkout <branch>``` to change the current directory to the branch.

```git clean``` to clean untracked files
- ```-n``` to dry run, ```-d``` to include directories, ```-f``` to force

```git merge --no-ff <branch>```, ```git rebase```, etc

**Best Practice**
- never reset a published commit because that would mess up others' commit history, only reset a local commit
- use ```git pull --rebase```
- ```git stash``` followed by ```git checkout -- file``` to revert local changes

[Solution for Git not generating merge conflicts](https://stackoverflow.com/questions/40097125/git-shows-no-merge-conflicts-when-it-should)

## Soft skills
* Learning from source codes, sample codes, documentations, ...
* Unit debugging
