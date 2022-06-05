# **Lab Report 5**
Anthony Roumi <br>
June 5, 2022 

___

_In this lab we will test two different __MarkdownParse__ implementations against two different files with a different output. We expect both implementations to produce different results, that we will see using built in vim command, vimdiff. We will compare the results to the correct output and describe the bug occuring._
___

_First, To find the tests that will produce different results, I first added ```echo $file``` to the loop in ```script.sh``` to output the names of all of the test files with their corresponding results. I then tunneled all of the results into a new file, and used vimdiff to see the differences._
<br>

>[My Implementation (left)](https://github.com/tonyroumi/markdown-parser.git)
<br>
[nidhidhamnani's Implementation(right)](https://github.com/nidhidhamnani/markdown-parser.git)

![image](https://github.com/tonyroumi/cse15l-lab-reports/blob/main/lab%2010/vimdiff481.png?raw=true)

![image](https://github.com/tonyroumi/cse15l-lab-reports/blob/main/lab%2010/vimdiff194.png?raw=true)

_As you can see, [481.md](https://github.com/nidhidhamnani/markdown-parser/blob/main/test-files/481.md) and [194.md](https://github.com/nidhidhamnani/markdown-parser/blob/main/test-files/194.md) both produce different results._


___

### [481.md](https://github.com/nidhidhamnani/markdown-parser/blob/main/test-files/481.md)
The actual output of both implementations:
![image](https://github.com/tonyroumi/cse15l-lab-reports/blob/main/lab%2010/vimdiff481.png?raw=true)

According to [CommonMark](https://spec.commonmark.org/dingus/) the __correct__ output of [481.md](https://github.com/nidhidhamnani/markdown-parser/blob/main/test-files/481.md) should be:

![image](https://github.com/tonyroumi/cse15l-lab-reports/blob/main/lab%2010/correctOutput481.png?raw=true)

__My implementation of MarkdownParse produced the correct results. The output should be an array with '/uri "title"' as the only link.__


The problem with [nidhidhamnani's Implementation](https://github.com/nidhidhamnani/markdown-parser.git) is with this conditional below. The loop will not consider the text as a potential link if a space is found between the parenthesis. The link will not evaulate to true in this conditional and therefore will be ignored. A simple fix would be to remove this conditional. 

![image](https://github.com/tonyroumi/cse15l-lab-reports/blob/main/lab%2010/problemwith481.png?raw=true)

<br>

### [194.md](https://github.com/nidhidhamnani/markdown-parser/blob/main/test-files/194.md)
The actual output of both implementations:
![image](https://github.com/tonyroumi/cse15l-lab-reports/blob/main/lab%2010/vimdiff194.png?raw=true)

According to [CommonMark](https://spec.commonmark.org/dingus/) the __correct__ output of [194.md](https://github.com/nidhidhamnani/markdown-parser/blob/main/test-files/194.md) should be:

![image](https://github.com/tonyroumi/cse15l-lab-reports/blob/main/lab%2010/correctOutput194.png?raw=true)

__My implementation of MarkdownParse produced the correct results. The output should be an empty array, whereas nidhidhamnani's Implementation includes 'url' as a link.__


The problem with [nidhidhamnani's Implementation](https://github.com/nidhidhamnani/markdown-parser.git) is that it does not check wether or not the open parenthesis is next to the closed bracket. This implementation will always produce a link as long as a closed bracket and open parenthesis exist in the file, which is not a correct implementation of a markdown parser. A simple fix would be to check if the closed bracket and open parenthesis are next to each other. 

![image](https://github.com/tonyroumi/cse15l-lab-reports/blob/main/lab%2010/problemwith194.png?raw=true)

