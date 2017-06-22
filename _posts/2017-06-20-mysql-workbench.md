---
layout: single
title: Setting up MySQL workbench and why you shouldn't
header:
    teaser: assets/images/mysql.jpeg
category: tutorial
---

## What is MySQL Workbench?

MySQL Workbench is a tool that allows you to connect to a MySQL database and run queries within an interface that is a bit nicer and more user friendly than relying on a command-line shell. If you are in the MSBA program, it is the "official" tool you'll be using to build and run your queries.

Fortunately, installing MySQL workbench and connecting to databases is pretty straightforward.

## Installation

In what is hopefully becoming a common refrain, if you're using OSX and using homebrew this is going to be extremely easy. Fire up a terminal and type:

```
brew cask install mysqlworkbench
```

If you're on Windows you can download and install from the [website](https://www.mysql.com/products/workbench/)

## Setting up a connection

To connect to a database click the plus icon and then enter in the relevant host, port, username and password information in the dialog box

![connection_window](/assets/images/mysql_connection.png){: .align-center}

**Note:** If the connection info you've been provided doesn't include a port number, it is most likely 3306, the default port for mysql
{: .notice--info}

Once you're connected you'll be taken to a screen where you can begin typing queries.

![main_window](/assets/images/mysql_window.png){: .align-center}

## A sample connection for you

If you're in the MSBA program you will have a mysql server made available to you. However, it may be desirable to have a local testing environment. We could set up a mysql server to run off our localhost, but it's a bit cleaner to use Vagrant to automagically spin up a mysql server for us. All you need is a Vagrantfile to handle the provisioning, and I happen to have one for you right [here!](https://github.com/JCPistell/msba_local_mysql) The README in the repo has the connection information.

So, there you have it. MySQL workbench up and running. If you're in the MSBA program this is the official tool you'll be using to connect to your program databases. All done!

...

you still here? 

/looks around

wanna know a secret?

I think MySQL Workbench sucks. Too many bells and whistles, the actual SQL connections are buggy, and it only works for MySQL databases which are not incredibly common as data warehouses in the real world.

There are many different clients out there and you can try them all. I'll tell you that my personal favorite is also probably the most simple: [SQL Workbench/J](http://www.sql-workbench.net/getting-started.html)

In order to get it working you'll need Java... technically you can get by with a simple JRE (Java Runtime Environment), but as burgeoning developers you'll probably want to get a JDK (Java Development Kit) installed. If you're using OSX we can once again use homebrew:

```
brew cask install java
```

Otherwise, you can start the process [here.](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)

Workbench uses JDBC drivers (Java Database Connectivity) to interact with databases. This requires that you get an appropriate JDBC driver and connect it with Workbench. The driver can be found [here](https://dev.mysql.com/downloads/connector/j/)

Unzip the archive and you'll find it contains a jar. You need to point Workbench to this jar.

After launching Workbench, select "Manage Drivers" from the Connection Window. In the next dialogue box select the new driver button in the upper left, then click the browse folder on the right. Navigate to the jdbc jar you just downloaded. The Classname should auto-populate. Click OK.

![jdbc1](/assets/images/jdbc1.png){: .align-center}

![jdbc2](/assets/images/jdbc2.png){: .align-center}

In order to connect you'll need to provide a valid connection string. The format for this is:

```
jdbc:mysql://<host>:<port>/<database>
```

An example using our Vagrant database:

![jdbc3](/assets/images/jdbc3.png){: .align-center}

The nice thing about Workbench is, once the appropriate JDBC driver has been installed it will work for any type of database. JDBC connections, in my experience, tend to be faster and less error prone than other types of connections so I think if you go to the trouble of setting it up you'll find that Workbench offers a superior (if somewhat bare-bones) SQL client experience.