# Lab Report 5
## Part 1

![Image](/lab5images/l5symp.png)

Student: I was working on an autograde bash script from lab 6, however I keep running into a weird situation where I get the message posted above whenever I run the command `bash grade.sh https://github.com/ucsd-cse15l-f22/list-methods-compile-error`. I'm not sure why I'm getting this output as I made sure to copy over the `lib` files with `-r`, and still I run into the situation where I cannot progress further. Could I get some help here?

TA: Have you tried providing the absolute path to the files? If that does not help, see if you made sure to copy the `lib` directory rather than just the files.

![Image](/lab5images/l5symp2.png)

Student: Thank you for your help, it turns out the bug was not copying the lib directory over; I was just copying its contents instead. With that said, I've run into a new error where it gives me a "Compilation successful" message when the provided directory is intended to run into a compilation error. 

TA: You may want to revisit how you check whether you have a compilation error or not. For example, what exit code should you be checking for?

![Image](/lab5images/l5sol.png)

Student: That helped! I forgot I should be checking for 0, which indicates success, and instead I had it checking for code 1, which indicates failure. Now my bash script runs perfectly fine!

### Information relevant for setup:
#### File & Directory Structure:

![Image](/lab5images/l5struct.png)

#### Contents of Files before fixing the bugs:
grade.sh:
```java
set -e
CPATH='.:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar'
JNIT='org.junit.runner.JUnitCore'

rm -rf student-submission
rm -rf grading-area

mkdir grading-area

git clone $1 student-submission
echo 'Finished cloning'

# Draw a picture/take notes on the directory structure that's set up after
# getting to this point

# Then, add here code to compile and run, and do any post-processing of the
# tests

if [[ -f student-submission/ListExamples.java ]]
then
    echo 'File found!'
    cp -r student-submission/ListExamples.java grading-area/
    cp -r TestListExamples.java grading-area/
    cp -r lib/ grading-area/
else
    echo 'File not found!'
    exit 1
fi

cd grading-area
set +e
javac -cp $CPATH ListExamples.java TestListExamples.java 2> error_log.txt
if [ $? == 1 ]
then
    echo 'Compilation successful!!'
    
else
    echo 'Compilation failed'
    exit 1
    
fi

java -cp $CPATH org.junit.runner.JUnitCore TestListExamples > test_results.txt

PASS=`grep -o OK test_results.txt`
FAILED=`grep -o FAILURES test_results.txt`

if [[ $PASS == "OK" ]]
then 
    echo 'Full Credit, good work!'
fi 
if [[ $FAILED == "FAILURES" ]]
then 
    echo 'Not full credit'
fi
```

GradeServer.java:
```java
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

Server.java:
```java
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

TestListExamples.java:
```java
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

#### Command to trigger bugs:

`bash grade.sh https://github.com/ucsd-cse15l-f22/list-methods-compile-error`

#### Fixes:
First I changed line 24 (`cp -r lib/ grading-area/`) to `cp -r lib grading-area/`. Then I changed line 33 (`if [ $? == 1 ]`) to `if [ $? == 0 ]`.


***

## Part 2
One very interesting thing I found out about was pertaining Github. I was introduced to Github and how to push/pull from it in one of my prior classes, however I never learned how to connect it to VS Code, which in turn made things a lot more difficult to work with and further having a fear towards it. So with finding out about Github desktop, it became a lot more easier to deal with Git and Github, making things much more organized than previously from directly using the terminal.
