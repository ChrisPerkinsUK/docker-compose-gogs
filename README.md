# docker-compose-gogs
A docker-compose configuration for setting up Gogs source control repository management.

## What is Gogs

Gogs is a selfhosted Git Service. It is lightwieght and ideal for running on your local machine or over a local network. It does not support HTTPS but is effective and can serve as a part of a local component of a CICD system.

Official website:        https://gogs.io
Gogs Documentation:      https://gogs.io/docs
Gogs on Docker Hub       https://hub.docker.com/r/gogs/gogs/

## QUICK START COMMANDS

#### Start

docker-compose up -d

#### Stop

docker-compose down

All data an logs will remain in the ./data directory after shut down.

#### List Containers (whilst running)

docker containers ls

containers:
       docker-compose-gogs_gogs_1
       docker-compose-gogs_postgres_1

#### View Logs (whilst running)

docker logs container_name

usermod: no changes
Oct 20 10:46:13 syslogd started: BusyBox v1.28.4
2018/10/20 10:47:16 [TRACE] Custom path: /data/gogs
2018/10/20 10:47:16 [TRACE] Log path: /app/gogs/log
2018/10/20 10:47:16 [TRACE] Build Time: 2018-09-16 03:57:36 UTC
2018/10/20 10:47:16 [TRACE] Build Git Hash: 3a4c981e3167875a3b60d0cee00ee85272608439
2018/10/20 10:47:16 [TRACE] Log Mode: File (Trace)
2018/10/20 10:47:16 [ INFO] gogs.mydomain.me 0.11.66.0916

## How to use docker-compose-gogs

### Starting

#### 1

Open the (Terminal) comandline window in the docker-compose-gogs directory and type:

#### 2

docker-compose up -d

#### 3

Wait a few minutes while gogs creates ssh certificates instantiates git and configuration, data, and log directories.

#### 4

Open a browser and enter the ip address of your server followed by the port 10080

For example on your local machine the localhost or loopback addresses could be used like this:

http://localhost:10080

or

http://127.0.0.1:10080

To use a specific ip on the host machine uncomment the entry:

- 127.0.0.20:10080

under the ports section of the docker-compose file prior to starting, change the ip address 127.0.0.20 to your desired ip address and comment out the line:

- 10080:10080

by placing a hash in front of it. Otherwise remove the line entirely.

## Filling in the Form for the initial install page

The first time you start up Gogs you need to fill in a form to tell Gogs how you want it to be configured. The following notes should help demistify some of the less obvious parts of the form.

#### Database settings

This installation uses the official Postgres database image from docker hub.
https://hub.docker.com/_/postgres/

At the top of the form is a section for Databse settings. For this configuration enter the following details:

##### Database Type:
Database Type: PostgresSQL

##### Host:
Host: postgres:5432

This must match the name of the database service in the docker-compose.yml file and the internal port port of the Postgres container

##### User:
User: postgres

##### Password:
Password: admin

##### Database Name:
Database Name: postgres

##### SSL Mode:
SSL Mode: Disabled

#### Application General settings

##### Application Name:
Application Name: Your Application Name (What ever you Like)

##### Repository Root Path:
Where the repositories will be stored inside the container. This will be mapped to the Bind Mount and will be written to a local directory on the host machine. Best to leave it as it is unless you have a specific need to change it.

Repository Root Path: /data/git/gogs-repositories

You may wish to change this for the following reasons:

1) To separate the bind mount out into separate and distinct directories for 'data', 'config' and 'logs'. I will be adding this in a later version.

2) To use volumes instead of bind mounts or a combination of both to separate concerns as in usecase 1)

##### Run User: Leave as git
Run User: git

##### Domain: Enter your domain name here.
Domain: mydomain.me

##### SSH Port: Leave at port 22
SSH Port: 22

##### Use Bulitin SSH Server: Not compatible with the current Docker container
Use Bulitin SSH Server: Do not tick

##### HTTP Port: Leave the port as the internal port of the container
HTTP Port: 3000

##### Application URL: (Same as Domain:) External domain : Port on the host machine mapped to the container.
Application URL: http://mydomain.me:10080

##### Log Path:
Leave as is unless you want to use separate bind mounts or volumes for 'data', 'config' and 'logs'. See Repository Root Path:

##### Enable Console Mode: Leave disabled

Log Path: /app/gogs/log

#### Email Service Settings
Untested so far just leave blank unless you specifically want to use with an email server.

#### Server and Other Services Settings
Select Options as desired

#### Admin Account Settings

Make sure you set up an admin user dispite the comment that informs that this is not needed. As this instance of Gogs is inside a container you will need to create the admin user to access it.


##### Enjoy! Chris Perkins
