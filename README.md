# Java 18

## Useful Links

### Podcast link and JEPs it talks about

[Episode 23 "Java 18 is Here!"](https://inside.java/2022/03/22/podcast-023/)  
Spotify - Inside Java - [Podcast Episode "Java 18 is Here!"](https://open.spotify.com/episode/1JCGSs0ZUC8PTRUYZvaZ5F)  
[JEP 400](https://openjdk.org/jeps/400) - UTF-8 by Default  
[JEP 408](https://openjdk.org/jeps/408) - Simple Web Server  
[JEP 413](https://openjdk.org/jeps/413) - Code Snippets in Java API Documentation  
[JEP 421](https://openjdk.org/jeps/421) - Deprecate Finalization for Removal  

### Other Links

[Inside Java Website](https://inside.java/)  
[Executable JavaDoc Code Snippets](https://www.morling.dev/blog/executable-javadoc-code-snippets/)  
[Inside Java - Episode 22 “JEP 408 - Simple Web Server”](https://inside.java/2022/03/04/podcast-022/)  
[Java 18’s Simple Web Server: A tool for the command line and beyond](https://blogs.oracle.com/javamagazine/post/java-18-simple-web-server)  
[Working with the Simple Web Server](https://inside.java/2021/12/06/working-with-the-simple-web-server/)  

### List of JEPs

[Link with all JEPs](https://openjdk.org/projects/jdk/18/)  

```
400:	UTF-8 by Default
408:	Simple Web Server
413:	Code Snippets in Java API Documentation
416:	Reimplement Core Reflection with Method Handles
417:	Vector API (Third Incubator)
418:	Internet-Address Resolution SPI
419:	Foreign Function & Memory API (Second Incubator)
420:	Pattern Matching for switch (Second Preview)
421:	Deprecate Finalization for Removal
```

### Use Simple Web Server via command line

<code>./jwebserver -d /c/test -o verbose</code>

### Use Simple Web Server programmatically

```java
package org.example;

import com.sun.net.httpserver.*;

import java.io.IOException;
import java.net.InetSocketAddress;
import java.nio.file.Files;
import java.nio.file.Path;
import java.util.function.Predicate;

public class SimpleWebServerDemo {

  public static void main(String[] args) throws IOException {
    Predicate<Request> IS_GET = r -> r.getRequestMethod().equals("GET");
    var jsonHandler = HttpHandlers.of(200, Headers.of("Content-Type", "application/json"),
        Files.readString(Path.of("C:/test/todos.json")));
    var notAllowedHandler = HttpHandlers.of(405, Headers.of("Allow", "GET"), "");
    var handler = HttpHandlers.handleOrElse(IS_GET, jsonHandler, notAllowedHandler);

    var server = HttpServer.create(new InetSocketAddress(8080),10, "/somecontext/", handler);
    server.start();
    System.out.println("Server started");
    // After running this code you can access http://127.0.0.1:8080/somecontext/ in the browser
  }

}
```
