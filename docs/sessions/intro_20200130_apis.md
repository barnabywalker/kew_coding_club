# APIs and their use

# What is an API?

API stands for Application Programming Interface and it is basically a server that can be used to retrieve or send information programmatically.

An API can do a lot of things: 
-   **GET:**  requests data from a server.
-   **POST:**  sends changes to the server.
-   **PUT:**  revises information.
-   **DELETE:**  deletes information.

We will focus into retrieve data (GET) , however we have some examples to send it as well (POST). 

In order to receive data from an API we need to make a **request**

![](https://hackernoon.com/hn-images/1*q9CRTmO258jWLsMZAd5JLw.png)

_This image is from Robert Drummond blog about how to build an API on a Raspberry Pi_

# Why should I use an API?
Basically an API allows you to access to the data of a third party without having to develop yourself any code to do it. Besides, the amount of coding needed to communicate to and retrieve data from a server is quite a lot and using an API will liberate you time to focus on the treatment of the data. 
Also, many of the problems that you could find to retrieve the data has been already solved by the developers of the API so you just need to consume it painless. 

# API response codes
When we are making a GET request we can have different responses from the server, we not always we have a the information straightforward from it. The most common responses that we can have are:

* 200; this is the code when everything has worked as expected.
* 301; redirected to a different point, the host has changed.
* 400; bad request. You will see this **A LOT**. When the request is not formed properly or there is no data to return. 
* 401; non authenticated. Some APIs required login credentials. 
* 403; forbidden. You don't have the right permissions to access the API. 
* 404; not found. This is quite common as well. Basically, something is wrong in the server. The URL indicated is not available, etc...
* 503; server not ready. Quite common as well. 

# API basic examples

This is a simple query to the gbif API to retrieve all the occurences between 1800 and 1899:
http://api.gbif.org/v1/occurrence/search?year=1800,1899
