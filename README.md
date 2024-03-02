# iia-ca-demo

## cloudformation commands
update ~/.aws/credentials\
aws cloudformation validate-template --template-body iia_ca1_cfn.yaml\
aws cloudformation create-stack --stack-name iia_ca1 --region us-east-1 --tags Key=Name,Value=iia_ca1 --template-body iia_ca1_cfn.yaml\
aws cloudformation delete-stack --stack-name iia_ca1 --region us-east-1

# demo
## ssh to management host, public IP in CF outputs
ssh -i labuser.pem ubuntu@websubnet1.internal.tud

## on managment host, setup SSH agent
source ~/.bashrc\
cd ~ && eval `ssh-agent -s` && vi labuser.pem\
chmod 400 labuser.pem && ssh-add labuser.pem

## ansible checks
ansible servers -m ping\
ansible web -m ping

## run automation
cd iia-ca-demo\
ansible-playbook patch-playbook.yaml\
ansible-playbook nginx-playbook.yaml

## connect to load balancer URL provided in CF outputs
