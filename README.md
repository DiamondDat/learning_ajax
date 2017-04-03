# RESEARCH AJAX
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

###XMLHttpRequest Object Methods
* new XMLHttpRequest()               :                Creates a new XMLHttpRequest object
* abort()                            :                Cancels the current request
* getAllReponseHeaders()             :              Returns header information
* get ReponseHeader()                :                 Returns specific header information
* open(method, url, async, user, psw): Specifies the request

                                        method: the request type GET or POST
                                        url: the file location
                                        async: true (asynchronous) or false (synchronous)
                                        user: optional user name
                                        psw: optional password
* send()                             :  Sends the request to the server
                                        Used for GET requests
* send(string)                        : Sends the request to the server
                                        Used for POST requests
* setRequestHeader()                  : Adds a label/value pair to the header to be sent

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
* onreadystatechange	Defines a function to be called when the readyState property changes
* readyState	        Holds the status of the XMLHttpRequest. 
                      0: request not initialized 
                      1: server connection established
                      2: request received 
                      3: processing request 
                      4: request finished and response is ready
* status	            200: "OK"
                      403: "Forbidden"
                      404: "Page not found"
*statusText	          Returns the status-text (e.g. "OK" or "Not Found")

## Using a Callback Function
A callback function is a function passed as a parameter to another function

## Server Response Properties
responseText: get the response data as a string
responseXML:  get the response data as XML data

## Server Response Methods
getResponseHeader()    : Returns specific header information from the server resource
getAllResponseHeaders(): Returns all the header information from the server resource































