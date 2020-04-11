# Cloud Custodian

This is an example policy repository to be used alongside https://github.com/RootPrivileges/terragrunt-aws-demo. This repository contains a Cloud Custodian policy to start/stop EC2 resources tagged with "CustodianOffHours" when they are running outside of the 08:00 - 22:00 GMT schedule.

The https://github.com/RootPrivileges/terragrunt-aws-demo-modules repository does the necessary set up to provision the custodian user, set up Access Keys and an S3 bucket for logging. After the account-init.sh script has been successfully run, the orgaccounts.py (latest version downloaded by wget during installation below) is responsible for creating accounts.yml, which holds the account IDs and provision roles for the organisation children accounts. After c7n-org is executed, Cloud Custodian deploys the necessary Lambda functions to run the checks once an hour, starting or stopping any matching instances at the correct time.

## Install

```
sudo apt install -y python3-venv

git clone https://github.com/RootPrivileges/cloud-custodian-aws-demo.git

python3 -m venv venv
source venv/bin/activate
pip3 install c7n c7n-org
wget https://raw.githubusercontent.com/cloud-custodian/cloud-custodian/master/tools/c7n_org/scripts/orgaccounts.py
```

