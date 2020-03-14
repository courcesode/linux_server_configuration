# Project Linux Server Configuration

The Project demonstrates how to set up and configure a linux based web server serving a flask application in a production environment. 


## Performed Configuration steps 

After setting up a lightsail server instance with a barebone ubuntu server installation, the following steps were performed: 

1. Through the webinterface, the aws firewall settings were modified to allow incomming connections on port 22, 80 and 123/udp.

2. After logging in to the server through ssh, the ssh port was changed. this was done by editing the sshd_config file located in /etc/ssh. The Port was changed from its default value (22) to 2200. 

3. the ssh port in the aws firewall settings was changed. 

4. ufw was configured to allow any outgoing and deny incoming connections except for 2200/tcp, 80/tcp and 123/udp. 

5. apache webserver and mod_wsgi was installed from repositories.  

6. a small wsgi "hello world" for testing purposes was applied. the wsgi file was placed outside of apache's DocumentRoot folder to prevent the possibility of code being downloaded or exposed. The root directory of the webserver was mapped to the wsgi file, this was done by editing the /etc/apache2/sites-available/000-default.conf file, using the WSGIScriptAlias directive. The directory directive was used to give apache access to the wsgi file. After visiting the uri of the hello world example, everything was confirmed to be working thus far. 

7. pip was installed from ubuntu repositories. 

8. the required python libraries for the item_catalog project to run were installed using pip. This includes flask, responses, sqlalchemy and oauth2client.

9. the item catalog project was cloned from my github repository, changes were made to the wsgi file to import the flask app instance and changes were made to apaches configuration files accordingly. 

10. when visiting the site, the server responded with a http 500 error. after reviewing the apache log files and consultation of the wsgi documentation, changes were made to the project accordingly. this includes (but is not limited to) changing relative to absolute filepaths and changing the ownership of files and the sqlitedatabase to the www-data user that runs the webserver on ubuntu. 

11. the final step to make the app working was to register the dns of the server with google to make it recognize the app and make oauth working.

12. the "grader" user was added to the system. the directive to give the grader user sudo was placed into the /etc/sudoers.d/ folder (see 90-cloud-init-users file) 

13. ssh keys were generated and the public key was placed into the .ssh directory inside the home directory of the grader user. 


## Project URL 

visit http://18.191.169.56.xip.io/ to browse the deployed app. 


## SSH Access data

To access the server, point your ssh client to ***ec2-18-191-169-56.us-east-2.compute.amazonaws.com*** on **port *2200***. The ssh key for the grader user will be provided with the submission in the "Notes for Reviewer" section. 
