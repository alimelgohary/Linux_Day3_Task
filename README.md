1.	Create a system user (no login shell, no home directory) named webapp_user. This user will own the application files.
`sudo useradd -rM -s /sbin/nologin webapp_user`

2.	Create a system group named webapp_support.
`sudo groupadd -r webapp_support`

3.	Create a regular user named support1. Ensure this user is added to the webapp_support group as a secondary group.
`sudo useradd support1`
`sudo usermod -aG webapp_support support1`


4.	Create the following directory tree under /opt/webapp/
`sudo mkdir -p /opt/webapp/bin`
`cd /opt/webapp`
`sudo mkdir config logs`
 

5.	Change the ownership of the entire /opt/webapp/ directory and all its contents to be owned by the user webapp_user and the group webapp_support
`sudo chown -R webapp_user:webapp_support .`


6.	Set directory permissions so that:
    a. webapp_user has full read, write, and execute access to everything.
        `sudo chmod -R u+rwx .`    

    b. Members of the webapp_support group can: 
          ▪ Read and list contents of the config/ and logs/ directories. 
                `sudo chmod g=rx config/ logs/`
          ▪ Read files inside config/ and logs/. 
                `sudo chmod -R g=r config/ logs/`
          ▪ Have no access (cannot list, read, or write) to the bin/ directory.
                `sudo chmod -R g-rwx bin/`

    c. All other users on the system (others) must have no access to any part of /opt/webapp/.
        `sudo chmod -R o-rwx .`
 