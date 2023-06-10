# Containerize a python application

In this project, we will containerize a simple python application using docker. We will go through the steps below.

- Deploy the application on a Linux machine

- Write the Dockerfile using an Ubuntu base image 

- write the Dockerfile using a python base image.

## A- Deploy  the application on a Linux machine ( it can be running anywhere , aws lightsail, aws ec2 , linode server or on prem servers).

### NB: In this project I'm using centos

## Step1- Installing Environment dependencies
### Installing python  and pip3

Run the command below to install python.
```
sudo yum update
```

Now install python3
```
yum install python3 -y
```
once it's installed, we will go ahead and install python3-pip

run the command 
```
yum install python3-pip -y
```

we are done with the Environment dependencies, let's go ahead and clone the application from GitHub.

# Step2- Clone the Application from GitHub
clone the application from github is the equivalent of copying the application.
```
git clone https://github.com/utrains/bookshopflaskapp.git
```

move into the directory

```
cd bookshopflaskapp
```

# Step3- Install application base dependencies
here, we will install the dependencies needed for the application to run. The list of the dependencies should be provided by the developer.
```
pip3 install -r requirements.txt
```
### NB: all these details are given by developers during the meeting.
After installing the pip we'll open the port 5000.

# Step4- Exposing port
exposing ports varies from one provided to another. For example, if you are on EC2 you will use security groups, if you are Google VMs, you will use Google firewalls etc.

if you are running on a centos7 / redhat7  on prem, you can bellow command to do it.
```
firewall-cmd --permanent --add-port=5000/tcp
firewall-cmd --reload 
```
run it in the root account.

if you have this error
![image](https://github.com/Tyannherve11/Containerize-a-python-application/assets/37128739/e55e85c7-2eee-4fd2-9c95-2dc91491dc5f)

run the following commands
```
rpm -qa firewalld
yum install firewalld
```
then 
```
ll /usr/lib/systemd/system | grep firewalld
```
or 
```
ll /etc/systemd/system | grep firewalld
```
verify if the firewall is acitvate
# check the status of the service (running and enabled)
```
systemctl status firewalld
```

# if the service is not running, start it
```
systemctl start firewalld
```

# if the service has exited, restart it(check for error if any)
```
systemctl restart firewalld
```
# if the service is not enabled, enable it
```
systemctl enable firewalld
```

and if you are on ubuntu or Debian, then run this instead
```
ufw allow 5000/tcp
service ufw restart
```


# Step5- Start the application.
To start the application, make sure you are in the application directory
```
cd ~/bookshopflaskapp
```

Now run the cmd
```
flask run --host=0.0.0.0
```


