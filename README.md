# training_node_setup

## Description
This cookbook is for Chef students to use.  It stands up 3 nodes of Centos in their lab that they can use to bootstrap to their own Chef Server

## How to Use
You run the following command:
```
$ kitchen create
```
Check in the .kitchen folder and you will find the IP and FQDN details

## Bootstrap Details
Run the following command
```
$ knife bootstrap FQDN -x USER -P PWD --sudo -N node1
```
FQDN - Public IP Address or Fully Qualified Domain Name or your Node
USER - 'centos'
PWD - Is the password (Use the '-i' for ~\.ssh\id_rsa )
node1 - The name.... You can use any name....

This is an example bootstrap command on AWS EC2 training lab BJC:
```
$ knife bootstrap -i workshop.pem centos@ec2-XX-XXX-XXX-XXX.us-west-2.compute.amazonaws.com -N Your_Node_Name --sudo -run-list 'recipe[Your_Cookbook_Name]'
```


