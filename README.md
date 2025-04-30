# php-mysql
This REAME will contain what I did to setup the Abyss X1 web server, PHP engine, and MySQL Server in the Linux distro Fedora 41.
It will also try to document code snippets, and general PHP/MySQL usage.

[Abyss install and setup](#abyss-x1-web-server)  
[PHP install](#php-setup)  
[Abyss and PHP together](#configuring-abyss-for-php)  
[Installing MySQL](#installing-mysql)  
[Using MySQL Monitor/Client](#using-the-mysql-client)  

### Abyss X1 Web Server
I pretty much put together pieces from [Abyss' documentation](https://aprelium.com/data/doc/2/abyssws-linux-doc-html/index.html) to install and setup Abyss. Follow this if you don't really want to read what I wrote.

#### Installing Abyss X1 Web Server
- I downloaded Abyss' Linux version from their [download page](https://aprelium.com/abyssws/download.php) and saved it in the Documents directory.
- Open the terminal, then:
  - `cd Document`
  - `tar xzfm abwsx1.tgz` *the name of the file might be different for you*
  - Abyss is now installed.
  - Do `ls` and you should see a directory called **abyssws**
 
#### Running installed Abyss Web Server
- `cd abyssws`
- Run the executable inside the directory by doing `./abyssws`
- The terminal should display something like below:
<img src="https://github.com/user-attachments/assets/60163422-52c5-478a-b439-63f11286dbf2" width=50% height=50%>

- This means that the Web Server is running. [To stop, do CTRL-C but don't stop it now]

#### Setup credentials for Abyss
- Access the Console local URL as seen in the terminal output.
- Go to your fav web browser and navigate to `http://127.0.0.1:9999`
  - Make sure it is *http* and not *https*.
- You'll be meet with a language selecion screen. Choose your prefered language.
- Then you'll be asked to provide a *Login* and *Password*
  - Once done, you'll be asked to reenter them to get into the Abyss Console.
-  You should be met with something like below:
<img src="https://github.com/user-attachments/assets/b937fb3c-97d3-449e-a1b4-0bcbfb561328" width=50% height=50%>

- Finally, with your web browser, navigate to `http://127.0.0.1:8000` to see the Abyss Welcome page which tells us that it is working.
- You should see something like below:
<img src="https://github.com/user-attachments/assets/a45b4346-24e0-45d4-92a7-77516603f60c" width=50% height=50%>

### PHP setup

#### Installing PHP
I followed [PHP's documentation](https://www.php.net/manual/en/install.unix.dnf.php) on the matter. Specifically for distros that use DNF package manager which is the case for Fedora.
- In the terminal, `sudo dnf upgrade` first. It is good practice to have the packages up to date before installing anything new.
- Now, `sudo dnf install php php-common`
- Type `y` for yes when/if needed.
- `sudo dnf install php-mysqlnd` to install utilities for connecting PHP and MySQL.
- To check if PHP is installed, do `php -v` in the terminal.

#### Configuring Abyss for PHP
I mainly followed [Abyss's documentation](https://aprelium.com/abyssws/php.html) for this. Go through the link if you prefer not to read my steps.

- With Abyss running (if not running follow [steps above](#running-installed-abyss-web-server).
- Open Abyss' console by going to `http://127.0.0.1:9999`
- Click on the 'Configure' button as seen in the picture below.  
<img src="https://github.com/user-attachments/assets/2153aee8-39fa-4671-8110-e26e7d4f3b2a" width=50% height=50%>

- Select the option 'Scripting Parameters', it should have a gear on its icon.
- You'll be met with a new window, make sure 'Enable Scripts Execution' is checked.
- Now, clikc on the **Add** button in the 'Interpreters' table.
- On the new window, set the 'Interface' option to *Fast CGI (Local - Pipes)*.
- In the 'Interpreter' field, click on Browse and go to the directory where PHP is installed.
  - For me it was `/usr/bin/php-cgi`
- Set 'Type' to *Standard*
- Make sure *Use the associated extensions to automatically update the Script Paths* is checked.
- Press *Add* button on the 'Associated Extensions' table.
  - In the 'Extension' field type `php`, and click on OK.
- Click OK again, and your 'Scripting Parameters' window should look like below:
<img src="https://github.com/user-attachments/assets/c0ee9356-3b2b-4135-a213-33bcafaf30cf" width=50% height=50%>

- Click on OK for the last time.
- Click on Restart to apply the changes.

#### Testing the configuration worked correctly
- Open any text editor and type the following on it: `<?php phpinfo() ?>`
- Save it as **phpinfo.php** in the directory: `home/user-name/Documents/abyssws/htdocs`
  - If you installed Abyss in a different directory, your location to save the file to will be different.
- Now, in a web browser navigate to `http://127.0.0.1/8000/phpinfo.php` or `http://localhost/8000/phpinfo.php`
- You should be meet with something like below:
<img src="https://github.com/user-attachments/assets/b05e4515-6a47-4425-8bbb-ce72d1135734" width=50% height=50%>

- Congrats, Abyss is configured correctly to work with PHP!

### Embeding PHP script
```
...
</head>
<body>
  <?php
  # The traditional message
  echo '<h1>Hello World!!</h1> ;
  ?>
</body>
</html>
```
### MySQL Setup and Usage

#### Installing MySQL
Followed [Fedora's documentation](https://docs.fedoraproject.org/en-US/quick-docs/installing-mysql-mariadb/) on the matter.
- `sudo dnf upgrade`
- `sudo dnf install community-mysql-server`
  - There is a chance that mariadb could be installed for whatever. These two can't coexist together so one or the other must be removed.
- Check if it is installed correctly by `mysql -V` in the terminal.
- To start MySQL server: `systemctl start mysqld`
- To check the status: `systemctl status mysqld`
- Now you'll have to configure MySQL. Start by typing in `sudo mysql_secure_installation`. It should only be done the first time you use MySQL.
  - It will guide you though a setup.
  - It's fine to say yes to everything but I've found that I like to have the minimal **password validation** so I can put in simpler password when developing. Make sure to change the validation when it goes into production.

#### Using the MySQL Client
- To use MySQL do `mysql -u root -p`
  - It will prompt you to type in your password (it will be invisible). Then your terminal will become the MySQL monitor like below:
    - <img src="https://github.com/user-attachments/assets/108291bb-ad41-4072-aa9f-12542c218d78" width=50% height=50%>

### MySQL and the SQL language
- `CREATE DATABASE IF NOT EXISTS site_db;` *creates a database called **side_db***
- `SHOW DATABASES;` *displays existing databases, there will be default databases created from installation*
- Creating MySQL users:
  - ````
    CREATE USER IF NOT EXISTS 'username'@'hostname' 
    IDENTIFIED WITH mysql_native_password BY 'password';
    ````
    - *the single quotation marks are not optional, e.g. 'katara'@'watergang' or 'userSecretPsw'*
- Giving privileges
  - ```
    GRANT SELECT, INSERT, UPDATE ON site_db.*
    TO 'katara'@'watergang';
    ```
- `SHOW GRANTS FOR 'katara'@'watergang';` to see and confirm their privileges.

### Connecting PHP and MySQL
- Open you favourite text editor and type in the following:
  - ```
    <?php
    
    # Connect on 'watergang' for user 'katara'
    # with psw 'elements' to db 'site_db'
    
    # Parameters are (host, user, psw, database)
    $dbc = mysqli_connect('watergang', 'katara', 'elements', 'site_db')
    OR die(mysqli_connect_error());
    
    # Set encoding to match PHP script encoding.
    mysqli_set_charset($dbc, 'utf8');
    ```
- Save the file with the name **connect_db.php** in the parent directory of htdocs (i.e. home/user-name/Documents/abyssws) for security reasons.
- Create a new file and type in the following:
  - ```
    <?php
    # Incorporate MySQL connection script
    require('../connect_db.php');
    
    # Will diplay connection information if attempt is successful.
    if(mysqli_ping($dbc))
    {echo 'MySQL Server' .mysqli_get_server_info($dbc).
            'connected on '.mysqli_get_host_info($dbc);}
    ```
  - This time save the file in the htdocs directory with the name **require.php**
- Now go to `http://localhost/8000/require.php` to see that it works.

