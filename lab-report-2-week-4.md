# **Lab Report 2**
Anthony Roumi <br>
April 24, 2022 

---
## Testing your code
_These past two weeks we have learned a variety of debugging and testing procedures. We have learned about new lines of development in github, as well as better ways of approaching and testing code._

## _Markdown Parsing_
_Last week we learned about markdown parsing. We were given a program that takes a markdown file as a command line argument and then prints out all the URLs of the links (but not of images) in that file and asked to debug the code._

_The parsing comes from obtaining a data structure out of a string._

## _Testing and Code Changes_
_We ran different inputs to test the code and insure that there are no symptoms or bugs._

---
## __Bug #1__
The first __bug__ that I encountered was when there were two links in the markdown file: ['test-file2'](https://github.com/tonyroumi/markdown-parser/blob/main/test-file2.md)

This __bug__ caused an infinite loop which resulted in an ```OutOFMemoryError```:

![image](https://github.com/tonyroumi/cse15l-lab-reports/blob/main/Lab%20Report%202%20screenshots/Screen%20Shot%202022-04-25%20at%205.30.12%20PM.png?raw=true)

This is the code change difference that resolved the __bug__:
![image](https://github.com/tonyroumi/cse15l-lab-reports/blob/main/Lab%20Report%202%20screenshots/changes%20to%20code%20for%20test%202.png?raw=true)

Write 2-3 sentences here

## __Bug #2__
The second __symptom__ that I encountered was when there was an image in the markdown file: ['test-file3'](https://github.com/tonyroumi/markdown-parser/blob/main/test-file3.md)

This __symptom__ would create a list including the image link, which is not apart of the program:

![image](https://github.com/tonyroumi/cse15l-lab-reports/blob/main/Lab%20Report%202%20screenshots/Screen%20Shot%202022-04-25%20at%205.50.12%20PM.png?raw=true)

This is the code change difference that resolved the __symptom__:
![image](https://github.com/tonyroumi/cse15l-lab-reports/blob/main/Lab%20Report%202%20screenshots/test-file%203%20diff.png?raw=true)

Write 2-3 sentences here

## __Bug #3__
The third __bug__ that I encountered was when a plain string and singular open bracket was in the markdown file: ['test-file4'](https://github.com/tonyroumi/markdown-parser/blob/main/test-file4.md)

This __bug__ caused a ```StringIndexOutOfBoundsException```:
![image](https://github.com/tonyroumi/cse15l-lab-reports/blob/main/Lab%20Report%202%20screenshots/test-file4.png?raw=true)

This is the code change difference that resolved the bug:
![image](https://github.com/tonyroumi/cse15l-lab-reports/blob/main/Lab%20Report%202%20screenshots/file4%20fix.png?raw=true)

write 2-3 sentences here

