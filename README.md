# php-mysql
This REAME will contain what I did to setup the Abyss X1 web server, PHP engine, and MySQL Server in the Linux distro Fedora 41.
It will also try to document code snippets, and general PHP/MySQL usage.

[Abyss install and setup](#abyss-x1-web-server)  
[PHP install](#php)
[Abyss and PHP together](#configuring-abyss-for-php)

### Abyss X1 Web Server
I pretty much to pieces from [Abyss' documentation](https://aprelium.com/data/doc/2/abyssws-linux-doc-html/index.html). Follow this if you don't really want to read what I wrote.

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
![abyss-terminal-output](https://github.com/user-attachments/assets/60163422-52c5-478a-b439-63f11286dbf2)
- This means that the Web Server is running. [To stop, do CTRL-C but don't stop it now]

#### Setup credentials for Abyss
- Access the Console local URL as seen in the terminal output.
- Go to your fav web browser and navigate to `http://127.0.0.1:9999`
  - Make sure it is *http* and not *https*.
- You'll be meet with a language selecion screen. Choose your prefered language.
- Then you'll be asked to provide a *Login* and *Password*
  - Once done, you'll be asked to reenter them to get into the Abyss Console.
-  You should be met with something like below:
![abyss-console](https://github.com/user-attachments/assets/b937fb3c-97d3-449e-a1b4-0bcbfb561328)
- Finally, with your web browser, navigate to `http://127.0.0.1:8000` to see the Abyss Welcome page which tells us that it is working.
- You should see something like below:  
![abyss-local-url](https://github.com/user-attachments/assets/a45b4346-24e0-45d4-92a7-77516603f60c)

### PHP

#### Installing PHP
- In the terminal, `sudo dnf upgrade` first. It is good practice to have the packages up to date before installing anything new.
- Now, `sudo dnf install php php-common`
- Type `y` for yes when/if needed.
- To check if PHP is installed, do `php -v` in the terminal.

#### Configuring Abyss for PHP
