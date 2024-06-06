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

# Setup Information:
1. File and Directory Structure: The file and directory structure should be followed
   from lab 6's list-examples-grader since that is where the bash script the student
   is running lies. Would Look like the following after running the script:
   ![File Structure](https://i.postimg.cc/kXg2RC2h/Screenshot-2024-06-05-at-7-32-46-PM.png)
2. Contents of each file before fixing the bug:
```
ListExamples.java:
import java.util.ArrayList;
import java.util.List;

interface StringChecker { boolean checkString(String s); }

class ListExamples {

  // Returns a new list that has all the elements of the input list for which
  // the StringChecker returns true, and not the elements that return false, in
  // the same order they appeared in the input list;
  static List<String> filter(List<String> list, StringChecker sc) {
    List<String> result = new ArrayList<>();
    for(String s: list) {
      if(sc.checkString(s)) {
        result.add(0, s);
      }
    }
    return result;
  }


  // Takes two sorted list of strings (so "a" appears before "b" and so on),
  // and return a new list that has all the strings in both list in sorted order.
  static List<String> merge(List<String> list1, List<String> list2) {
    List<String> result = new ArrayList<>();
    int index1 = 0, index2 = 0;
    while(index1 < list1.size() && index2 < list2.size()) {
      if(list1.get(index1).compareTo(list2.get(index2)) < 0) {
        result.add(list1.get(index1));
        index1 += 1;
      }
      else {
        result.add(list2.get(index2));
        index2 += 1;
      }
    }
    while(index1 < list1.size()) {
      result.add(list1.get(index1));
      index1 += 1;
    }
    while(index2 < list2.size()) {
      result.add(list2.get(index2));
      index1 += 1;
    }
    return result;
  }


}
```
```
grade.sh:
CPATH='.:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar'

rm -rf student-submission
rm -rf grading-area

mkdir grading-area

git clone $1 student-submission
echo 'Finished cloning'


# Draw a picture/take notes on the directory structure that's set up after
# getting to this point

# Then, add here code to compile and run, and do any post-processing of the
# tests
#STEP 2:
if [[ -f student-submission/ListExamples.java ]]
then
	echo "ListExamples.java file found."
else
	echo "ListExamples.java file not found."
	echo "Grade: 0"
	exit
fi
#STEP 3:
cp TestListExamples.java student-submission/ListExamples.java grading-area
cp -r lib grading-area
#STEP 4:
cd grading-area
javac -cp $CPATH *.java

if [[ $? -eq 0 ]]
then
	echo "The java files compiled successfully."
	java -cp $CPATH TestListExamples > results.txt
	grep -q 'Failures' results.txt
	if [[ $? -eq 0 ]]
	then
		echo "Grade: pass"
	else
		echo "Grade: 0"
	fi
		
else 
	echo "The java files compiled unsucessfully."
fi
#STEP 5:
#echo "'$?'"
```
```
TestListExamples.java:
import static org.junit.Assert.*;
import org.junit.*;
import java.util.Arrays;
import java.util.List;

class IsMoon implements StringChecker {
  public boolean checkString(String s) {
    return s.equalsIgnoreCase("moon");
  }
}

public class TestListExamples {
  @Test(timeout = 500)
  public void testMergeRightEnd() {
    List<String> left = Arrays.asList("a", "b", "c");
    List<String> right = Arrays.asList("a", "d");
    List<String> merged = ListExamples.merge(left, right);
    List<String> expected = Arrays.asList("a", "a", "b", "c", "d");
    assertEquals(expected, merged);
  }
}
```
```
Server.java:
// A simple web server using Java's built-in HttpServer

// Examples from https://dzone.com/articles/simple-http-server-in-java were useful references

import java.io.IOException;
import java.io.OutputStream;
import java.net.InetSocketAddress;
import java.net.URI;

import com.sun.net.httpserver.HttpExchange;
import com.sun.net.httpserver.HttpHandler;
import com.sun.net.httpserver.HttpServer;

interface URLHandler {
    String handleRequest(URI url) throws IOException;
}

class ServerHttpHandler implements HttpHandler {
    URLHandler handler;
    ServerHttpHandler(URLHandler handler) {
      this.handler = handler;
    }
    public void handle(final HttpExchange exchange) throws IOException {
        // form return body after being handled by program
        try {
            String ret = handler.handleRequest(exchange.getRequestURI());
            // form the return string and write it on the browser
            exchange.sendResponseHeaders(200, ret.getBytes().length);
            OutputStream os = exchange.getResponseBody();
            os.write(ret.getBytes());
            os.close();
        } catch(Exception e) {
            String response = e.toString();
            exchange.sendResponseHeaders(500, response.getBytes().length);
            OutputStream os = exchange.getResponseBody();
            os.write(response.getBytes());
            os.close();
        }
    }
}

public class Server {
    public static void start(int port, URLHandler handler) throws IOException {
        HttpServer server = HttpServer.create(new InetSocketAddress(port), 0);

        //create request entrypoint
        server.createContext("/", new ServerHttpHandler(handler));

        //start the server
        server.start();
        System.out.println("Server Started! Visit http://localhost:" + port + " to visit.");
    }
}
```
```
GradeServer.java:
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStream;
import java.io.InputStreamReader;
import java.net.URI;
import java.net.URISyntaxException;
import java.util.Arrays;
import java.util.stream.Stream;

class ExecHelpers {

  /**
    Takes an input stream, reads the full stream, and returns the result as a
    string.

    In Java 9 and later, new String(out.readAllBytes()) would be a better
    option, but using Java 8 for compatibility with ieng6.
  */
  static String streamToString(InputStream out) throws IOException {
    String result = "";
    while(true) {
      int c = out.read();
      if(c == -1) { break; }
      result += (char)c;
    }
    return result;
  }

  /**
    Takes a command, represented as an array of strings as it would by typed at
    the command line, runs it, and returns its combined stdout and stderr as a
    string.
  */
  static String exec(String[] cmd) throws IOException {
    Process p = new ProcessBuilder()
                    .command(Arrays.asList(cmd))
                    .redirectErrorStream(true)
                    .start();
    InputStream outputOfBash = p.getInputStream();
    return String.format("%s\n", streamToString(outputOfBash));
  }

}

class Handler implements URLHandler {
    public String handleRequest(URI url) throws IOException {
       if (url.getPath().equals("/grade")) {
           String[] parameters = url.getQuery().split("=");
           if (parameters[0].equals("repo")) {
               String[] cmd = {"bash", "grade.sh", parameters[1]};
               String result = ExecHelpers.exec(cmd);
               return result;
           }
           else {
               return "Couldn't find query parameter repo";
           }
       }
       else {
           return "Don't know how to handle that path!";
       }
    }
}

class GradeServer {
    public static void main(String[] args) throws IOException {
        if(args.length == 0){
            System.out.println("Missing port number! Try any number between 1024 to 49151");
            return;
        }

        int port = Integer.parseInt(args[0]);

        Server.start(port, new Handler());
    }
}

class ExecExamples {
  public static void main(String[] args) throws IOException {
    String[] cmd1 = {"ls", "lib"};
    System.out.println(ExecHelpers.exec(cmd1));

    String[] cmd2 = {"pwd"};
    System.out.println(ExecHelpers.exec(cmd2));

    String[] cmd3 = {"touch", "a-new-file.txt"};
    System.out.println(ExecHelpers.exec(cmd3));
  }
}

```
3. Command line to trigger bug:
```
bash grade.sh https://github.com/ucsd-cse15l-f22/list-methods-lab3
```
4. Description of edit to fix bug:
> Student needed to fix in line 36 of grade.sh the java compilation command since
> they had forgotten the org.junit.runner.JUnitCore

## **PART 2:**
---
> This quarter was much better than last for me and was able to learn a lot from cse15l
> this time around. Something cool in the second half of the quarter I learned is how
> to debug using jdb and more recently today how to debug using VSCode instead. I find
> it interesting to learn the various ways in which software development is done in the
> industry setting since that is the path that I want to venture on in the future. I
> think that being able hone in on specific skill sets would make you a more desriable
> candidate for job offers which is why its important these basics are ground into us.
