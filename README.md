## awsserver

Create a virtual server in AWS.

## Requirements

1) Remove keypair from AWS and private key from ~/.ssh

2) Set environment variables

    export AWS_ACCESS_KEY_ID='AK123'
    export AWS_SECRET_ACCESS_KEY='abc123'

3) Install `boto`.

If you do not wish to use private DNS (route53), VPC variable is not
needed and can be removed


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
        iam_role: Web
        iam_policy: Web
    
      roles:
        - { role: aws_ec2_key }
        - { role: aws_group }
        - { role: aws_policy, policy_document: 'files/policies/Web.json' }
    
        ## CHECK ME
        - { role: aws_ec2, tag_name: frodo, instance_type: t2.small }

## Connect

    ssh -i ~/.ssh/<key_name> <os-user>@<tag_name>.<dns_zone>
