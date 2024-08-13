# Servlet

## What is a Servlet
A Servlet is a java class that allow us to manage the request/response cycle of web applications. It acts as a handler between the client requests and the server response.

 It runs inside a container -Servlet Container- which provides the runtime environment for Java EE. This container usually is part of the web add server, but it can run separately too.

  There are **three types of Servlet Containers**:
  
  - __Standalone__: The container and the server are integral parts of the web application: *tomcat running by itself.*
  
  - __In-process__: The container is separated from the server as there is another program using the main address of the server: *tomcat running inside JBoss.*
  
  - __Out-process__: The container run in a separated process from the server, but there can be communication between them if the server uses the plug-in provided by the container.

## How to implement it

There are two classes that allow us to inherit and create our own Servlet: 
*GenericServlet*, __HttpServlet__.

```java
import java.io.IOException;
import java.io.PrintWriter;
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

public class Welcome extends HttpServlet {
    protected void doGet(HttpServletRequest request, HttpServletResponse response)
            throws ServletException, IOException {
        response.setContentType("text/html");
        PrintWriter out = response.getWriter();
        out.println("<HTML>");
        out.println("<HEAD>");
        out.println("<TITLE>Welcome</TITLE>");
        out.println("</HEAD>");
        out.println("<BODY>");
        out.println("<h1>ServEx_1: Hello</h1>");
        out.println("<p>Hello user, welcome to the welcome servlet!</p>");
        out.println("</BODY>");
        out.println("</HTML>");
    }
}
```