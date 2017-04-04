# RESEARCH AJAX
## AJAX
* Update a web page without reloading the page
* Request data from a server - after the page has loaded
* Receive data from a server - after the page has loaded
* Send data to a server - in the background

AJAX = *A*synchronous *J*avascript *A*nd *X*ML.
AJAX is not a programming language.
AJAX uses a combination of:
* A browser built-in XMLHttpRequest object (to request data from a web server)
* JavaScript & HTML DOM (to display or use the data)

## The XMLHttpRequest Object
Syntax for creating an XMLHttpRequest object:
```
variable = new XMLHttpRequest();
```

### XMLHttpRequest Object Methods
* new XMLHttpRequest(): Creates a new XMLHttpRequest object
* abort(): Cancels the current request
* getAllReponseHeaders(): Returns header information
* get ReponseHeader(): Returns specific header information
* open(method, url, async, user, psw): Specifies the request
    * method: the request type GET or POST
    * url: the file location
    * async: true (asynchronous) or false (synchronous)
    * user: optional user name
    * psw: optional password
* send(): 
    * Sends the request to the server
    * Used for GET requests
* send(string): 
    * Sends the request to the server
    * Used for POST requests
* setRequestHeader(): Adds a label/value pair to the header to be sent
### Handling binary data
You need to add the event listeners before calling open() on the request.  Otherwise the progress events will not fire.
### Submitting forms and uploading files
* Using only AJAX
* Using FormData API
#### Using nothing but XMLHttpReques
An html `<form>` can be sent in four ways:
* using the POST method and setting the enctype attribute to application/x-www-form-urlencoded (default);
* using the POST method and setting the enctype attribute to text/plain;
* using the POST method and setting the enctype attribute to multipart/form-data;
* using the GET method (in this case the enctype attribute will be ignored).
### XMLHttpRequest Properties
* onreadystatechange: Defines a function to be called when the readyState property changes
* readyState: Holds the status of the XMLHttpRequest. 
    * 0: request not initialized 
    * 1: server connection established
    * 2: request received 
    * 3: processing request 
    * 4: request finished and response is ready

* status:
   * 200: "OK"
   * 403: "Forbidden"
   * 404: "Page not found"
                      
* statusText: Returns the status-text (e.g. "OK" or "Not Found")

## AJAX - Send a Request to a Server
The XMLHttpRequest object is used to exchange data with a server.
Using GET 
```
xhttp.open("GET", "ajax_info.txt", true);
xhttp.send();
```
USING POST
To POST data like an HTML form, add an HTTP header with setRequestHeader(). Specify the data you want to send in the send() method:
```
xhttp.open("POST", "ajax_test.asp", true);
xhttp.setRequestHeader("Content-type", "application/x-www-form-urlencoded");
xhttp.send("fname=Henry&lname=Ford");
```
### GET or POST?
GET is simpler and faster than POST, can be used in most cases
Use POST requests when:
* A cached file is not an option (update a file or database on the server).
* Sending a large amount of data to the server (POST has no size limitations).
* Sending user input(which can contain unknown characters), POST is more robust and secure than GET.

## AJAX - Server Response
```
function loadDoc() {
    var xhttp = new XMLHttpRequest();
    xhttp.onreadystatechange = function() {
        if (this.readyState == 4 && this.status == 200) {
            document.getElementById("demo").innerHTML =
            this.responseText;
       }
    };
    xhttp.open("GET", "ajax_info.txt", true);
    xhttp.send(); 
}
```

### Using a Callback Function
A callback function is a function passed as a parameter to another function

### Server Response Properties
responseText: get the response data as a string
responseXML:  get the response data as XML data

### Server Response Methods
getResponseHeader(): Returns specific header information from the server resource
getAllResponseHeaders(): Returns all the header information from the server resource

## Browser Support
All the available browsers cannot support AJAX. Here is a list of major browsers, that support AJAX.
* Mozilla Firefox 1.0 and above.
* Netscape version 7.1 and above.
* Apple Safari 1.2 and above.
* Microsoft Internet Explorer 5 and above.
* Konqueror.
* Opera 7.6 and above.

## Writing Browser Specific Code
The Simplest way to make your source code compatible with a browser is to use try...catch blocks in your JavaScript.
```
<script language="javascript" type="text/javascript">
   <!-- 
   //Browser Support Code
   function ajaxFunction(){
      var ajaxRequest;  // The variable that makes Ajax possible!

      try{
         // Opera 8.0+, Firefox, Safari 
         ajaxRequest = new XMLHttpRequest();
      }catch (e){

         // Internet Explorer Browsers
         try{
            ajaxRequest = new ActiveXObject("Msxml2.XMLHTTP");
         }catch (e) {
            try{
               ajaxRequest = new ActiveXObject("Microsoft.XMLHTTP");
            }catch (e){

               // Something went wrong
               alert("Your browser broke!");
               return false;
            }
         }
      }
   }
   //-->
   </script>
```
## Security
### Server side
* AJAX-based Web applications use the same server-side security schemes of regular Web applications.
* You specify authentication, authorization, and data protection requirements in your web.xml file (declarative) or in your program (programmatic).
* AJAX-based Web applications are subject to the same security threats as regular Web applications.
### Client side
* JavaScript code is visible to a user/hacker. Hacker can use JavaScript code for inferring server-side weaknesses.
* JavaScript code is downloaded from the server and executed ("eval") at the client and can compromise the client by mal-intended code.
* Downloaded JavaScript code is constrained by the sand-box security model and can be relaxed for signed JavaScript.

## [Working with JavaScript in Rails](http://guides.rubyonrails.org/working_with_javascript_in_rails.html#an-introduction-to-ajax)
Rails ships with CoffeeScript by default, of course, the rules apply to vanilla JavaScript as well.
Example: 
```
$.ajax(url: "/test").done (html) ->
  $("#results").append html
```
### Turbolinks
Rails ships with the Turbolinks library, which uses Ajax to speed up page rendering in most applications.
#### How turbolinks work
The only thing you have to do to enable Turbolinks is have it in your Gemfile, and put `//= require turbolinks` in your JavaScript manifest, which is usually `app/assets/javascripts/application.js`.
#### Page change events
When writing CoffeeScript, you'll often want to do some sort of processing upon page load. With jQuery, you'd write something like this:
```
$(document).ready ->
  alert "page has loaded!"
```
However, because Turbolinks overrides the normal page loading process, the event that this relies on will not be fired. If you have code that looks like this, you must change your code to do this instead:
```
$(document).on "turbolinks:load", ->
  alert "page has loaded!"
  ```
#### Render both html and javascript responses in Controller
* Render both html and javascript responses with all of our controller actions.
```
respond_to :html, :js
```
* Render for specific action in controller
```
respond_to do |format|
  format.html
  format.json
 end
```

# HTTP Request & Response
It's a stateless request-response based communication protocol. It's used to send and receive data on the Web i.e., over the Internet. This protocol uses reliable TCP connections either for the transfer of data to and from clients which are Web Browsers in this case. HTTP is a stateless protocol means the HTTP Server doesn't maintain the contextual information about the clients communicating with it and hence we need to maintain sessions in case we need that feature for our Web-applications.

An HTTP request consists of two parts: a header that contains a set of global metadata about the browser's capabilities, and a body that can contain information necessary for the server to process the specific request.

##GET - Requests data from a specified resource
Note that the query string (name/value pairs) is sent in the URL of a GET request
```
/test/demo_form.php?name1=value1&name2=value2
```
* GET requests can be cached
* GET requests remain in the browser history
* GET requests can be bookmarked
* GET requests should never be used when dealing with sensitive data
* GET requests have length restrictions
* GET requests should be used only to retrieve data

##POST - Submits data to be processed to a specified resource
Note that the query string (name/value pairs) is sent in the HTTP message body of a POST request
```
POST /test/demo_form.php HTTP/1.1
Host: w3schools.com
name1=value1&name2=value2
```
* POST requests are never cached
* POST requests do not remain in the browser history
* POST requests cannot be bookmarked
* POST requests have no restrictions on data length
## Other HTTP Request Methods
| Methods | Description
|---------|------------
| HEAD    | Same as GET but returns only HTTP headers and no document body
| PUT     | Uploads a representation of the specified URI
| PATCH   | Update the specified resource
| DELETE  | Deletes the specified resource
| OPTIONS | Returns the HTTP methods that the server supports
| CONNECT | Converts the request connection to a transparent TCP/IP tunnel

## Format of an HTTP Request
It has three main components, which are:-
* HTTP Request Method, URI, and Protocol Version - this should always be the first line of an HTTP Request. As it's quite evident from the name itself, it contains the HTTP Request method being used for that particular request, the URI, and the HTTP protocol name with the version being used. It may look like 'GET /servlet/jspName.jsp HTTP/1.1' where the request method being used is 'GET', the URI is '/servlet/jspName.jsp', and the protocol (with version) is 'HTTP/1.1'.
* HTTP Request Headers - this section of an HTTP Request contains the request headers, which are used to communicate information about the client environment. Few of these headers are: Content-Type, User-Agent, Accept-Encoding, Content-Length, Accept-Language, Host, etc. Very obvious to understand what info do these headers carry, isn't it? The names are quite self-explanatory.
* HTTP Request Body - this part contains the actual request being sent to the HTTP Server. The HTTP Request Header and Body are separated by a blank line (CRLF sequence, where CR means Carriage Return and LF means Line Feed). This blank line is a mandatory part of a valid HTTP Request.

## Format of an HTTP Response
Similar to an HTTP Request, an HTTP Response also has three main components, which are:-
* Protocol/Version, Status Code, and its Description - the very first line of a valid HTTP Response is consists of the protocol name, it's version, status code of the request, and a short description of the status code. A status code of 200 means the processing of request was successful and the description in this case will be 'OK'. Similarly, a status code of '404' means the file requested was not found at the HTTP Server at the expected location and the description in this case is 'File Not Found'.
* HTTP Response Headers - similar to HTTP Request Headers, HTTP Response Headers also contain useful information. The only difference is that HTTP Request Headers contain information about the environment of the client machine whereas HTTP Response Headers contain information about the environment of the server machine. This is easy to understand as HTTP Requests are formed at the client machine whereas HTTP Responses are formed at the server machine. Few of these HTTP Response headers are: Server, Content-Type, Last-Modified, Content-Length, etc.
* HTTP Response Body - this the actual response which is rendered in the client window (the browser window). The content of the body will be HTML code. Similar to HTTP Request, in this case also the Body and the Headers components are separated by a mandatory blank line (CRLF sequence).

## Status code
| S.N | Code & Description 
|-----|--------------------
| 1   | **1xx: Informational** It means the request has been received and the process is continuing.
| 2   | **2xx: Success** It means the action was successfully received, understood, and accepted.
| 3   | **3xx: Redirection** It means further action must be taken in order to complete the request.
| 4   | **4xx: Client Error** It means the request contains incorrect syntax or cannot be fulfilled. 
| 5   | **5xx: Server Error** It means the server failed to fulfill an apparently valid request.

# Query String
On the World Wide Web, a query string is the part of a uniform resource locator (URL) containing data that does not fit conveniently into a hierarchical path structure. The query string commonly includes fields added to a base URL by a Web browser or other client application, for example as part of an HTML form.
A typical URL containing a query string is as follows:

## Structure
```
http://example.com/over/there?name=ferret
```
When a server receives a request for such a page, it may run a program, passing the query string, which in this case is, `name=ferret` unchanged, to the program. The first question mark is used as a separator, and is not part of the query string.

A link in a web page may have a URL that contains a query string. HTML defines three ways a user agent can generate the query string:
* an HTML form via the `<form>...</form>` element
* a server-side image map via the ismap attribute on the `<img>` element with a `<img ismap>` construction
* an indexed search via the now deprecated `<isindex>` element (Deprecated)
### Web forms
One of the original uses was to contain the content of an HTML form, also known as web form. In particular, when a form containing the fields field1, field2, field3 is submitted, the content of the fields is encoded as a query string as follows:
```
field1=value1&field2=value2&field3=value3...
```
* The query string is composed of a series of field-value pairs.
* Within each pair, the field name and value are separated by an equals sign, '='.
* The series of pairs is separated by the ampersand, '&' (or semicolon, ';' for URLs embedded in HTML and not generated by a `<form>...</form>`. See below).

While there is no definitive standard, most web frameworks allow multiple values to be associated with a single field (e.g. `field1=value1&field1=value2&field2=value3`).

For each field of the form, the query string contains a pair field=value. Web forms may include fields that are not visible to the user; these fields are included in the query string when the form is submitted.

## URL Encoding
HTML 5 specifies the following transformation for submitting HTML forms with the "get" method to a web server:
* Characters that cannot be converted to the correct charset are replaced with HTML numeric character references
* SPACE is encoded as '+' or '%20'
* Letters (A–Z and a–z), numbers (0–9) and the characters '*','-','.' and '_' are left as-is
* All other characters are encoded as %HH hex representation with any non-ASCII characters first encoded as UTF-8 (or other specified encoding)
