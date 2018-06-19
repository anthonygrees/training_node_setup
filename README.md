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
- FQDN - Public IP Address or Fully Qualified Domain Name or your Node
- USER - 'centos' 
- PWD - Is the password (Use the '-i' for ~\.ssh\id_rsa )
- node1 - The name.... You can use any name....

## AWS EC2 Specific Examples
This is an example BOOTSTRAP command on AWS EC2 training lab BJC:
```
$ knife bootstrap -i ~\.ssh\id_rsa centos@ec2-xxx-xxx-xxx-xxx.us-west-2.compute.amazonaws.com -N node1 --sudo
```
This is an example ADD RECIPE command on AWS EC2 training lab BJC:
```
$ knife node run_list add node1 "recipe[your_cookbook]"
```
This is an example bootstrap and add recipe command on AWS EC2 training lab BJC:
```
$ knife bootstrap -i ~\.ssh\id_rsa centos@ec2-xxx-xxx-xxx-xxx.us-west-2.compute.amazonaws.com -N node1 --sudo --run-list 'recipe[your_cookbook]'
```

## Converge Your Recipe
Converge node 1 and run the Chef-Client
```
$ knife ssh 'name:node1' 'sudo chef-client' -x centos -i ~\.ssh\id_rsa
```
Converge all your nodes
```
$ knife ssh "*:*" "sudo chef-client" -x centos -i ~\.ssh\id_rsa
```

## Should the AWS Reaper take down your nodes
Remove the missing nodes from Chef Server
```
##Delete all nodes
$ knife node delete node1
$ knife node delete node2
$ knife node delete node3
$ knife node delete node4
```

Restore node1
```
$ knife bootstrap -i ~\.ssh\id_rsa centos@ec2-xxx-xxx-xxx-xxx.us-west-2.compute.amazonaws.com -N node1 --sudo -r 'role[web]' -E production
```
Restore node2
```
$ knife bootstrap -i ~\.ssh\id_rsa centos@ec2-xxx-xxx-xxx-xxx.us-west-2.compute.amazonaws.com -N node2 --sudo -r 'role[web]' -E production
```
Restore node3
```
$ knife bootstrap -i ~\.ssh\id_rsa centos@ec2-xxx-xxx-xxx-xxx.us-west-2.compute.amazonaws.com -N node3 --sudo -r 'role[loadbalancer]' -E production
```
Restore node4
```
knife bootstrap -i ~\.ssh\id_rsa centos@ec2-xxx-xxx-xxx-xxx.us-west-2.compute.amazonaws.com -N node4 --sudo -r 'role[web]' -E acceptance
```
