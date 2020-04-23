# marxan-server
Back end Marxan Server installation for running Marxan Web. See also [marxan-client](https://github.com/marxanweb/marxan-client).

## Architecture
The following image shows the high level architecture of marxan-server. 
![marxan-server architecture](https://github.com/marxanweb/marxan-client/raw/master/architecture_client.png)  

## Installation
The following instructions describe how to install on Ubuntu 18.04 LTS. For Windows, see [here](https://github.com/marxanweb/general/releases)    

### Clone the repo:  
In the folder where you want to install marxan-server, type the following:
```
git clone https://github.com/marxanweb/marxan-server.git
```
### Install marxan-server:
```
marxan-server/install.sh
```

### Start marxan-server:
```
sudo marxan-server/startup.sh
```

## Test the installation
To test the installation goto: http://\<host\>/marxan-server/testTornado.  

To run a complete set of unit tests:  
```
cd marxan-server/
./unittest.sh
```
  
## Configuration  
marxan-server can be configured to change various settings including linking to an existing database, configuring security etc. For more information see the [Administrator Guide - Configuration](https://docs.marxanweb.org/admin.html#configuration).  

## Starting automatically

You can also configure marxan-server to start automatically whenever the server is started. For example, on a Google Cloud Platform VM you can use the startup script (/marxan-server/startup.sh) like the following (replace \<user\> with your logged in user name):

```
#!/bin/bash -i
${CONDA_EXE} activate base
screen -d -m ${CONDA_PYTHON_EXE} /home/<user>/marxan-server/marxan-server.py
```

Then this can then be added to the VM so that it is run when the server starts:

```
gcloud compute instances add-metadata <instance> --metadata-from-file startup-script=/home/<user>/marxan-server/startup.sh
```

## Troubleshooting
### Cannot connect to marxan-server
If you see a connection refused error on attempting to connect, then it is likely that a Firewall is blocking the connections. Add the following rules: Allow TCP:80, TCP:8080, TCP:8081 for the IP ranges 0.0.0.0/0. 

### Server stops running after a while
On some Cloud hosts like Google Cloud Platform, when the SSH connection is closed then the instances may be shut down, thus terminating the marxan-server. To avoid this, use Virtual Terminal software like screen. For more information see [here](https://www.tecmint.com/keep-remote-ssh-sessions-running-after-disconnection/).  For example:  

```
screen python marxan-server.py
```
