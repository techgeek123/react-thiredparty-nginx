# Webservers - Nginx

## Learning Competencies
- Introduction to Webserver
- Overview of Apache and Nginx
- Start/Stop server and reload configuration
- Configuring Nginx server
  - Nginx configuration files
- Handling nginx log

## Overview

### What's a webserver?
[Wiki says](https://en.wikipedia.org/wiki/Web_server)
> Web server refers to server software, or hardware dedicated to running said software, that can serve contents to the World Wide Web. A web server process incoming network requests over the HTTP protocol (and several other related protocols).
[From MDN](https://developer.mozilla.org/en-US/docs/Learn/Common_questions/What_is_a_web_server)
> At the most basic level, whenever a browser needs a file which is hosted on a web server, the browser requests the file via HTTP. When the request reaches the correct web server (hardware), the HTTP server (software) accepts request, finds the requested document (if it doesn't then a 404 response is returned), and sends it back to the browser, also through HTTP.

### Nginx vs Apache
The [Apache HTTP server and NGINX](https://www.nginx.com/blog/nginx-vs-apache-our-view/) are the two most popular open source web servers powering the Internet today.

### Installation

#### MacOS

Check out this awesome [medium blog post](https://medium.com/@ThomasTan/installing-nginx-in-mac-os-x-maverick-with-homebrew-d8867b7e8a5a). This uses a package manager Homebrew. Make sure you have HB installed

#### Linux or other Debian systems
- **Step 1** − Open the command terminal on Ubuntu desktop and run the following command.

     sudo apt-get update  

This first ensures that all packages on the operating system are up to date.

- **Step 2** − Next enter the following command to install the nginx server.

     sudo apt-get install nginx

- **Step 3** − Once done, if we run **ps –ef | grep nginx**, we can see the process for the web server in a running state.


 To start nginx, run the executable file. Once nginx is started, it can be controlled by invoking the executable with the -s parameter. Use the following syntax:

    nginx -s signal

Where signal may be one of the following:

    stop — fast shutdown
    quit — graceful shutdown
    reload — reloading the configuration file
    reopen — reopening the log files

For example, to stop nginx processes with waiting for the worker processes to finish serving current requests, the following command can be executed:

    nginx -s quit

    This command should be executed under the same user that started nginx.

Changes made in the configuration file will not be applied until the command to reload configuration is sent to nginx or it is restarted. To reload configuration, execute:

    nginx -s reload

Once the master process receives the signal to reload configuration, it checks the syntax validity of the new configuration file and tries to apply the configuration provided in it. If this is a success, the master process starts new worker processes and sends messages to old worker processes, requesting them to shut down. Otherwise, the master process rolls back the changes and continues to work with the old configuration. Old worker processes, receiving a command to shut down, stop accepting new connections and continue to service current requests until all such requests are serviced. After that, the old worker processes exit.

A signal may also be sent to nginx processes with the help of Unix tools such as the kill utility. In this case a signal is sent directly to a process with a given process ID. The process ID of the nginx master process is written, by default, to the nginx.pid in the directory /usr/local/nginx/logs or /var/run. For example, if the master process ID is 1628, to send the QUIT signal resulting in nginx’s graceful shutdown, execute:

    kill -s QUIT 1628

For getting the list of all running nginx processes, the ps utility may be used, for example, in the following way:

    ps -ax | grep nginx


### Nginx Configuration files

#### Technical Content

Nginx consists of modules which are controlled by directives specified in the configuration file. Directives are divided into simple directives and block directives. A simple directive consists of the name and parameters separated by spaces and ends with a semicolon (;). A block directive has the same structure as a simple directive, but instead of the semicolon it ends with a set of additional instructions surrounded by braces ({ and }). If a block directive can have other directives inside braces, it is called a context (**examples: events, http, server, and location**).

Directives placed in the configuration file outside of any contexts are considered to be in the main context. The ```events``` and ``http`` directives reside in the main context, server in http, and location in server.

The rest of a line after the *#*  sign is considered a comment. 

## Exploration
- [How to Configure NGINX by Linode](https://www.linode.com/docs/web-servers/nginx/how-to-configure-nginx/)
- [What is ngnix and how it works](https://www.atulhost.com/nginx)
- [nginx jobs](https://www.glassdoor.co.in/Jobs/NGINX-Jobs-E1009251.htm) See the requirement and understand they are looking for
- [Nginx vs Apache](https://www.itworld.com/article/2695421/choosing-a-linux-web-server-nginx-vs-apache.html)
- Nginx tutorials: [Eduonix](https://www.eduonix.com/courses/Software-Development/practical-nginx-the-zero-to-hero-guide), [From Carrot.js](http://carrot.is/coding/nginx_introduction)
- [Load balancing with nginx](https://nginx.org/en/docs/http/load_balancing.html), [Video tutorial](https://serversforhackers.com/s/load-balancing-with-nginx)
