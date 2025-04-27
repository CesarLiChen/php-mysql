# php-mysql
This REAME will contain what I did to setup the Abyss X1 web server, PHP engine, and MySQL Server in the Linux distro Fedora 41.
It will also try to document code snippets, and general PHP/MySQL usage.

[Abyss install and setup](#abyss-x1-web-server)  
[PHP install](#php)  
[Abyss and PHP together](#configuring-abyss-for-php)

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

### PHP

#### Installing PHP
- In the terminal, `sudo dnf upgrade` first. It is good practice to have the packages up to date before installing anything new.
- Now, `sudo dnf install php php-common`
- Type `y` for yes when/if needed.
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
