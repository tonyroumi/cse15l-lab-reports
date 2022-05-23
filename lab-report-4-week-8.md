# **Lab Report 4**
Anthony Roumi <br>
May 22, 2022 

---
_These past two weeks we have learned a variety of clean coding techniques. It is important to maintain a clear and legible coding environment to produce the best results. We have learned about the unix VIM editor to make edits to files only using the command line. We also learned how to debug code using java's built-in debugger (JDB). This debugger allows us to track the stack and local variables line by line, giving us a more comprehensive breakdown of the error._

___
_In this lab we will test three different types of tests against two different implementations of __MarkdownParse__._

- My Implementation: [MarkdownParse](https://github.com/tonyroumi/markdown-parser.git)

- Week 7 implementation: [MarkdownParse](https://github.com/ujik500/markdown-parser.git)

>I will use [Commonmark](https://spec.commonmark.org/dingus/) to find the correct expected output of __MarkdownParse__. 

___
### __Test #1__
```
`[a link`](url.com)
[another link](`google.com)`
[`cod[e`](google.com)
[`code]`](ucsd.edu)
```


The correct output for _Test #1_ should be: 
```
[`google.com, google.com, ucsd.edu]
```

This is the code for the Junit test #1 that I will run on both implementations in __MarkdownParseTest__:

![image](https://github.com/tonyroumi/cse15l-lab-reports/blob/main/Lab%20Report%204/markdowntest-test1.png?raw=true)

This is the output for __my implementation__:

![image](https://github.com/tonyroumi/cse15l-lab-reports/blob/main/Lab%20Report%204/test1-mine.png?raw=true)

>As you can see my implementation of __MarkdownParse__ failed _test #1_ and outputs the incorrect parsed list.


This is the output for the __week 7 implementation__:

![image](https://github.com/tonyroumi/cse15l-lab-reports/blob/main/Lab%20Report%204/test1-week7.png?raw=true)

>As you can see the week 7 implementation of __MarkdownParse__ failed _test #1_ and outputs the incorrect parsed list. 

<br>


_1.)_ __Do you think there is a small (<10 lines) code change that will make your program work for snippet 1 and all related cases that use inline code with backticks? If yes, describe the code change. If not, describe why it would be a more involved change.__


There is a small (<10 lines), simple solution to inline code with backticks. We can create a variable that will track the index of all backticks. If there is a backtick before the open bracket and another backtick to close it off, then ignore it.

### __Test #2__
```
[a [nested link](a.com)](b.com)
[a nested parenthesized url](a.com(()))
[some escaped \[ brackets \]](example.com)
```

The correct output for _Test #2_ should be: 
```
[a.com, a.com(()), example.com]
```

This is the code for the Junit test #2 that I will run on both implementations in __MarkdownParseTest__:

![image](https://github.com/tonyroumi/cse15l-lab-reports/blob/main/Lab%20Report%204/markdowntest-test2.png?raw=true)

This is the output for __my implementation__:

![image](https://github.com/tonyroumi/cse15l-lab-reports/blob/main/Lab%20Report%204/test2-mine.png?raw=true)

>As you can see my implementation of __MarkdownParse__ failed _test #2_ and outputs the incorrect parsed list.


This is the output for the __week 7 implementation__:

![image](https://github.com/tonyroumi/cse15l-lab-reports/blob/main/Lab%20Report%204/test2-week7.png?raw=true)

>As you can see the week 7 implementation of __MarkdownParse__ failed _test #2_ and outputs the incorrect parsed list. 

<br>

_2.)_ __Do you think there is a small (<10 lines) code change that will make your program work for snippet 2 and all related cases that nest parentheses, brackets, and escaped brackets? If yes, describe the code change. If not, describe why it would be a more involved change.__

I am not sure if this is possible in 10 lines of code or less, but , a solution to nest parentheses and brackets would be to create a variable that will track the index of open and close parenthesis once an open bracket is found. If a URL is inside two parenthesis after an open bracket is found, then append, and continue parsing once the closed paranethsis is found. 


### __Test #3__
```
[this title text is really long and takes up more than 
one line
and has some line breaks](
    https://www.twitter.com
)
[this title text is really long and takes up more than 
one line](
https://sites.google.com/eng.ucsd.edu/cse-15l-spring-2022/schedule
)
[this link doesn't have a closing parenthesis](github.com
And there's still some more text after that.
[this link doesn't have a closing parenthesis for a while](https://cse.ucsd.edu/
)
And then there's more text
```
The correct output for _Test #2_ should be: 
```
[https://sites.google.com/eng.ucsd.edu/cse-15l-spring-2022/schedule]
```

This is the code for the Junit test #3 that I will run on both implementations in __MarkdownParseTest__:

![image](https://github.com/tonyroumi/cse15l-lab-reports/blob/main/Lab%20Report%204/markdowntest-test3.png?raw=true)

This is the output for __my implementation__:

![image](https://github.com/tonyroumi/cse15l-lab-reports/blob/main/Lab%20Report%204/test3-mine.png?raw=true)

>As you can see my implementation of __MarkdownParse__ failed _test #3_ and outputs the incorrect parsed list.


This is the output for the __week 7 implementation__:

![image](https://github.com/tonyroumi/cse15l-lab-reports/blob/main/Lab%20Report%204/test3-week7.png?raw=true)

>As you can see the week 7 implementation of __MarkdownParse__ failed _test #3_ and outputs the incorrect parsed list. 

<br>

_3.)_ __Do you think there is a small (<10 lines) code change that will make your program work for snippet 3 and all related cases that have newlines in brackets and parentheses? If yes, describe the code change. If not, describe why it would be a more involved change.__

Yes, a small (<10 lines) solution to newlines in brackets and parentheses would be to create a conditional that checks for newlines and spaces immediately after the open paranthesis, if there is space, then ignore the URL. 






