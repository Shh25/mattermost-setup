## Ansible-Mattermost-Setup

## Clone repository
git clone git_repository_link

## Prerequisites
1. Install VirtualBox - version 5.2.* (Please install this version for baker to run smoothly. Vagrant can be used instead but extra setup and steps will be required to setup successfully)
2. Install Vagrant
3. Install Baker ([Baker website](https://docs.getbaker.io/installation/)) - latest stable version


## Installation and Instructions
1. Clone project from git repository
2. Create public and private key in ansible-srv directory from CLI using the command:
```
cd ansible-srv
ssh-keygen -t rsa -b 4096 -C "web-srv" -f web-srv
```


## Starting Web Server
1. Go into directory web-srv
```
cd web-srv
```
2. Create VM using baker (called from baker.yml).This will also save your public key in directory ~/.ssh/public_key which we need to add in authorized_keys once we are logged into the VM.
```
baker bake
```
3. Start VM using baker. Use command:
```
baker ssh
```
4. Set public key: (append key from public_key to authorized_keys)
```
cat ~/.ssh/public_key >> ~/.ssh/authorized_keys
```

## Starting Ansible Server
1. Go into directory ansible-srv
```
cd ansible-srv
```
2. Create VM using baker (called from baker.yml). This will also install ansible in the server directly and save your private key in directory ~/.ssh/web-srv which we need to add in in order to access the web server (Please do not share this key with anybody).
```
baker bake
```
3. Start VM using baker. Use command:
```
baker ssh
```
4. Change permission of private key
```
chmod 600 ~/.ssh/web-srv
```
5. Changed into linked directory for ansible server
```
cd /ansible-srv/
```
6. (Recommended but optional) Modify database and other config variables. As your keys are not committed to the repository, these config variables in git do not leave your system exposed but it is recommended to not save them in Git and change them.
```
vim vars/common.yml
```

7. Call ansible playbook main.yml where all the related playbooks and files are called from.
````
ansible-playbook main.yml -i inventory
````
8. Open browser on http://192.168.33.100:8065 to open mattermost.
If everything installs correctly, the browser should open a mattermost window. 

9. Login with user_1 as specified in vars/common file, add comment in team channel, check for message after login with user_2 as specified in vars/common file.

## ScreenCast link
https://drive.google.com/file/d/1tnCCLj8mYyY-OZI4c0Kzzu1at7N2Zd82/view?usp=sharing

## Authors
Shefali Agarwal (sdagarwa@ncsu.edu)
