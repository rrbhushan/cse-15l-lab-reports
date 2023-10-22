# Lab Report 2
### Part 1
StringServer code:

![Image](/lab2images/l2code.png)

First use of `/add-message`:

![Image](/lab2images/l2ss1.png)

The methods called in my code are `handleRequest` (which the relevant arguments is the url provided), `main` (which the relevant argument is the port number specified when initiating the server, taken as a string for the time being), and then methods from Server.java, which include `handle` (relevant argument would be an HttpExchange type input) and `start` (which the relevant arguments are the port provided as an integer and the url handler). In terms of changed values, the argument provided to `main` is taken in as a string, but is changed to an integer for `start` so that it can act as the port number. Additionally, the url input after `?s=` gets treated as a string despite the type specificity, but this is to be treated as a normal case as URLs are just query strings. In this case, the string recorded into `newMess` also has all the "+" instances changed into " " using the `replace` function, as this was done due to my platform being a Mac, which would usually produce a "+" whenever a space was inputted.

Second use of `/add-message`:

![Image](/lab2images/l2ss2.png)

The methods called in my code are `handleRequest` (which the relevant arguments is the url provided), `main` (which the relevant argument is the port number specified when initiating the server, taken as a string for the time being), and then methods from Server.java, which include `handle` (relevant argument would be an HttpExchange type input) and `start` (which the relevant arguments are the port provided as an integer and the url handler). In terms of changed values, the argument provided to `main` is taken in as a string, but is changed to an integer for `start` so that it can act as the port number. Additionally, the url input after `?s=` gets treated as a string despite the type specificity, but this is to be treated as a normal case as URLs are just query strings. Just like the previous case, the string recorded into `newMess` also has all the "+" instances changed into " " using the `replace` function, as this was done due to my platform being a Mac, which would usually produce a "+" whenever a space was inputted. Lastly, the string is being updated with this new `/add-message` request, so it adds another count, followed by the message to be added (all this is recorded under a single string that keeps track of all prior additions).

***

### Part 2
Path to private key for SSH key for logging into ieng6:

![Image](/lab2images/l2ls1.png)

Path to public key for SSH key for logging into ieng6:

![Image](/lab2images/l2ls2.png)

Logging in without a password prompt:

![Image](/lab2images/l2login.png)

***

### Part 3
I really liked learning about how to create my own server, along with being able to login without needing to input my password to my ieng6 account. Before, I had no clue about any of these, especially with how people create servers but it's a straightforward process, which can be used to apply code that I have written to a more global scale in that anyone can access it and update to the program running by adding in a message, for example. In terms of logging in without needing to input my password, that is a big relief as I do not have to constantly refer back to what I used as my password, with the help of ssh keys. 
