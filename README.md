# ohsu-cm
OHSU configuration management

Currently, hyrax 2 derivatives only work with this configuration on Ubuntu 16.10, ami-b374d5a5.

## General instructions
Clone this repo to your local system to build a demo environment on AWS.  

1. Ensure you have ansible >= 2.3 installed
1. Make an EC2 server using `ami-b374d5a5` (Ubuntu 16.10) and put the IP address in `hosts` under `ohsu_demo_servers`. Ansible-samvera at present does not create a server for you the way ansible-hydra does.
1. Ensure you have [boto](https://boto3.readthedocs.io/en/latest/) >= 3 installed
1. Get your aws access key and secret from https://console.aws.amazon.com/iam/home?region=us-east-1#/users
1. Export your key and secret to environment variables:
   ```
    export AWS_ACCESS_KEY_ID='AK123'
    export AWS_SECRET_ACCESS_KEY='abc123'
   ```
1.  `git clone --recurse https://github.com/bess/ohsu-cm.git`
1.  `cd ohsu-cm`
1.  Check your connection:
   `ansible-playbook check-connection.yml`
1. If that runs without errors, run ansible:
  `ansible-playbook -i hosts build_ohsu_demo_server.yml`
