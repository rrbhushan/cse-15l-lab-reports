# Lab Report 2
### Part 1
StringServer code:

![Image](/lab2images/l2code.png)

First use of `/add-message`:

![Image](/lab2images/l2ss1.png)

The methods called in my code are `handleRequest` (which the relevant arguments is the url provided), `main` (which the relevant argument is the port number specified when initiating the server, taken as a string for the time being), and then methods from Server.java, which include `handle` (relevant argument would be an HttpExchange type input) and `start` (which the relevant arguments are the port provided as an integer and the url handler). In terms of changed values, the argument provided to `main` is taken in as a string, but is changed to an integer for `start` so that it can act as the port number. Additionally, the url input after `?s=` gets treated as a string despite the type specificity, but this is to be treated as a normal case as URLs are just query strings. In this case, the string recorded into `newMess` also has all the "+" instances changed into " " using the `replace` function, as this was done due to my platform being a Mac, which would usually produce a "+" whenever a space was inputted.

Second use of `/add-message`:

![Image](/lab2images/l2ss2.png)

The methods called in my code are `handleRequest` (which the relevant arguments is the url provided), `main` (which the relevant argument is the port number specified when initiating the server, taken as a string for the time being), and then methods from Server.java, which include `handle` (relevant argument would be an HttpExchange type input) and `start` (which the relevant arguments are the port provided as an integer and the url handler). In terms of changed values, the argument provided to `main` is taken in as a string, but is changed to an integer for `start` so that it can act as the port number. Additionally, the url input after `?s=` gets treated as a string despite the type specificity, but this is to be treated as a normal case as URLs are just query strings. In this case, the string recorded into `newMess` also has all the "+" instances changed into " " using the `replace` function, as this was done due to my platform being a Mac, which would usually produce a "+" whenever a space was inputted.

***

### Part 2
Path to private key for SSH key for logging into ieng6:

![Image](/lab2images/l2ls1.png)

Path to public key for SSH key for logging into ieng6:

![Image](/lab2images/l2ls2.png)

Logging in without a password prompt:

![Image](/lab2images/l2ls3.png)

***

### Part 3
Describing something I didn't know.
