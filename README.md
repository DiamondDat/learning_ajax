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


## AJAX - Send a Request to a Server
The XMLHttpRequest object is used to exchange data with a server.
```
xhttp.open("GET", "ajax_info.txt", true);
xhttp.send();
```
### GET or POST?
GET is simpler and faster than POST, can be used in most cases
Use POST requests when:
* A cached file is not an option (update a file or database on the server).
* Sending a large amount of data to the server (POST has no size limitations).
* Sending user input(which can contain unknown characters), POST is more robust and secure than GET.

## AJAX - Server Response
* onreadystatechange: Defines a function to be called when the readyState property changes
* readyState: Holds the status of the XMLHttpRequest. 
    * 0: request not initialized 
    * 1: server connection established
    * 2: request received 
    * 3: processing request 
    * 4: request finished and response is ready

* status: 
  200: "OK"
  403: "Forbidden"
  404: "Page not found"
                      
* statusText: Returns the status-text (e.g. "OK" or "Not Found")

## Using a Callback Function
A callback function is a function passed as a parameter to another function

## Server Response Properties
responseText: get the response data as a string
responseXML:  get the response data as XML data

## Server Response Methods
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
The only thing you have to do to enable Turbolinks is have it in your Gemfile, and put `//= require` turbolinks in your JavaScript manifest, which is usually `app/assets/javascripts/application.js`.
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
