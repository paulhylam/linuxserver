# linuxserver

# Instructions for grader

ssh grader@18.196.33.181 -i [private key] -p 2200

passcode: passw0rd

run 'sudo python rest-app/project.py' on the ubuntu server
try in browser http://18.196.33.181/ to access the catalogapp

Software installed and third-party resource used:
finger
python3
python3-pip
flask
SQlAlchemy
OAuth-client2.0
Google API

# Setting up the server and new users

1. Login to lightsail and add a new server.
2. Login with the standard user ubuntu
3. Install some necessary packages, e.g. sudo apt-get install finger
4. Manage users by e.g. sudo adduser -or - sudo deluser
5. Once done check the new user by logging in ssh grader@localhost -p 22

# grant sudo right to new users

1. in the default user - sudo ls /etc/sudoers.d
2. sudo cp /etc/sudoers.d/90-cloud-init-users /etc/sudoers.d/grader
3. update the name from 'ubuntu' to 'new_username'

# setting up ssh via 2200

generate the keys in local machine

ssh-keygen /directory/
/Users/Paul/.ssh/linuxCourse
ls /Users/Paul/.ssh/
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDKNjI+okfZrzX04jgEiUPSX1iqIduG5MTxNE7jQe6ab84ivG/kSPHjWqVo1s0/S6Id5FAeJmbjax0CfMzdPXf3/s5Uqc/TdrmsOu+5MjvaE+z0llRNg7YsvppcugekBYiTM3M0lXqKu23p5JrbG9iATS4D892/KWqTj0gOll00NyfQaJbJDmGo4Bf1Cn3sfQPY3rhX9U0eVn/X3XnnMvz4xXuz8mwkvnXid4cSEVIbcydpQCIVmhxpg1hsd3RxpCax+pdHOEk20+fVKyVJtVrzcN1os38miXgB+uB0Rb2wlmLS2ojfq3H1DM9o5YWQJtlLGoy9LhdqIzCrzahkGjmj paul@Pauls-MBP

copy the private key

get back to the server login as the new user:

- mkdir .ssh
- touch .ssh/authorized_keys
- paste the key in the file
- chmod 700 .ssh
- chmod 644 .ssh/authorized_keys

# Update everything

sudo apt-get update
sudo apt-get upgrade

# Setup ufw

sudo ufw default allow outgoing
sudo ufw default deny incoming
sudo ufw allow ssh
sudo ufw allow 2222/tcp
sudo ufw allow www
sudo ufw allow 2200/tcp
sudo ufw enable

# update all the webserver items, python by pip (python3 by pip3)

sudo apt-get install libapache2-mod-wsgi-py3
sudo apt-get install postgresql
sudo apt-get install git
sudo apt-get install python3-dev python3-pip
sudo pip3 SQLAlchemy
sudo pip3 flask
sudo pip3 install -t lib google-api-python-client
sudo pip3 install --upgrade oauth2client

# git clone the webserver

rm -rf rest-app
git clone https://github.com/paulhylam/rest-app
cd rest-app
sudo python rest-app/project.py




