# #1 Tutorial: My first Webserver 
In this forst tutorial you are going to create a webserver with a webpage and deploy it to an online host. So the result will be your first, public accessable Node.js website.

You will be guided through installing Node.js on your computer, creating a webserver on your Node.js installation. This webserver will be accessable to anyone on the local network you are currently on. Then you will create an account at Heroku, a host, where you will be deploying your new website. At the end you will have your first Node.js public accesable website up and running.

## Installing Node.js

First of all you need to download and install [Node.js](https://nodejs.org/en/) _(download the version with the LTS prefix (LTS = Long Term Support))_. The Installations is pretty straight forward, but if you need it, guides kan be found here:

* [Installing Node.js on a Mac](https://www.lynda.com/MyPlaylist/Watch/5464398/110731?autoplay=true)
* [Installing Node.js on Windows](https://www.lynda.com/MyPlaylist/Watch/5464398/110731?autoplay=true)
* [Installing Node.js on Linux](https://www.lynda.com/MyPlaylist/Watch/5464398/110731?autoplay=true)

To test if your installation went ok, and that you have Node.js on your computer, open the console and type:

<pre>node --version</pre>
Then you should see something like this:

<pre>node --version
v4.4.7</pre>

The version number could differ in your case. If you do not see this, something went wrong in the installation process, and try to install Node.js again.

## Create a local Webserver

Now let´s create our first server. Create a folder and in it a file called server.js, containing the following code.

```prettyprint javascript
    var http = require('http');

    var server = http.createServer(function (req, res) {
      res.writeHead(200, {'Content-Type': 'text/plain'});
      res.end('Hello World\n');
    });

    server.listen(3000);

```

Start the server from the console by browsing to the folder you just created and type:

```javascript   
   node server.js   
```

Now open your browser and type in the url: http://localhost:3000/

![](/img/browser.png)

If what you made now is indeed a webserver, and not just a document saying “Hello World”,  you should be able to access this site from you phone or another computer.

Get the ip-address of you machine (the server) and then make sure that your phone is on the same network as your computer (the server). Type in 10.108.10.86:3000 (this is my ip, you should of cause use yours).

<img src="/img/iphone.png" width="400" >


Hopefully you see this, otherwise check if your devices are on the same network.

## HTML 

Normally a webpage is presented a bit more detailed than the plain text file with "Hello world".
Instead of plain text we can formate the output in html instead. This makes us able to structure our content and to add collors and other design elements.

Change the 2 lines in your webserver code to:

```prettyprint javascript

      res.writeHead(200, {'Content-Type': 'text/html'});
      res.end('<h1>Hello World</h1><p>This is my first html page</p>');

```
Then stop you server by typing ``` ctrl + c ``` and start it again by in the console typing:

```javascript   
      node server.js   
``` 
Now you should see something like this instead.

<img src="/img/htmlscreen.png" width="400" >

## JSON
Another way of outputting data from a webserver is by serving the data in JSON format.
When we do this it is called a web api. 

```prettyprint JSON
      {
        "title" : "Hello World",
        "Text" : "This is my first web api"
      }
```

Now stop the server by typing ``` ctrl + c ```.

Change the 2 lines in the code to:

```prettyprint javascript

      res.writeHead(200, {'Content-Type': 'text/json'});
      res.end('{
          "title" : "Hello World",
          "Text" : "This is my first web api"
      }');

```
Start the server again

```javascript   
      node server.js   
``` 
Then you should see this in your browser

<img src="/img/jsonscreen.png" width="400" >


## Deploy to an online host

So far everything has been going on on your local computer.    

In order to make our new website realy useful, we need to making it accessable to the rest of the world.    

### Heroku

Create an account at [Heroku](https://www.heroku.com/)

Create a new app.    

### Github

Create a [Github](https://github.com/) account and create a new repository and call it firstwebserver.

In the folder on your computer create a file and call it **Procfile** (spell it exatly like this and don´t put any extension).    

add this to the file

```javascript   
      web: node server.js   
```
Push your _server.js_ file and the _Procfile_ to your github repository.

## Exercise: Deploy the site to heroku
#### TODO: write tutorial 
Dette gøres ved at vælge github somm deployment method efter at have oprettet et projekt på Heroku.

Derpå vil man blive bedt om at specificere et repository. Ved at klikke på 'Search' knappen, kan man få fremvist en liste af repositories der er tilknyttet en github account.

Herfra er det blot at vælge et repository, og klikke 'connect'.

Så vil der dukke et vindue op, hvori Heroku vil bede om lov til at interagere med din github account. Hvis du allerede er logget ind, er det så simpelt som at klikke på den grønne knap, ellers vil der formentlig være behov for at logge ind først.

Når dette så er gjort, er forbindelsen mellem de to accounts oprettet, og dette skridt er afsluttet.

## Connect a simple frontend HTML and JQuery app to the API

Use this [index.html](https://github.com/ElectiveNodejs/01_Tutorial_My_first_Webserver/blob/master/htmlfile/index.html) file to connect to the API.    

In order to do so, you will need to put in an extra line in the server.js file

````prettyprint javascript  
      
      res.setHeader('Access-Control-Allow-Origin', '*');
      
      res.writeHead(200, {'Content-Type': 'text/json'});
      res.end('{
          "title" : "Hello World",
          "Text" : "This is my first web api"
      }');

````   


You should just run the file on your computer.    

If your API is on your local computer it should work without any changes.    
If your API is on Heroku, you should change the URL in the index.html file to the URL of you API.

````   

 $.getJSON("http://localhost:3003/", function (data) {

````   




 ___ 
<footer align="right" style="font-size: small">(heavily inspired by http://howtonode.org/deploy-blog-to-heroku)</footer>
