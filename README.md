## ansible-role-awsserver

Create a virtual server in AWS.

## Requirements

To install this role:

    cat requirements.yml
	- src: https://github.com/jreisinger/ansible-role-awsserver
      version: master
      name: ansible-role-awsserver
    
    ansible-galaxy install -r requirements.yml -p ~/ansible-roles/

	cat ansible.cfg
	[defaults]
	roles_path = ~/ansible-roles

Remove keypair from AWS and private key from ~/.ssh

Set environment variables

    export AWS_ACCESS_KEY_ID='AK123'
    export AWS_SECRET_ACCESS_KEY='abc123'

Install `boto`.

## Example Playbook

	- hosts: localhost
	  connection: local
	  gather_facts: False
	
	  vars:
	
	    region: eu-west-1
	    vpc_id: vpc-3ca45d58
	    vpc_subnet_id: subnet-0a81266e
	    dns_zone: reisingers.org
	
	    key_pair_name: ansible-frodo
	    security_group: web_sg
	
	    tag_name: frodo
	    instance_type: t2.small
	
	  roles:
	    - { role: ansible-role-awsserver }

## Connect

    ssh -i ~/.ssh/<key_name> ubuntu@<tag_name>.<dns_zone>
