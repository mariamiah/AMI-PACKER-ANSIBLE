### AUTOMATED MACHINE IMAGE - ANSIBLE & PARKER
This projects sets up an Amazon Automated Machine Image using Packer and provisions it using Ansible

### Setting up Packer
#### Packer Installation
Although there are number of ways of installing Packer, using a precompiled binary is the most recommended way as shown below:
   - [macos](http://macappstore.org/packer-2/)
   - [freeBSD, Linux and Windows](https://computingforgeeks.com/install-latest-packer-on-linux-freebsd-macos-windows/)

#### Setup Packer Template for build config

The Packer template file comprises of a json object that contains the following keys:
- Variables: These help provide abstraction and protect sensitive keys such as AWS access keys
- Builders: Contains a set of configurations that packer follows to build the image
- Provisioners: Contains paths to files that have all the necessary installation instructions to set up and customise the AMI
- Post-processesors: These are optional, and they can be used to upload artifacts, re-package and transform an artifact

#### Building the AMI with Packer
Inorder to build an AMI with Packer, the following files must be present according to this project repository:
- packer.json - This file consists of the Packer template as discussed in the step above
- playbook.yml - This is an Ansible playbook YAML file that comprises of step by step instructions that are followed while provisioning the AMI. They are executed using a top-down approach
- ansible_installation.sh - Comprises of a function that contains a number of instructions to install ansible onto the Amazon machine image
- The packer.json file consists of  the variables section has aws_access_key and aws_secret_key which reads the keys from the .env file that should be created as explained in the setup step below

#### Setting Up this project
- Create an AWS account here https://aws.amazon.com if you do not have one
- Clone this repository by using `https://github.com/mariamiah/AMI-PACKER-ANSIBLE.git`
- Navigate into the `AMI-PACKER-ANSIBLE` folder
- Create a .env file
- Add your AWS credentials as shown in the `sample_env.txt` file
- To get your access and secret keys please follow AWS documentation here https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html#Using_CreateAccessKey
- Run the command `packer build packer.json` to set up the AMI and provision it with Ansible

#### LAUNCH THE AMI
- Navigate to your AWS console and select the EC2 service
- Select AMI on the left panel and view your recently created AMI
- Select this AMI and click the blue launch button at the top.
- Follow through all the necessary steps according to the installation assistant
- Complete the configuration by selecting the 'review and launch` button
- Create a new key pair or select an existing one.
- Once the setup is complete, copy the IPv4 public address of the instance and add it to the broswer window in order to view the deployed application
