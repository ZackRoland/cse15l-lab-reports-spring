#**cd command**
---
1. No Args
   ```
   zroland@its-cseb260-07 MINGW64 ~/lecture1 (main)
   $ cd
   
   ```
   > The absolute path is /Users/zackroland/lecture1, cd returns us to the home directory. This is not an error
   > since cd changes the directory to whathever directory is given as an argument and
   > without any arguments the directory will be changed to the home directory as default. The absolute path
   > after the command is run is /Users/zackroland
2. Directory Arg
   ```
    zroland@its-cseb260-07 MINGW64 ~
    $ cd lecture1/
    
    zroland@its-cseb260-07 MINGW64 ~/lecture1 (main)
    $
   ```
   > The absolute path is /Users/zackroland, cd with the lecture1 directory as the argument will
   > change the directory to the lecture1 directory as shown in the line preceeding the command.
   > The absolute path aftweards will be /Users/zackroland/lecture1. This is not an error since this follows the
   > functionality of the cd command, changing the directory to whatever directory that is given as input.
3. File Arg
   ```
    zroland@its-cseb260-07 MINGW64 ~/lecture1 (main)
    $ cd messages/en-us.txt 
    bash: cd: messages/en-us.txt: Not a directory

   ```
   > The absolute path is /Users/zackroland/lecture1 cd with the file path to en-us.txt returns a message "Not
   > a directory.? This is indeed an error since the only inputs cd can take as argument are either no input or
   > a directory path, so when a file path is given an error message is displayed. The absolute path afterwards
   > is the same.

#**ls command**
---
1. No Args
   ```
    zroland@its-cseb260-07 MINGW64 ~/lecture1 (main)
    $ ls
    Hello.class  Hello.java  messages/  README
   ```
   > The absolute path is /Users/zackroland/lecture1, calling ls with no arguments returns all the files that are
   > within the lecture1 directory. This is not an error since ls displays all the files within the argument
   > directory/file paths and if no argument is given as input it just returns all the files within the current
   > directory.
2. Directory Arg
   ```
    zroland@its-cseb260-07 MINGW64 ~/lecture1 (main)
    $ ls messages/
    en-us.txt  es-mx.txt  jp.txt  zh-cn.txt
   ```
   > The absolute path is /Users/zackroland/lecture1, calling ls with the message directory as an argument returns
   > all the files within the message directory. This is not an error since this follows the functionality of the
   > ls command to return all the files within a directory or file path if given it as an argument.
3. File Arg
   ```
    zroland@its-cseb260-07 MINGW64 ~/lecture1 (main)
    $ ls messages/en-us.txt 
    messages/en-us.txt
   ```
   > The absolute path is /Users/zackroland/lecture1, calling ls with the file path returns the path back to you.
   > This is not an error since what ls does as its function is return all the files within a given path and if a
   > file is given as the path that would be the only path possible since a file can only hold itself since it
   > not a directory. Therefore it subsequently returns the path to the file which is not an output done in error.
   
#**cat command**
---
1. No Args
   ```
    zroland@its-cseb260-07 MINGW64 ~/lecture1 (main)
    $ cat





   ```
   > The absolute path is /Users/zackroland/lecture1. Calling cat without any argument just returns
   > nothing no matter how many times you press enter. This is not an error, this follows the direct functionality of
   > the cat function. It is supposed to read the contents of whatever file it is given as an argument and if
   > no file is given as an arguement it doesn't know what to do and subsequently just waits till a file path is given.
2. Directory Arg
   ```
    zroland@its-cseb260-07 MINGW64 ~/lecture1 (main)
    $ cat messages/
    cat: messages/: Is a directory
   ```
   > The absolute path is /Users/zackroland/lecture1. Calling cat with the message directory as its argument returns
   > a output of "Is a directory". This is an error since the function of cat is to read the contents of files and
   > since a directory is just a folder that holds the files, if a file path is not called there would be nothing to
   > read since a folder on its own does not contain any information.
3. File Arg
   ```
    zroland@its-cseb260-07 MINGW64 ~/lecture1 (main)
    $ cat messages/en-us.txt 
    Hello World!
   ```
   > The absolute path is /Users/zackroland/lecture1. Calling cat with the file as an argument returns the content
   > of the file which in this case is Hello World!. This is not an error since this follows the direct funtionality
   > of the cat command since it is supposed to take in a file as an argument and print out the contents of the file
   > in the terminal and it does exactly that.
