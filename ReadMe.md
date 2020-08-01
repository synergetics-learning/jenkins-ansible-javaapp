# Setup Jenkins with Ansible for deployment

1. Start Jenkins server, connect using SSH inside Jenkins Master.

```
$ sudo apt update -y
$ sudo apt install ansible -y
```

2. Visit Jenkins Dashboard, Install new plugin "Ansible Plugin" Use "Install without Restart"

3. From Jenkins dashboard, goto "Global Tool Configuration" > Setup path for Ansible "/usr/bin"

4.  Create an additional virtual machine in same VPC / VNet as jenkins master. Lets call it "Sample1" 

5. Use SSH connection with Jenkins Master, to create a new SSH Keypair and Use "private-key" in Jenkins credentials and public-key tobe copied to "Sample1"

```
$ cd /home/$USER
$ mkdir temp
$ ssh-keygen 
Path for Public Key: /home/$USER/temp/id_rsa.pub
Pass Phrase: <ENTER>
$ cd temp
$ ls
## Lets copy PUBLIC Key to Sample1
## Private IP of Sample1 : 10.0.1.5
$ ssh-copy-id -i /home/$USER/temp/id_rsa.pub mahendra@10.0.1.5
Accept the server thumbprint: YES
## Change File permissions of SSH Keys
$ chmod 600 id_rsa
$ chmod 600 id_rsa.pub
## Test the connectivity with 10.0.1.5
$ ssh -i /home/$USER/temp/id_rsa mahendra@10.0.1.5
## You should be now connected
$ exit
## Display contents of PRIVATE KEY on Screen
$ cat id_rsa
## Just COPY entire private key
```

6.  Open Jenkin dashboard > Manage Credentials > Global Credential Manager "Jenkins" > Add Credentials

    Choose option "SSH Username with private key"

    ```yaml
    ID: webhostid
    Description: SSH Credentials for Web Host
    Username: mahendra
    Private Key: Enter Directly
        PASTE the key copied from SSH Terminal
    ```

    Save the credentials


