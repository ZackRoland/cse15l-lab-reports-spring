## **PART 1:**
---

> Student: Hi i am encountering an error when trying to run my grade.sh bash script for
> list-examples-grader and was wondering if I could get help debugging it. Provided is a
> screenshot of the terminal error output when running the bash script.
![Error](https://i.postimg.cc/Lsfv1LJD/Inital-Error.png)
> TA: It's hard to figure out exactly what is causing the error without having the code to the
> bash script provided, but the error output can provide us with some useful information on
> trying to pin down the root of the issue. It seems like the bash script is running fine
> up until the point where you echoed “The java files compiled successfully” and it seems
> like the error is isolated around that point since “Grade: 0” is being echoed after the
> error message is being displayed. Please attach a screenshot of your code and I will be
> able to provide additional assistance.

> Student: Heres the screenshots of my code
![First half](https://i.postimg.cc/Bvxc63zw/Screenshot-2024-06-05-at-6-44-06-PM.png)
![Second half](https://i.postimg.cc/D0mXq3Ch/Screenshot-2024-06-05-at-6-25-23-PM.png)

> TA: I think I have identified the issue, on line 36 it's almost correct but you are
> forgetting something key. Back in lab 4 I believe we went over the commands to run
> junit tests via the terminal.
```
javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar *.java
java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore ArrayTests
```
> What is it that is missing from your line 36?

> Student: I’ve figured it out, was missing “org.junit.runner.JUnitCore” so when I had put that in
> and reran my bash script, everything ran smoothly
![Fixed Code](https://i.postimg.cc/HWJ0cbFy/Screenshot-2024-06-05-at-6-26-07-PM.png)
![Correct Terminal Output](https://i.postimg.cc/50XzzMKV/Screenshot-2024-06-05-at-6-26-37-PM.png)
## **PART 2:**
---
