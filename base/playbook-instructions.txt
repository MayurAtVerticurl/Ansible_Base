#Run command

ansible-playbook -i inventory.ini kubectl_run.yml


#To login without  password run the ssh and ansible as "ansadmin"


# run this as Root to copy the .kube/config
sudo su
cp -r $HOME/.kube /home/ansadmin

chown ansadmin:ansadmin /home/ansadmin/.kube/config


# insall plugin for confirmation

ansible-galaxy collection install community.general
