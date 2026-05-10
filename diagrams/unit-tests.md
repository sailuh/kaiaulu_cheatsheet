Unit Test Umbrella Issue: [https://github.com/sailuh/kaiaulu/issues/398](https://github.com/sailuh/kaiaulu/issues/398)   
\# Unit Test Process  
Throughout the process of working on the unit tests, multiple cycles of iteration were performed with @carlosparadis. The definition of my types of unit tests and their structure has changed over time. The bulk of my iteration takes place in this issue. [https://github.com/sailuh/kaiaulu/issues/356](https://github.com/sailuh/kaiaulu/issues/356) 

Some table iterations are linked here.   
[https://github.com/sailuh/kaiaulu/issues/356\#issuecomment-3882734656](https://github.com/sailuh/kaiaulu/issues/356#issuecomment-3882734656)   
[https://github.com/sailuh/kaiaulu/issues/356\#issuecomment-3982522790](https://github.com/sailuh/kaiaulu/issues/356#issuecomment-3982522790) 

My final test definitions are below. These are subject to change in the future, but were the furthest I got in defining my types of tests.   
\# Types of Test  
\*\*Third party tools tests\*\* (Third Party Tools)  
Tests that verify if third party tools are specified, and then test if their \-help message is functional  
Ex. \`”testthat given Perceval is specified on tools.yml, when Perceval \--help is called, then it returns the help message”\`

\*\*Raw data edge case tests\*\* (Parser)  
Tests that feed parsers erroneous/odd data with the intent of breaking its functionality  
Ex. \`"testthat when parse\_gitlog is given a ./git folder with a file inside a folder inside another folder, then it will extract the current commit correctly to a data table"\`

\*\*Data structure tests\*\* (Parser, Transform)  
Tests that verify functions return the correct data structure  
Ex. \`"When parse\_gitlog is given a perceval\_path and a ./git folder, then it returns a data table"\`

\*\*Mode/switch tests\*\* (Transforms)  
Tests that verify transform functions filter nodes correctly depending on a specified mode  
Ex. \`"testthat when transform\_gitlog\_to\_bipartite\_network is given a parsed git project and mode, then the type of remaining nodes consist only of those from the mode specified"\`

\*\*Error raising tests\*\* (Parser)  
Tests that verify parsers will not run when given an invalid input.   
These work in conjunction with try catch statements  
Ex. \`"testthat when parse\_gitlog is not given .git/, then an error will be raised"\`

\*\*Expected behavior tests\*\* (All functions)  
Tests that verify a function returned the data it was supposed to  
In the context of transforms/graphs, this is correctly preserving node-edge structure  
In the context of parsers, this is correctly parsing the data from a file  
Ex. \`"testthat when bipartite\_graph\_projection is given a bipartite graph with Author 1 having two connections to File 1 and Author 2 having one connection to File 1, and weight\_scheme\_function \= weight\_scheme\_sum\_edges, and mode \= TRUE, then their returned edge is 4"\`

I have currently implemented some of these types of tests in Pull Requests which pertain to R/git.r, R/src.r, R/mail.R, R/jira.R, and R/graph.R. What I have implemented is definitely not comprehensive, and in their current state, some tests are skipped because they always fail due to them breaking the parsers. The parser edge cases also live in the Example.R file as functions that create fake data for the parsers to be tested. As more Examples will be written with more tests, I think that Example.R should have hashtag dividers splitting the types of fake examples created for parsers in different files. I’ve added these in the JIRA fake examples and mail fake examples, since it’s obvious what data they are for. 

Something important to note is that I did not get to Downloader or Refresher testing, which are relevant in R/mail.R and R/jira.R. 

\# Try Catch  
From my best understanding of Kaiaulu’s codebase, \`\`\`try catches\`\`\` should be implemented in parsers, specifically when they are processing the output of third party tools. Since they trigger specifically from R errors, whenever R reads the raw data stream from these tools, that is when it is the most vulnerable to crashing. I’ve implemented some in the parsers in my Pull Requests. 

I originally thought that the Git Cmd functions would throw an R error if their wrapper fails, but I don’t think this is the case now. I was originally planning to wrap them in try catch statements, but on error it looks like they return only an exit status for their specific line. This means that they shouldn’t be caught by try catch, and instead by checking the exit status produced and printing what it means to the user. 

I wasn’t able to get to doing this, as I ran out of time to work on this project, but this could be something that can be clarified in the future, especially so that future developers working on Example functions can make more sense of the Git errors that are thrown. 

\# Codecov  
This is something that I wasn’t able to get to at all. My issue for it is here.   
[https://github.com/sailuh/kaiaulu/issues/370\#issue-4043055648](https://github.com/sailuh/kaiaulu/issues/370#issue-4043055648)  
This is a tool that utilizes a bot in GitHub Pull Requests to enforce code coverage standards. It does this by feeding the test results from testthat into the covr package, which generates a complete report of each individual line of test coverage. If a certain amount of these lines in newly created code is not tested for, the Codecov bot can automatically deny a Pull Request from a merge, and leave a comment on it.   
