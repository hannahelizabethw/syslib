# Notes on Systems Librarianship

Using this to show how to create a GitHub repo and
how to use Git on the Linux command line.

## Installing a LAMP stack

### Installing MySQL

```
sudo apt install mysql-server
systemctl status mysql
```

#### Log in as the root user:
```
sudo su
```

Be careful when logging in as the root user

Welcome to MySQL monitor. Commands end with ; or \g.
Your MySQL connection id is 8.
Server version: 8.0.32-0ubuntu0.20.04.2 (Ubuntu)

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

```
create user 'opacuser'@'localhost' identified by 'jellyfish';
```
```
create database opacdb;
mysql> \q
Bye
root@syslib-2023:/home/hannahwilliams# exit
exit
```

## Week 8: Creating a Bare Bones OPAC

Must cd to /var/www/html before creating any of these files.

When trying to create the file called 'opacbb.html', I ran nano opacbb.html and when I tried to save it,
I got an error saying that permission was denied. Cue mild panic. So I went back to the Week 7 video
about creating PHP scripts to look for how we created the opac.php file. Ran sudo nano opacbb.html and was
able to create the file. 

Was getting an error online bc I named my file opacbb.html not opacbb.php. Ran sudo nano opacbb.html
and changed file name to opacbb.php.

## Week 10: Installing WordPress

To make sure my systems met the requirements for installing WordPress, I ran: 

```
php --version
mysql --version
```

Systems met the requirements.

Added additional PHP modules to system per Dr. Burns. Could not install
php-imagick, as it could not be found. Unsure if this was a typo.
I'm not sure how/if this will really impact my WordPress installation.

Downloaded WordPress using:
```
sudo wget https://wordpress.org/latest.tar.gz
```

Created the database and user

## Week 11: Installing Omeka

The fact that we are not getting comprehensive instructions for this makes me
**very nervous**.

Prerequisites:
1. Install ImageMagick
```
sudo apt install imagemagick
```
2. Enable Apache mod_rewrite
```
sudo a2enmod rewrite
sudo systemctl restart apache2
```
Tried to install unzip command and it didn't work. Hoping it is pre-installed
because a quick Google told me that newer Ubuntu comes with it installed.

Okay, now it's time to hopefully not f this up.

In order to not f this up, I believe I have to cd to /var/www/html,
where I will download Omeka using 
```
sudo wget https://github.com/omeka/Omeka/releases/download/v3.1/omeka-3.1.zip
```
I then ran ls to see how it downloaded. It is called omeka-3.1.zip. I will
now attempt to unzip it using 
```
sudo unzip omeka-3.1.zip
```
It did not work. Says the unzip command is not found. Looked at Element to
see if anyone else had issues with this. One person did, but no one answered
their question. Going to attempt to install again, this time while in
/var/www/html/

```
sudo apt install unzip
```
Successfully installed unzip!! Maybe had to be in /var/www/html/ before I
could install??

Will now try to unzip again:
```
sudo unzip omeka-3.1.zip
```
**Successfully unzipped!!**

Now it's time to create a new database and user in MySQL for Omeka.
While still in /var/www/html/, I need to run:
```
sudo su
mysql -u root
```
1. Create a new user for the Omeka database
2. Create a new database for Omeka
3. Grant all privileges to the new user for the new database
4. Make sure the database was created.
5. Exit MySQL
```
create user 'omeka'@'localhost' identified by 'queenoffill0ry';
create database omeka;
grant all privileges on omeka.* to 'omeka'@'localhost';
show databases;
\q
```
Database successfully created.

Getting out of the root user by typing ```exit```

Back in /var/www/html/

Changed omeka-3.1 to omeka using:
```
sudo mv omeka-3.1 omeka
```
```
cd omeka
ls
```
Need to open db.ini and enter credentials.
```
sudo nano db.ini
```
host     = "localhost"
username = "omeka"
password = "queenoffill0ry"
dbname   = "omeka"
prefix   = "omeka_"
charset  = "utf8"
;port     = ""

To change file ownership, went to /var/www/html/omeka/files and ran:
```
sudo chown -R www-data:www-data *
```
Now to restart Apache2 and MySQL and hope everything worked okay.
```
sudo systemctl restart apache2
sudo systemctl restart mysql
```
I went to my IP address to continue the install and was met with an
Installation Error message. The dom PHP extension is required for Omeka to
run. So now I have to go back and figure out what I did wrong. 

Then thought maybe the db.ini file need to be a .php file, so I made a copy
named db.php. That didn't work, so I asked the Technical Help chat on Element.
They suggested I need to run the php extras, so I did that will still in
/var/www/html/omeka. Restarted apache2 and mysql and reloaded my browswer,
and got the right thing!

## Week 12: Installing Koha

After creating the new VM and connecting to the server, in order to update 
the system, I ran
```
sudo apt update
sudo apt upgrade
sudo apt autoremove -y && sudo apt clean
sudo apt install gnupg2
sudo reboot now
```
Logging in as root user to add Koha Repository
```
sudo su
```
Adding Koha repository:
```
echo 'deb http://debian.koha-community.org/koha stable main' | sudo tee /etc/apt/sources.list.d/koha.list
wget -q -O- https://debian.koha-community.org/koha/gpg.asc | sudo apt-key add -
```
Installing Koha
```
apt update
apt show koha-common
apt install koha-common
```

Configure Koha

```
cd /etc/koha
nano koha-sites.conf
```
change INTRAPORT ='80' TO INTRAPORT = '8080'

cd to get home and then install mysql

```
cd
apt install mysql-server

## Working with Koha

I made one MARC record from scratch and that took me absolutely way too long.
I need to figure out a way to do copy-cataloging because I am lazy.

 

## Random Notes

If you are trying to get out of something and there are no obvious exit commands or prompts,
try using 'q' to exit.

Because I can never remember how to push my notes back to GitHub:

```
git add filename
git commit -m "message"
git push origin main
```

