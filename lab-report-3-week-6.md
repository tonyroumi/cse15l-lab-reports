# **Lab Report 3**
Anthony Roumi <br>
May 8, 2022 

---
## Github actions, Unix commands, and Shell Scripting
_These past two weeks we have learned about better software development techniques as well as workflows within github. A workflow is a configured automated process that allows for faster and more efficient testing. We have learned more unix commands to filter through files and more efficiently execute code through the command line. We have also learned about shell scripting, which is run by Unix shell to interpret the command line._

---

### Streamlining `SSH` Configuration
We will create a config file in the `.ssh` directory. We will access the file using the git command __`nano`__ to use the __nano editor__. Or simply access the file via `.ssh/config:` 

![image](https://github.com/tonyroumi/cse15l-lab-reports/blob/main/Lab%20Report%203/config%20file%20in%20ssh.png?raw=true)

 Within this config file we will set the host configuration to `ieng6`, accessing the server `ieng6.ucsd.edu` with my user login `cs15lsp22ato`.

![image](https://github.com/tonyroumi/cse15l-lab-reports/blob/main/Lab%20Report%203/nano%20editor.png?raw=true)

<br>

We are now able to access the server using the configuration host `ieng6`.

<br>

![image](https://github.com/tonyroumi/cse15l-lab-reports/blob/main/Lab%20Report%203/login%20with%20new%20host%20configuration.png?raw=true)


>We are also able to copy files over to the server using the newly created host configuration. 

![image](https://github.com/tonyroumi/cse15l-lab-reports/blob/main/Lab%20Report%203/scp%20to%20server.png?raw=true)
___

### Setup Github Access from `ieng6`
First we must add the key previously made for remote access to my Github account. This public key is stored under `/users/anthonyroumi/.ssh/id_rsa.pub` and is accessable via the __`cat`__ command.

![image](https://github.com/tonyroumi/cse15l-lab-reports/blob/main/Lab%20Report%203/cat%20key%20stored%20local.png?raw=true)

Now store the corresponding key on Github under settings/access in the _SSH and GPG key_ tab

![image](https://github.com/tonyroumi/cse15l-lab-reports/blob/main/Lab%20Report%203/key%20stored%20on%20git.png?raw=true)

The private key is stored in the same `.ssh` directory under `.ssh/id_rsa`

![image](https://github.com/tonyroumi/cse15l-lab-reports/blob/main/Lab%20Report%203/privatekeylocation.png?raw=true)


We have saved the public key of the remote server to github so we are now able to `add`, `commit`, and `push` on the remote server.


![image](https://github.com/tonyroumi/cse15l-lab-reports/blob/main/Lab%20Report%203/commitworks.png?raw=true)

>As you can see the `git push origin main` works on the server. 
[Here](https://github.com/tonyroumi/markdown-parser/commit/acd6f0480de1038fa5e736380e63e9b9f27e9ccc) is the resulting commit.

___
### Copy whole directories with `scp -r`
To copy the entire markdown-parser directory to the server use the command:
```
scp -r markdown-parser ieng6:~/markdown-parser
```

This is what it looks like when the directory is recursively copied onto the server

![image](https://github.com/tonyroumi/cse15l-lab-reports/blob/main/Lab%20Report%203/copymarkdownparser.png?raw=true)

Now we should be able to run the Junit tests on the server.

![image](https://github.com/tonyroumi/cse15l-lab-reports/blob/main/Lab%20Report%203/junit%20tests%20on%20server.png?raw=true)

We can combine both of these commands for a more effective and faster command line using:
```
scp -r . ieng6:~/lab-report-3 ; ssh ieng6 "cd lab-report-3 ; /software/CSE/oracle-java-17/jdk-17.0.1/bin/javac -cp .:lib/junit-4.13.2.jar:lib/hamcrest-core-1.3.jar MarkdownParseTest.java ; /software/CSE/oracle-java-17/jdk-17.0.1/bin/java -cp .:lib/junit-4.13.2.jar:lib/hamcrest-core-1.3 jar org.junit.runner.JUnitCore MarkdownParseTest"
```
>this is all one line






