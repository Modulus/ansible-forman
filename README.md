# How to use this
1. vagrant up
2. vagrant ssh machine1
3. cd /vagrant
4. ansible-playbook playbook.yml
. Done
*Keep in mind this will take some time to run, so please be patient*

Access 192.168.89.21:8031 for foreman dashboard

# To run on ec2/azure etc
1. Create ubuntu 14.04 node
2. Run "sudo sh install_ansible.sh"
3. sudo apt-get install git
4. git clone https://github.com/Modulus/ansible-forman.git
5. cd into ansible-forman
6. change inventory folder in ansible.cfg
7. ansible-playbook playbook.yml
