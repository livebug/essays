# Antlt4

## Install  ANTLR v4 on unix
+ Install Java (version 1.7 or higher)
Download
    $ cd /usr/local/lib
    $ curl -O https://www.antlr.org/download/antlr-4.9-complete.jar
Or just download in browser from website: https://www.antlr.org/download.html and put it somewhere rational like /usr/local/lib.

+ Add antlr-4.9-complete.jar to your CLASSPATH:
    $ export CLASSPATH=".:/usr/local/lib/antlr-4.9-complete.jar:$CLASSPATH"
It's also a good idea to put this in your .bash_profile or whatever your startup script is.

+ Create aliases for the ANTLR Tool, and TestRig.
    $ alias antlr4='java -Xmx500M -cp "/usr/local/lib/antlr-4.9-complete.jar:$CLASSPATH" org.antlr.v4.Tool'
    $ alias grun='java -Xmx500M -cp "/usr/local/lib/antlr-4.9-complete.jar:$CLASSPATH" org.antlr.v4.gui.TestRig'

## antlr4 安装 2

不多说先放地址 https://github.com/antlr/antlr4/blob/master/doc/getting-started.md

```bash
$ cd /usr/local/lib
$ curl -O https://www.antlr.org/download/antlr-4.9-complete.jar
# 后面的写到 .bashrc 中
$ export CLASSPATH=".:/usr/local/lib/antlr-4.9-complete.jar:$CLASSPATH"
$ alias antlr4='java -Xmx500M -cp "/usr/local/lib/antlr-4.9-complete.jar:$CLASSPATH" org.antlr.v4.Tool'
$ alias grun='java -Xmx500M -cp "/usr/local/lib/antlr-4.9-complete.jar:$CLASSPATH" org.antlr.v4.gui.TestRig'
```

## Book source code
The book has lots and lots of examples that should be useful too. You can download them here for free:

http://pragprog.com/titles/tpantlr2/source_code

Also, there is a large collection of grammars for v4 at github:

https://github.com/antlr/grammars-v4/

## 编译

```bash
 antlr4 -lib ./  HiveLexer.g4  -o csharp -Dlanguage=CSharp -visitor -package Hive.V3
 antlr4 -lib ./ HiveParser.g4 -o csharp -Dlanguage=CSharp  -visitor -package Hive.V3
 antlr4 -lib ./ HiveParser.g4 -o csharp -Dlanguage=CSharp  -visitor -package Hive.V3
 antlr4 -lib ./ HiveParser.g4 -o csharp -Dlanguage=CSharp  -visitor -package Hive.V3
 antlr4 -lib ./ HiveParser.g4 -o csharp -Dlanguage=CSharp  -visitor -package Hive.V3
```

 antlr4 -lib ./ HiveLexer.g4            -o csharp -Dlanguage=CSharp  -visitor -package Hive.V3
 antlr4 -lib ./ IdentifiersParser.g4    -o csharp -Dlanguage=CSharp  -visitor -package Hive.V3
 antlr4 -lib ./ HintParser.g4           -o csharp -Dlanguage=CSharp  -visitor -package Hive.V3
 antlr4 -lib ./ SelectClauseParser.g4   -o csharp -Dlanguage=CSharp  -visitor -package Hive.V3
 antlr4 -lib ./ FromClauseParser.g4     -o csharp -Dlanguage=CSharp  -visitor -package Hive.V3
 antlr4 -lib ./ HiveParser.g4           -o csharp -Dlanguage=CSharp  -visitor -package Hive.V3
 antlr4 -lib ./ ResourcePlanParser.g4   -o csharp -Dlanguage=CSharp  -visitor -package Hive.V3