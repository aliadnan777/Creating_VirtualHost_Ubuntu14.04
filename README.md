# Creating_VirtualHost_Ubuntu14.04

### install apache

* first install apache on your server by using following commands
* `sudo apt-get update`
* `sudo apt-get install apache2`

### Create Directory Structure

* For instance, for our sites, we're going to make our directories like this:

* `sudo mkdir -p /var/www/adnan.com/public_html`
* `sudo mkdir -p /var/www/dbadnan.com/public_html`
* adnan.com and dbadnan.com are domain names that we are wanting to serve from our VPS
* VPS(Virtual private server)

### Grant Permissions

* Now we have the directory structure for our files, but they are owned by our root user. If we want our regular user to be able to modify files in our web directories, we can change the ownership by doing this
* `sudo chown -R $USER:$USER /var/www/adnan.com/public_html`
* `sudo chown -R $USER:$USER /var/www/dbadnan.com/public_html`
* We should also modify our permissions a little bit to ensure that read access is permitted to the general web directory and all of the files and folders it contains so that pages can be served correctly
* `sudo chmod -R 755 /var/www`

### Create Demo Pages for Each Virtual Host

* We're just going to make an index.html page for each site
* `vi /var/www/adnan.com/public_html/index.html`
* In this file, create a simple HTML document
* ```<html>
  <head>
    <title>Welcome to Example.com!</title>
  </head>
  <body>
    <h1>Success!  The example.com virtual host is working!</h1>
  </body>
</html>```
