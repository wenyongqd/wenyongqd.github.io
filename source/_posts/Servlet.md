---
title: Servlet
subtitle: "\"“A successful man is one who can lay a firm foundation with the bricks others have thrown at him.”— David Brinkley \""

date: 2020-03-19 21:29:21
tags: 
    - Servlet
---
![image](https://miro.medium.com/max/9792/1*c6Lw3mIePawaWKRV7c7K_Q.jpeg)
> “Five years from now you will arrive, the question is where?” — Jim Rohn

>‘Spend each day trying to be a little wiser than you were when you woke up. Discharge your duties faithfully and well. Step by step you get ahead, but not necessarily in fast spurts. But you build discipline by preparing for fast spurts… Slug it out one inch at a time, day by day, at the end of the day — if you live long enough — most people get what they deserve.’

## Servlet

- **Concept**：Servlets are Java programs that runs inside a Java-capable HTTP server.

    - Java servlets typically run on the HTTP protocol. HTTP is an asymmetrical request-response protocol.
- **Quick Start**：
    1. Create a JavaEE program
    2. Write a Java Servlet which extends Servlet Interface.
    3. Implement the abstract methods in Servlet Interface
    4. Configure the Application Deployment Descriptor - "web.xml"

## First "Hello-world" Servlet
---
#### Write a Hello-world Java Servlet - "HelloServlet.java"
```java
package cn.itcast.web.servlet;

import java.io.*;
import javax.servlet.*;
import javax.servlet.http.*;

public class HelloServlet extends HttpServlet {
    @Override
    public void doGet(HttpServletRequest request, HttpServletResponse response)
            throws IOException, ServletException {
        // Set the response message's MIME type
        response.setContentType("text/html;charset=UTF-8");
        // Allocate a output writer to write the response message into the network socket
        PrintWriter out = response.getWriter();

        // Write the response message, in an HTML page
        try {
            out.println("<!DOCTYPE html>");
            out.println("<html><head>");
            out.println("<meta http-equiv='Content-Type' content='text/html; charset=UTF-8'>");
            out.println("<title>Hello, World</title></head>");
            out.println("<body>");
            out.println("<h1>Hello, world!</h1>");  // says Hello
            // Echo client's request information
            out.println("<p>Request URI: " + request.getRequestURI() + "</p>");
            out.println("<p>Protocol: " + request.getProtocol() + "</p>");
            out.println("<p>PathInfo: " + request.getPathInfo() + "</p>");
            out.println("<p>Remote Address: " + request.getRemoteAddr() + "</p>");
            // Generate a random number upon each request
            out.println("<p>A Random Number: <strong>" + Math.random() + "</strong></p>");
            out.println("</body>");
            out.println("</html>");
        } finally {
            out.close();  // Always close the output writer
        }
    }
}


```

- As mentioned, a servlet is invoked in response to a request URL issued by a client. Specifically, a client issues an HTTP request, the server routes the request message to the servlet for processing. The servlet returns a response message to the client.
- An HTTP request could use either `GET` or `POST` request methods, which will be processed by the servlet's `doGet()` or `doPost()` method, respectively.
- In the HelloServlet, we override the `doGet()` method (as denoted by the annotation @Override). The doGet() runs in response to an HTTP GET request issued by a user via an URL. doGet() takes two arguments, an `HttpServletRequest` object and an `HttpServletResponse` object, corresponding to the request and response messages.
- The `HttpServletRequest` object can be used to retrieve incoming **HTTP request headers** and **form data**. `The HttpServletResponse` object can be used to set the **HTTP response headers** (e.g., content-type) and the **response message body**.
- In Line 12, we set the "MIME" type of the response message to "text/html". The client need to know the message type in order to correctly display the data received. (Other MIME types include text/plain, image/jpeg, video/mpeg, application/xml, and many others.) In Line 14, we retrieve a Writer object called out for writing the response message to the client over the network. We then use the out.println() to print out a proper HTML page containing the message "Hello, world!". This servlet also echoes some of the clients's request information, and prints a random number for each request.

#### Configure the Application Deployment Descriptor - "web.xml"

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0">
    <!--  配置Servlet  -->
    <servlet>
        <servlet-name>HelloWorldServlet</servlet-name>
        <servlet-class>cn.itcast.web.servlet.HelloServlet</servlet-class>
    </servlet>

    <servlet-mapping>
        <servlet-name>HelloWorldServlet</servlet-name>
        <url-pattern>/sayhello</url-pattern>
    </servlet-mapping>

</web-app>
```
- The "web.xml" is called web application deployment descriptor. It provides the configuration options for that particular web application, such as defining the the mapping between URL and servlet class.
- The above configuration defines a servlet named "_HelloWroldServlet_", implemented in "_cn.itcast.web.servlet.HelloServlet.class_" (written earlier), and maps to URL "_/sayhello_", where "/" denotes the context root of this webapp "_helloservlet_". In other words, the absolute URL for this servlet is _http://localhost:8080/sayhello_.

<img class="shadow" width="620" src="https://www3.ntu.edu.sg/home/ehchua/programming/java/images/Servlet_HelloServletURL.png">

#### Run the Hello-world Servlet
We shall see the output "Hello, world!".
<img class="shadow" width="320" src="servlet.png" />

## Processing HTML Form Data
---
#### Write an HTML Form
Create the following HTML script, and save as "form_input.html".
```html
<!DOCTYPE html>
<html>
<head>
    <meta http-equiv='Content-Type' content='text/html; charset=UTF-8'>
    <title>User Input Form</title>
</head>

<body>
<h2>User Input Form</h2>
<form method="get" action="echo">
    <fieldset>
        <legend>Personal Particular</legend>
        Name: <input type="text" name="username" /><br /><br />
        Password: <input type="password" name="password" /><br /><br />
        Gender: <input type="radio" name="gender" value="m" checked />Male
        <input type="radio" name="gender" value="f" />Female<br /><br />
        Age: <select name = "age">
        <option value="1">&lt; 1 year old</option>
        <option value="99">1 to 99 years old</option>
        <option value="100">&gt; 99 years old</option>
    </select>
    </fieldset>

    <fieldset>
        <legend>Languages</legend>
        <input type="checkbox" name="language" value="java" checked />Java
        <input type="checkbox" name="language" value="c" />C/C++
        <input type="checkbox" name="language" value="cs" />C#
    </fieldset>

    <fieldset>
        <legend>Instruction</legend>
        <textarea rows="5" cols="30" name="instruction">Enter your instruction here...</textarea>
    </fieldset>

    <input type="hidden" name="secret" value="888" />
    <input type="submit" value="SEND" />
    <input type="reset" value="CLEAR" />
</form>
</body>
</html>
```
Start the tomcat server. Issue the following URL to request for the HTML page:
http://localhost:8080/form_input.html
<img class="shadow" width="450" src="form.png" />

##### Explanation
- The `<fieldset>...</fieldset>` tag groups related elements and displays them in a box. The `<legend>...</legend>` tag provides the legend for the box.
- This HTML form (enclosed within `<form>...</form>`) contains the following types of input elements:
    - Text field (`<input type="text">`): for web users to enter text.
    - Radio buttons (`<input type="radio">`): choose any one (and possibly none).
    - Pull-down menu (`<select>` and `<option>`): pull-down menu of options.
    - Checkboxes (`<input type="checkbox">`): chose none or more.
    - Text area (`<textarea>...<textarea>`): for web users to enter multi-line text. (Text field for single line only.)
    - Hidden field (`<input type="hidden">`): for submitting hidden name=value pair.
    - Submit button (`<input type=submit>`): user clicks this button to submit the form data to the server.
    - Reset button (`<input type="reset">`): resets all the input field to their default value.

- Each of the input elements has an attribute "`name`", and an optional attribute "`value`". If an element is selected, its "`name=value`" pair will be submitted to the server for processing.
- The `<form>` start-tag also specifies the URL for submission in the `action="url"` attribute, and the request method in the `method="get|post"` attribute.

For example, suppose that we enter "Alan Smith" in the text field, select "male", and click the "SEND" button, we will get a "404 page not found" error (because we have yet to write the processing script). BUT observe the destination URL:
 
    ```html
http://localhost:8080/echo?username=Alan+Smit&password=&gender=m&age=1&language=java&instruction=Enter+your+instruction+here...&secret=888
    ```
 
Observe that:
- The URL `http://localhost:8080/echo` is retrieved from the attribute `action="echo"` of the <form> start-tag. Relative URL is used in this example. The base URL for the current page "`form_input.html`" is `http://localhost:8080/`. Hence, the relative URL "`echo`" resolves into `http://localhost:8080/echo`.
- A '`?`' follows the URL, which separates the URL and the so-called query string (or query parameters, request parameters) followed.
- The query string comprises the "`name=value`" pairs of the selected input elements (i.e., "`username=Alan+Smith`" and "`gender=m`"). The "`name=value`" pairs are separated by an '`&`'. Also take note that the blank (in "`Alan Smith`") is replace by a '`+`'. This is because special characters are not permitted in the URL and have to be encoded (known as URL-encoding). Blank is encoded as '`+`' (or `%20`). Other characters are encoded as %xx, where xx is the ASCII code in hex. For example, '`&`' as %26, '`?`' as %3F.
- Some input elements such as checkboxes may trigger multiple parameter values, e.g., "`language=java&language=c&language=cs`" if all three boxes are checked.
- HTTP provides two request methods: **GET** and **POST**. For GET request, the query parameters are appended behind the URL. For POST request, the query string are sent in the request message's body. POST request is often preferred, as users will not see the strange string in the URL and it can send an unlimited amount of data. The amount of data that can be sent via the GET request is limited by the length of the URL. The request method is specified in the `<form method="get|post"...>` start-tag. In this tutorial, we use the GET request, so that you can inspect the query string.

#### Write a Servlet to Process Form Data - "EchoServlet.java"
The form that we have written send its data to a server-side program having relative URL of "`echo`" (as specified in the `action="url"` attribute of the `<form>` start-tag). Let us write a servlet called **EchoServlet**, which shall be mapped to the URL "`echo`", to process the incoming form data. The servlet simply echoes the data back to the client.
```java
package cn.itcast.web.servlet;
import java.io.*;
import javax.servlet.*;
import javax.servlet.http.*;
import java.util.*;

public class EchoServlet extends HttpServlet {

    @Override
    public void doGet(HttpServletRequest request, HttpServletResponse response)
            throws IOException, ServletException {
        // Set the response message's MIME type
        response.setContentType("text/html; charset=UTF-8");
        // Allocate a output writer to write the response message into the network socket
        PrintWriter out = response.getWriter();

        // Write the response message, in an HTML page
        try {
            out.println("<!DOCTYPE html>");
            out.println("<html><head>");
            out.println("<meta http-equiv='Content-Type' content='text/html; charset=UTF-8'>");
            out.println("<title>Echo Servlet</title></head>");
            out.println("<body><h2>You have enter</h2>");

            // Retrieve the value of the query parameter "username" (from text field)
            String username = request.getParameter("username");
            // Get null if the parameter is missing from query string.
            // Get empty string or string of white spaces if user did not fill in
            if (username == null
                    || (username = htmlFilter(username.trim())).length() == 0) {
                out.println("<p>Name: MISSING</p>");
            } else {
                out.println("<p>Name: " + username + "</p>");
            }

            // Retrieve the value of the query parameter "password" (from password field)
            String password = request.getParameter("password");
            if (password == null
                    || (password = htmlFilter(password.trim())).length() == 0) {
                out.println("<p>Password: MISSING</p>");
            } else {
                out.println("<p>Password: " + password + "</p>");
            }

            // Retrieve the value of the query parameter "gender" (from radio button)
            String gender = request.getParameter("gender");
            // Get null if the parameter is missing from query string.
            if (gender == null) {
                out.println("<p>Gender: MISSING</p>");
            } else if (gender.equals("m")) {
                out.println("<p>Gender: male</p>");
            } else {
                out.println("<p>Gender: female</p>");
            }

            // Retrieve the value of the query parameter "age" (from pull-down menu)
            String age = request.getParameter("age");
            if (age == null) {
                out.println("<p>Age: MISSING</p>");
            } else if (age.equals("1")) {
                out.println("<p>Age: &lt; 1 year old</p>");
            } else if (age.equals("99")) {
                out.println("<p>Age: 1 to 99 years old</p>");
            } else {
                out.println("<p>Age: &gt; 99 years old</p>");
            }

            // Retrieve the value of the query parameter "language" (from checkboxes).
            // Multiple entries possible.
            // Use getParameterValues() which returns an array of String.
            String[] languages = request.getParameterValues("language");
            // Get null if the parameter is missing from query string.
            if (languages == null || languages.length == 0) {
                out.println("<p>Languages: NONE</p>");
            } else {
                out.println("<p>Languages: ");
                for (String language : languages) {
                    if (language.equals("c")) {
                        out.println("C/C++ ");
                    } else if (language.equals("cs")) {
                        out.println("C# ");
                    } else if (language.equals("java")) {
                        out.println("Java ");
                    }
                }
                out.println("</p>");
            }

            // Retrieve the value of the query parameter "instruction" (from text area)
            String instruction = request.getParameter("instruction");
            // Get null if the parameter is missing from query string.
            if (instruction == null
                    || (instruction = htmlFilter(instruction.trim())).length() == 0
                    || instruction.equals("Enter your instruction here...")) {
                out.println("<p>Instruction: NONE</p>");
            } else {
                out.println("<p>Instruction: " + instruction + "</p>");
            }

            // Retrieve the value of the query parameter "secret" (from hidden field)
            String secret = request.getParameter("secret");
            out.println("<p>Secret: " + secret + "</p>");

            // Get all the names of request parameters
            Enumeration names = request.getParameterNames();
            out.println("<p>Request Parameter Names are: ");
            if (names.hasMoreElements()) {
                out.print(htmlFilter(names.nextElement().toString()));
            }
            do {
                out.print(", " + htmlFilter(names.nextElement().toString()));
            } while (names.hasMoreElements());
            out.println(".</p>");

            // Hyperlink "BACK" to input page
            out.println("<a href='form_input.html'>BACK</a>");

            out.println("</body></html>");
        } finally {
            out.close();  // Always close the output writer
        }
    }

    // Redirect POST request to GET request.
    @Override
    public void doPost(HttpServletRequest request, HttpServletResponse response)
            throws IOException, ServletException {
        doGet(request, response);
    }

    // Filter the string for special HTML characters to prevent
    // command injection attack
    private static String htmlFilter(String message) {
        if (message == null) return null;
        int len = message.length();
        StringBuffer result = new StringBuffer(len + 20);
        char aChar;

        for (int i = 0; i < len; ++i) {
            aChar = message.charAt(i);
            switch (aChar) {
                case '<': result.append("&lt;"); break;
                case '>': result.append("&gt;"); break;
                case '&': result.append("&amp;"); break;
                case '"': result.append("&quot;"); break;
                default: result.append(aChar);
            }
        }
        return (result.toString());
    }
}

```
**Dissecting the Program**
- The query string comprises `name=value` pairs. We can retrieve the query parameters from the request message (captured in `doGet()`'s argument `HttpServletRequest request`) via one of the following methods:
    ```java
request.getParameter("paramName")
  // Returns the parameter value in a String.
  // Returns null if parameter name does not exist.
  // Returns the first parameter value for a multi-value parameter.
 
request.getParameterValues("paramName")
  // Return all the parameter values in a String[].
  // Return null if the parameter name does not exist.
 
request.getParameterNames()
  // Return all the parameter names in a java.util.Enumeration, possibly empty.
    ```

- Take note that the parameter name is case sensitive.
- We also replace the special HTML characters (`>`, `<`, `&`, `"`) with the HTML escape sequences in the input strings, before we echo them back to the client via `out.println()`. This step is necessary to prevent the so-called `command-injection attack`, where user enters a script into the text field. The replacement is done via a static helper method `htmlFilter()`.
- If the parameter could possess multiple values (e.g., checkboxes), we use `request.getParameterValues()`, which returns an array of `String` or `null` if the parameter does not exist.
- One of the nice features of Java servlet is that all the form data decoding (i.e., URL-decoding) is handled automatically. That is, '+' will be decoded to blank, %xx decoded into the corresponding character.

#### Configure the Servlet URL mapping in "web.xml"
```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0">
    <!--  配置Servlet  -->
    <servlet>
        <servlet-name>demo1</servlet-name>
        <servlet-class>cn.itcast.web.servlet.ServletDemo1</servlet-class>
    </servlet>

    <servlet>
        <servlet-name>HelloWorldServlet</servlet-name>
        <servlet-class>cn.itcast.web.servlet.HelloServlet</servlet-class>
    </servlet>

    <servlet>
        <servlet-name>EchoServletExample</servlet-name>
        <servlet-class>cn.itcast.web.servlet.EchoServlet</servlet-class>
    </servlet>

    <servlet-mapping>
        <servlet-name>demo1</servlet-name>
        <url-pattern>/demo1</url-pattern>
    </servlet-mapping>

    <servlet-mapping>
        <servlet-name>HelloWorldServlet</servlet-name>
        <url-pattern>/sayhello</url-pattern>
    </servlet-mapping>

    <servlet-mapping>
        <servlet-name>EchoServletExample</servlet-name>
        <url-pattern>/echo</url-pattern>
    </servlet-mapping>
</web-app>
```
#### Run the EchoServlet
Start the Tomcat server. Issue URL `http://localhost:8080/form_input.html`.

<img class="shadow" width="450" src="form2.png" />
Fill up the form, click the submit button to trigger the servlet. Alternatively, you could issue a URL with query string.
<img class="shadow" width="450" src="form_2.png" />

#### Form-Data Submission Methods: GET|POST
Two request methods, GET and POST, are available for submitting form data, to be specified in the `<form>`'s attribute "`method=GET|POST`". GET and POST performs the same basic function. That is, gather the name-value pairs of the selected input elements, URL-encode, and pack them into a query string. However, in a GET request, the query string is appended behind the URL, separated by a '?'. Whereas in a POST request, the query string is kept in the request body (and not shown in the URL). The length of query string in a GET request is limited by the maximum length of URL permitted, whereas it is unlimited in a POST request. I recommend POST request for production, as it does not show the strange looking query string in the URL, even if the amount of data is limited. In this tutorial, I use GET method, so that you can inspect the query string on the URL.

To try out the POST request, modify the "`form_input.html`":
```html
<form method="post" action="echo">
  ......
</form>
```

Inside the servlet, GET request is processed by the method `doGet()`, while POST request is processed by the method `doPost()`. Since they often perform identical operations, we re-direct `doPost()` to `doGet()` (or vice versa), as follows:
```java
public class MyServlet extends HttpServlet {
   // doGet() handles GET request
   @Override
   public void doGet(HttpServletRequest request, HttpServletResponse response)
               throws IOException, ServletException {
      ......
      ......
   }
   
   // doPost() handles POST request
   @Override
   public void doPost(HttpServletRequest request, HttpServletResponse response)
               throws IOException, ServletException {
      doGet(request, response);  // call doGet()
   }
}
```

## Request Header and Response Header
HTTP is a request-response protocol. The client sends a request message to the server. The server, in turn, returns a response message. The request and response messages consists of two parts: header (information about the message) and body (contents). Header provides information about the messages. The data in header is organized in name-value pairs. Read "`HTTP Request and Response Messages`" for the format, syntax of request and response messages.

#### HttpServletRequest
The request message is encapsulated in an `HttpServletRequest` object, which is passed into the `doGet()` methods. `HttpServletRequest` provides many methods for you to retrieve the headers:
- General methods: `getHeader(name)`, `getHeaders(name)`, `getHeaderNames()`.
- Specific methods: `getContentLength()`, `getContentType()`, `getCookies()`, `getAuthType()`, etc.
- URL related: `getRequestURI()`, `getQueryString()`, `getProtocol()`, `getMethod()`.

#### HttpServletResponse
The response message is encapsulated in the `HttpServletResponse`, which is passed into `doGet()` by reference for receiving the servlet output.
- `setStatusCode(int statuscode)`, `sendError(int code, String message)`, `sendRedirect(url)`.
- `response.setHeader(String headerName, String headerValue)`.
- `setContentType(String mimeType)`, `setContentLength(int length)`, etc.

## Session Tracking
HTTP is a stateless protocol. In other words, the current request does not know what has been done in the previous requests. This creates a problem for applications that runs over many requests, such as online shopping (or shopping cart). You need to maintain a so-called **session** to pass data among the multiple requests.

You can maintain a session via one of these three approaches:
1. **Cookie**: A cookie is a small text file that is stored in the client's machine, which will be send to the server on each request. You can put your session data inside the cookie. The biggest problem in using cookie is clients may disable the cookie.
2. **URL** **Rewriting**: Passes data by appending a short text string at the end of every URL, e.g., `http://host/path/file.html;jsessionid=123456`. You need to rewrite all the URLs (e.g., the "`action`" attribute of `<form>`) to include the session data.
3. **Hidden field in an HTML form**: pass data by using hidden field tag (`<input type="hidden" name="session" value="...." />`). Again, you need to include the hidden field in all the pages.

#### HttpSession
Programming your own session tracking (using the above approaches) is tedious and cumbersome. Fortunately, Java Servlet API provides a session tracking facility, via an interface called `javax.servlet.http.HttpSession`. It allows servlets to:
- View and manipulate information about a session, such as the session identifier, creation time, and last accessed time.
- Bind objects to sessions, allowing user information to persist across multiple user requests.
