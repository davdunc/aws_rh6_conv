AWS RHEL 6 to RHEL 6 ELS Conversion
=========

This role allows the user to convert the root volume of an on-demand RHEL 6 instance to a Marketplace instance of the On-demand RHEL 6 with Extended Lifecycle Support. 

As of now, the role supportes converting instances built from AMIs that are backed by official RHEL 6 AMIs provided by Red Hat, so the instance from which the conversion must have the following: 
 - a valid RunInstance:0010 code identifying that it is derivative of the official AMI. 
 - access to the external network for access to the RHEL 6 ELS updates.
 
There are many ways to approach making a move from one instance to another. The images built for the RHEL 6 Extended Lifecycle Support for 
 

Requirements
------------

Access to the external Amazon EC2 network to connect to the ec2 API. 
IAM permissions must allow for the creation of a VPC and subnets across all AZ's 
When configuring the role in the placy 

Role Variables
--------------

#### `aws_inject.aws_access_key`
    The Account Access key default is `null`. If ithis is not set then
    the value of the *AWS_ACCESS_KEY_ID*, *AWS_ACCESS_KEY* or
    *EC2_ACCESS_KEY* environment variable is used. See
    [configuring the aws cli](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-configure.html "Configuring the AWS CLI") documentation for additional details on configuring
    credentials (Aliases: ec2_access_key, access_key)[Default: (null)]

#### `aws_inject.aws_secret_key` 
    The AWS secret key default is `null`. If not set then the value of
    the *AWS_SECRET_ACCESS_KEY*, *AWS_SECRET_KEY*, or EC2_SECRET_KEY
    environment variable is used. See [configuring the aws
    cli](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-configure.html
    "Configuring the AWS CLI") documentation for additional details on
    configuring credentials (Aliases: ec2_secret_key,
    secret_key)[Default: (null)] type: str

#### `instance_tag`
     This is the tag assigned to the instances you wish to migrate
     from RHEL 6 to RHEL 6 ELS. By default, this is set to
     `rhel-6-els`

Dependencies
------------

This is dependent upon the following collections:
  - aws.amazon
  - community.amazon

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

When running this playbook, it is important to know that it is configured to run all the tasks for each instance. If you do not choose to run it across individual instances, the information will not be associated with the correct instances: 

    - hosts: tag_task_convert_rhel_6_to_els
      serial: 1
      roles:
         - { rhel_6_els: region: us-east-1, profile: default }
         
I am looking for assistance in making this run in an idempotent way, but there is so much scaffolding for the instance conversion that much of the content was not manageable without creating many complex associative arrays. 

License
-------

Apache-2.0

Author Information
------------------

David Duncan <davdunc@amazon.com> 
