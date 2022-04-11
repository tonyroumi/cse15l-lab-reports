# **Lab Report 1**
Anthony Roumi <br>
April 10, 2022 

---
## Remote Access Tutorial
_This tutorial will guide you step by step on how to log into a course specific account on `ieng6`. You will learn basic commands, how to move files from client to server, and optimizing remote running._
## Step 1 - _Installing Visual Studio Code_
Go to the [Visual Studio Code](https://code.visualstudio.com/) website, and follow the instructions to install the source-code editor. After it is installed, open the program. You should see a window that looks something like this:

![Image](https://github.com/tonyroumi/cse15l-lab-reports/blob/78948cf8fb42d6e277a3a271af76cd9419baaa91/Week%201/Screen%20Shot%202022-03-31%20at%204.14.55%20PM.png)

## Step 2 - _Remotely Connecting_
If you are on Windows you must install a program called [OpenSSH](https://docs.microsoft.com/en-us/windows-server/administration/openssh/openssh_install_firstuse) to allow for your computer to be able to connect to other computers with this account. <br>
If you are not on windows or you have finished, then look up your course related specific account [here](https://sdacs.ucsd.edu/~icc/index.php).

Now, in Visual Studio Code we will connect to the remote server. Open up a terminal and input this command. <br>

`$ ssh cs15lsp22XX@ieng6.ucsd.edu` <br>
NOTE: replace the 'XX' with your course specific account. <br>
You should get a message like this since it is your first time remotely connecting: <br>
```
The authenticity of host 'ieng6.ucsd.edu (128.54.70.227)' can't be established. 

RSA key fingerprint is
SHA256:ksruYwhnYH+sySHnHAtLUHngrPEyZTDl/1x99wUQcec.

Are you sure you want to continue connecting
(yes/no/[fingerprint])?
```

Say yes to these messages when connecting to a new server for the first time. After you input yes, it should prompt you for your password.

>NOTE: The password is hidden, proceed and press enter.

![Image](https://github.com/tonyroumi/cse15l-lab-reports/blob/78948cf8fb42d6e277a3a271af76cd9419baaa91/Week%201/Screen%20Shot%202022-03-31%20at%204.17.00%20PM.png)

You are now connected to the remote server in the CSE basement and any commands you run will run on that computer. 

## Step 3 - _Trying Some Commands_
Try running some commands that you have learned in class. Here is a list of some useful commands. Test them out, what happens?
```
- pwd: print working directory
- ls: list files
    * ls -a (list all files)
- cp: copy
- mkdir: make directory
- rm: remove
- cat: view or create a file
- touch: create a file
- man: display command manual 
```

![Image](https://github.com/tonyroumi/cse15l-lab-reports/blob/23fe98c1783a3a063df0547a3dde38bccc4cc8d4/Week%201/Screen%20Shot%202022-04-10%20at%207.39.01%20PM.png)

## Step 4 - _Moving Files with scp_
Another way to copy a file from your computer onto a remote server is with the command `scp`. <br>
Create any file on your computer with the extension .java. Make sure the file will compile. <br>

>NOTE: If you do not have java, don't worry about this step. You should still make the file.

Then from the terminal in the same directory as the newly made file, input this command: <br>
`scp FILE.java cs15lsp22XX@ieng6.ucsd.edu:~/`<br>
You will be prompted for a password, input your password and press enter.

![Image](https://github.com/tonyroumi/cse15l-lab-reports/blob/23fe98c1783a3a063df0547a3dde38bccc4cc8d4/Week%201/Screen%20Shot%202022-03-31%20at%204.45.53%20PM.png)

You have successfully copied the file onto the remote server. <br>
Now, log into `ieng6` and check the list of files. You should see the newly created file. Run the code from the remote machine, it should execute with no problems. 

## Step 5 - _Setting an SSH key_
Anytime we run scp or ssh we are promted for our password. This can be frustrating and interrupt one's flow. A solution to this is to use a program called `ssh-keygen`. 

This command creates a public key and a private key. You transfer a copy of the public key to a specific location on the server, and the private key to a specific location on the client. 

__On the client (your computer) run the command__
`$ ssh-keygen` <br>
You should see:
```
Generating public/private rsa key pair.

Enter file in which to save the key
(/Users/<user-name>/.ssh/id_rsa): /Users/<user-name>/.ssh/id_rsa

Enter passphrase (empty for no passphrase):
```

>NOTE: DO NOT enter a passphrase (leave blank)

After this you should see something that looks like this: <br>
![Image](https://github.com/tonyroumi/cse15l-lab-reports/blob/b54743f80c8224f76e8565337d325a6ea7134379/Week%201/Screen%20Shot%202022-03-31%20at%204.51.25%20PM.png)

>If you are on windows, follow the extra steps [here](https://docs.microsoft.com/en-us/windows-server/administration/openssh/openssh_keymanagement#user-key-generation).

You have successfully created two new files on your system. The private key (stored in id_rsa) and the public key (stored in id_rsa.pub), stored on your computer. <br>
Next, you will need to copy the __public__ key to the `.ssh` directory on the server. 

Log onto the server with `ssh cs15lsp22zz@ieng6.ucsd.edu` and make the directory using `mkdir .ssh`.

After you have done this, logout. Now use what you have learned with scp to copy the public key over to the newly created directory. 

`$ scp /Users/<user-name>/.ssh/id_rsa.pub
cs15lsp22XX@ieng6.ucsd.edu:~/.ssh/authorized_keys`

>NOTE: Use your own username.

Now you should be able to login or use scp to the server without entering your password. 

![Image](https://github.com/tonyroumi/cse15l-lab-reports/blob/b54743f80c8224f76e8565337d325a6ea7134379/Week%201/Screen%20Shot%202022-03-31%20at%205.40.06%20PM.png)

## Step 6 - Optimizing Remote Running
There is an easier process to calling commands on the remote server.

You can write a specific command in quotes at the end of running the ssh command. <br>
For example: <br>
`$ ssh cs15lsp22zz@ieng6.ucsd.edu "mkdir hello"` <br>
Will make a new directory called hello on the remote server. <br>
This applys to all commands, try and test each one yourself and observe what happens.

Another way of optimizing commands is to run multiple commands on the same line. 
* `cp hello.java; javac hello.java; java hello`


![Image](https://github.com/tonyroumi/cse15l-lab-reports/blob/b54743f80c8224f76e8565337d325a6ea7134379/Week%201/Screen%20Shot%202022-03-31%20at%205.51.30%20PM.png)

That's it! You have learned how to connect to a remote server, the basic unix commands, how to move files using `scp` command, you set up an SSH key, and learned optimal remote running tricks. 



