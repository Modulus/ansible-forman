# How to use this
1. vagrant up
2. vagrant ssh machine1
3. cd /vagrant
4. ansible-playbook playbook.yml
. Done
*Keep in mind this will take some time to run, so please be patient*

Access 192.168.89.21:8031 for foreman dashboard

# To run on ec2/azure etc
1. Create ubuntu 16.04 node, (It will not be as easy on an older ubuntu version)
2. Run "sudo sh install_ansible.sh"
3. sudo apt-get install git
4. git clone https://github.com/Modulus/ansible-forman.git
5. cd into ansible-forman
6. change inventory folder in ansible.cfg
7. ansible-playbook playbook.yml

## This playbook also install and configures the following
1. salt-master
2. salt-minion
3. salt-api

## Verify salt-api:
curl -sSk https://localhost:9191/login \
    -H 'Accept: application/x-yaml' \
    -d username=bob \
    -d password=bob \
    -d eauth=pam

You should get a return message that looks something like this:
return:
- eauth: pam
  expire: 1479337165.176836
  perms:
  - '@runner'
  - '@wheel'
  - '@jobs'
  - test.*
  start: 1479293965.176831
  token: 6fd812929febdeda24e2731517d01d1f14994137
  user: bob    

curl -sSk https://localhost:9191 \
     -H 'Accept: application/x-yaml' \
     -H 'X-Auth-Token: 6fd812929febdeda24e2731517d01d1f14994137'\
     -d client=local \
     -d tgt='*' \
     -d fun=test.ping

*check /var/log/salt/master for errors*

### For generating new password
1. Make sure you have the "whois" package installed
*sudo apt-get install whois*
2. Run mkpasswd --method=sha-512
3. Paste the result into roles/salt/tasks/users.yml


# NB!!!!
/usr/sbin/upload-salt-reports keeps failing. Python 2.7.11 is needed for this to work
This probably means you are running a ubuntu version lower than 16.04

Also you need to change the minion id to the fqdn using sudo salt-cloud -a rename oldname newname=newname
You also need to change this in the /etc/salt/minion file....
