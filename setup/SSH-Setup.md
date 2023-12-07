# Setup SSH 

- add a user (on BOTH)

        useradd -m -s /bin/bash ansadmin
        passwd ansadmin

password : `ansadmin`

- adding the user to Sudoers List 

        visudo
        ansadmin  ALL=(ALL)        NOPASSWD:ALL

        # EXAMPLE
        root@ip-172-31-6-252 ec2-user]# visudo
        root        ALL=(ALL)        ALL
        ansadmin  ALL=(ALL)        NOPASSWD:ALL

        %sudo   ALL=(ALL:ALL) NOPASSWD: ALL

        sudo usermod -aG sudo ansadmin
- Give Permission to the USer for ssh folder on WORKER

        sudo su ansadmin
        cd 
        mkdir -p ~/.ssh
        touch ~/.ssh/authorized_keys

        chmod -R 700 ~/.ssh
	    chmod 600 ~/.ssh/*

- Permitting Passwdless Login on WORKER

        # sudo is mandatory
		sudo nano /etc/ssh/sshd_config

		# To disable tunneled clear text passwords, change to no here!
        PasswordAuthentication yes
        PermitRootLogin yes #(PermitRootLogin prohibit-password for ubuntu)
        ClientAliveInterval 1200
        ClientAliveCountMax 3

- Add Hosts in known hosts

        #add host to list
        ip.ad.dr.ess    ansadmin

- generate and Copy SSH key to other nodes (on MASTER)

        sudo su - ansadmin 
        ssh-keygen -t rsa
        ls -a
        cd .ssh

        ssh-copy-id ansadmin@<ip> 


        cat ~/.ssh/id_rsa.pub
            Copy it to the remote ~/.ssh/authorized_keys
            [cat ~/.ssh/id_rsa.pub | ssh ansadmin@kmaster 'cat >> ~/.ssh/authorized_keys']



### >>>>See SSH-Setup.md