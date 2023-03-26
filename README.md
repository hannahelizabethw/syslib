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

## Random Notes

If you are trying to get out of something and there are no obvious exit commands or prompts,
try using 'q' to exit.

