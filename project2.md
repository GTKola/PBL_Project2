# LEMP STACK IMPLEMENTATION

## *I started by creating a new EC2 instance of the t2.micro family with Ubunti 20.04 LTS (HVM) image.*

### Step 1 - Install Ngnix Web Server
 The first thing I did after creating the EC2 instance was to install the Ngnix web server.

1. Updated the server's package index

 `sudo apt update` 


 ![UpdateServerPackage](./Images2/Step1-Update_Server_Package_Index.PNG)

 Then I installed Ngnix

 `sudo apt install nginx`

 ![InstallNgnix](./Images2/Step1-Install_Nginx.PNG)

 2. I verified Ngnix installation status

 `sudo systemctl status nginx`


 3. Checking Ngnix server response to request from the internet

 ![NgnixResponse](./Images2/Step1-Nginx_ServerResponse.PNG)



 ### Step 2 - Installing MySQL


 1. Acquired and Installed MySQL serving using *apt*

 `sudo apt install mysql-server`

 ![InstallMySQL](./Images2/Step2-Install_MySQL_Server.PNG)


 2. After installing MySQL, I logged into the console and exit

 `sudo mysql`

  ![In_and_OutMySQL](./Images2/Step2-LoggedIn_MySQL_Server_Exit.PNG)

 3. Started Interactive Scripting

  `sudo mysql_secure_installation`

   ![InteractiveScripting](./Images2/Step2-Interactive_Scripting.PNG)


 4. Testing log in to MySQL console

  `sudo mysql -p`

 ![LoginTest](./Images2/Step2-Login_Test.PNG)


 ### Step 3 - Installing PHP


 1. I installed 2 PHP packages; 
    - php-fpm, which stands for “PHP fastCGI process manager”
    -  php-mysql, a PHP module that allows PHP to communicate with MySQL-based databases

  `sudo apt install php-fpm php-mysql`

  ![Install_Php](./Images2/Step3-Install_Php.PNG)



 ### Step 4 - Configuring Ngnix to use PHP Processor


 1. Created a root web directory

 `sudo mkdir /var/www/projectLEMP`

 ![CreateRootDir](./Images2/Step4-Create_RootWebDirectory.PNG)


 2. Assign ownership of the directory with the $USER environment variable

 `sudo chown -R $USER:$USER /var/www/projectLEMP`


 3. Open a new configuration file in Ngnix

  `sudo nano /etc/nginx/sites-available/projectLEMP`

 4. Activate configuration by linking to the config file from Nginx’s sites-enabled directory

 `sudo ln -s /etc/nginx/sites-available/projectLEMP /etc/nginx/sites-enabled/`

    Then verify configuration for syntax error
 `sudo nginx -t`

 ![Activate_and_TestConfig](./Images2/Step4-Activate_Test_Configuration.PNG)


 5. Disable default Ngnix Config host

 `sudo unlink /etc/nginx/sites-enabled/default`

 ![DisableNgnix](./Images2/Step4-Disable_Default_NginxHost.PNG)


 6. Reload Ngnix

 `sudo systemctl reload nginx`

    and create an index.html file in the web root /var/www/projectLEMP

 `sudo echo 'Hello LEMP from hostname' $(curl -s http://169.254.169.254/latest/meta-data/public-hostname) 'with public IP' $(curl -s http://169.254.169.254/latest/meta-data/public-ipv4) > /var/www/projectLEMP/index.html`

 ![Create_index.html](./Images2/Step4-Reload_Nginx-Create_IndexHTML_File.PNG)

 7. Open Website to verify configuration of Ngnix using Php Processor

 ![WebsiteCheck](./Images2/Step4-Website_Check.PNG)



### Step 5 - Testing php with Ngnix


 1. Open a new file within the document root

  `sudo nano /var/www/projectLEMP/info.php`

  ![info.php](./Images2/Step5-NewFile_info.php)

    and test create a test file

 `sudo nano /var/www/projectLEMP/info.php`

 ![TestFile](./Images2/Step5-Create_Test_PhpFile.PNG)


 2. Access the web page in a web browser

 ![WebPage](./Images2/Step5-WebPage.PNG)

 3. Remove the file containing details about the php server

 ![RemoveFile](./Images2/Step5-RemoveFile.PNG)


### Step 6 - Retreiving data from MySQL database with Php

 1. Connect to MySQL console

 `sudo mysql -p`

 ![ConnectMySQL](./Images2/Step6-Connect_to_MySQL.PNG)


 2. Create a new DB

 `mysql> CREATE DATABASE `example_database`;`

 ![CreateDB](./Images2/Step6-Create_New_DB.PNG)

 3. Create a new user and define permission for the new user named example_user

 `mysql> CREATE USER 'example_user'@'%' IDENTIFIED WITH mysql_native_password BY 'Pass.Word@1';`

 ![NewUser](./Images2/Step6-Define_New_UserPermission.PNG)

 4. Grant permission to new user and exit

 `mysql> GRANT ALL ON example_database.* TO 'example_user'@'%';`

 ![GrantPermission](./Images2/Step6-Grant_User_Permission.PNG)


 5. Show database 

 `mysql> SHOW DATABASES;`

 ![DB](./Images2/Step6-ShowDB.PNG)


 6. Created a test table named todo_list

  `mysql> CREATE TABLE example_database.todo_list (
    item_id INT AUTO_INCREMENT,
    content VARCHAR(255),
    PRIMARY KEY(item_id)
    );`

 ![TestTable](./Images2/Step6-TestTable.PNG)

 Add data to the table

 ` INSERT INTO example_database.todo_list (content) VALUES ("My first important item");`

 ![MoreData](./Images2/Step6-More_Data_for_ToDoList.PNG)


 7. Create a new php file with custom web root directory and add contents to it.

 `nano /var/www/projectLEMP/todo_list.php`
 
 ![CreateNewFile](./Images2/Step6-CreateNewPhpFile.PNG)

 8. Verify the todo_list web page

  ![ToDo_List](./Images2/Step6-ToDoList_WebPage.PNG)

  
