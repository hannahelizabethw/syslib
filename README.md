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

#### Logging in as a Regular User

#### Week 8: Creating a Bare Bones OPAC

Must cd to /var/www/html before creating any of these files.

When trying to create the file called 'opacbb.html', I ran nano opacbb.html and when I tried to save it,
I got an error saying that permission was denied. Cue mild panic. So I went back to the Week 7 video
about creating PHP scripts to look for how we created the opac.php file. Ran sudo nano opacbb.html and was
able to create the file. 

Was getting an error online bc I named my file opacbb.html not opacbb.php. Ran sudo nano opacbb.html
and changed file name to opacbb.php.

## Random Notes

If you are trying to get out of something and there are no obvious exit commands or prompts,
try using 'q' to exit.

