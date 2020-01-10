# Connect to Your Linux Instance using an SSH Client
- ``ssh -i /path/my-key-pair.pem ec2-user@ec2-198-51-100-1.compute-1.amazonaws.com``
- (``ssh -i /path/my-key-pair.pem user@ip_address`` )

# Copying Files Between Local Computer and Instance (AWS)
- To copy files between your computer and your instance you can use an FTP service like FileZilla or the command scp which stands for secure copy.
- To use scp with a key pair use the following command: ``scp -i path/to/key file/to/copy user@ip_address:path/to/file.``
- To use it without a key pair, just omit the flag -i and type in the password of the user when prompted.
- To copy an entire directory, add the -r recursive option:
``scp -i path/to/key -r directory/to/copy user@ip_address:path/to/directory``

# Deployment
- Use SSH Agent plugin
  - Add credentials - SSH username with private key
  - Add the .pem private key created in AWS
- Execute shell
  - In shell script add something like:
````
scp -o StrictHostKeyChecking='no' -r app ubuntu@34.253.192.79:/home/ubuntu/
scp -o StrictHostKeyChecking='no' -r environment ubuntu@34.253.192.79:/home/ubuntu/

ssh -o StrictHostKeyChecking='no' ubuntu@34.253.192.79 <<EOF
	echo 'Run bash files (make sure you can actually run)'

    echo 'Go to the right directory'
    echo 'install dependencies'
    echo 'Start our app'

    cd environment/
    cd app
    chmod +x provision.sh
    ./provision.sh

    cd ..
    cd db
    chmod +x provision.sh
    ./provision.sh

    cd ..
    cd ..
    cd app
    npm install
    npm start &
    exit


EOF  
````

## Changing permission to execute file
`` chmod +x <file_name> ``

## How to run.sh files
`` ./file_name.sh ``

--- Dev branch Test 3

## AWS
EC2
Ubuntu Server 18.04 LTS (HVM), SSD Volume Type
1.	T2 micro
2.	Enable auto-assign IP
3.	Skip storage
4.	Added tag
5.	Source my IP

Deny everything in general and allow what you need
Changed to Launch-wizard-6
HTTP – 80
SSH – 22
3000
Decide where we want to SSH into
cd ~/.ssh
ssh -i ~/.ssh/thomas-eng-48-first-key.pem ubuntu@54.171.133.226 (ip is your public)
note don’t need ~/.ssh/ however makes it absolute (can be used everywhere)
exit
ssh -i daniel-eng-48-first-key.pem ubuntu@54.171.133.226

Manually deploying code to a server online using the provisions
- atom . to deployment code
- Make sure the provisions are executable in app by using command ll in the folder and db admin, owner and groups should be executable
- If not chmod +x provision.sh or can do it inside linux
- If we want to run in linux from windows – dos2unix -h

Back to app to provision - dox2unix provision.sh

Using SCP command to securely copy files from local machine to AWS

To use scp with a key pair use the following command: scp -i path/to/key file/to/copy user@ec2-xx-xx-xxx-xxx.compute-1.amazonaws.com:path/to/file.
	To use it without a key pair, just omit the flag -i and type in the password of the user when prompted.

scp -i ~/.ssh/thomas-eng-48-first-key.pem ../environment/app/provision.sh ubuntu@54.171.133.226:/home/ubuntu/file.sh

the file should then be in your ubuntu ssh

./file.sh – to run the file

Can use it in recursive mode when you want to transfer several files at once

To copy a directory (in this case environment) to Ubuntu

scp -i ~/.ssh/thomas-eng-48-first-key.pem -r ../environment/ ubuntu@54.171.133.226:/home/ubuntu/

To run it:

./provision.sh

To give executable instructions:

chmod +x provision.sh

To set a path e.g. if I had to download dos2unix -h

Path > edit system environment variables > environmental envariables

Copy dos2unix and put it inside windows/system32

To terminate:

Exit ubuntu

Actions > Instance State > Stop > wait to stop then Terminate
.
