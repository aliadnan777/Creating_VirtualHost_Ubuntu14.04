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
* `<html>`
*  `<body>`
*    `<h1>Success The adnan.com virtual host is working!</h1>`
*  `</body>`
* `</html>`
* save and close the file with `:wq!`
* now copy the content of this file to our second site's index file
* `cp /var/www/adnan.com/public_html/index.html /var/www/dbadnan.com/public_html/index.html`
* now open this file and modify it according to need
* `vi /var/www/dbadnan.com/public_html/index.html`
* save and close the file 

### Create New Virtual Host Files

* Virtual host files are the files that specify the actual configuration of our virtual hosts and dictate how the Apache web server will respond to various domain requests
* Apache comes with a default virtual host file called 000-default.conf that we can use as a jumping off point. We are going to copy it over to create a virtual host file for each of our domains
* Start by copying the file for the first domain
* `sudo cp /etc/apache2/sites-available/000-default.conf /etc/apache2/sites-available/adnan.com.conf`
* now open the file `adnan.com.conf` in vi and change the following things
* First, we need to change the ServerAdmin directive to an email that the site administrator can receive emails through
* `ServerAdmin admin@adnan.com`
* ServerName, establishes the base domain that should match for this virtual host definition
* `ServerName adnan.com`
* ServerAlias, defines further names that should match as if they were the base name. This is useful for matching hosts you defined, like www
* `ServerAlias www.adnan.com`
* the last thing we need to change is `DocumentRoot`
* `DocumentRoot /var/www/adnan.com/public_html`
* save and close the file
* same changes required in other virtual host files

### Enable the New Virtual Host Files

* `sudo a2ensite adnan.com.conf`
* `sudo a2ensite dbadnan.com.conf`
* now restart your apache server
* `sudo service apache2 restart`
* you have to stop enginex or apche before running youe desired server

### Set Up Local Hosts File

* open local host file
* `sudo vi /etc/hosts/`
* now enter the IP address and domain name of newly made virtual host
* save and close the file

### Test Your result

* open your browser and type http://adnan.com


