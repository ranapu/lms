# Inshura LMS Setup and Configuration/Customization Bible
## _Introduction_
This document captures all the details about installing moodle and describes about all the configurations/customizations done as part of developing Inshura LMS. This document can be referenced when making any enahancements/changes to the Inshura LMS.
[![N|Solid](https://www.inshura.com/wp-content/uploads/2022/10/New-Inshura-logo-new.png.webp)](https://inshura.com/)

[![Build Status](https://travis-ci.org/joemccann/dillinger.svg?branch=master)](https://travis-ci.org/joemccann/dillinger)
## Moodle
This document follows the steps outlined [here](https://docs.moodle.org/404/en/Installing_Moodle) to install the moodle. LMS uses moodle ver 4.3. 

Setup 

Run the below command to enable php in apache
```sh
sudo apt update
```
## Enable HTTPS
Add the following line into ```config.php``` file
```sh
$CFG->sslproxy  = true;
```
## Configure Cron Job
The admin/cli/cron.php script has never been run and should run every 1 min. 


## Increase Upload Size Limit
### 1. Reverse proxy configuration
First increase the limit at the reverse proxy/load balancer level with help from ITS/Infra team.
### 2. Server configuration
Then update the following values in ```php.ini``` file:
```sh
upload_max_filesize = 100M
post_max_size = 100M
```
restart the apache by running the below command:
```sh
sudo service apache2 restart
```
### 3. Increase Maximum File Size Limit in Moodle
Navigate to: Site administration > Security > Site security settings
Find the setting Maximum uploaded file size and increase it to ''Site upload limit (100 MB)''.

## Customizations
### Branding and themes
Upload Inshura Logo
TODO Upload the images into git add path here. upload into compact logo also.
Copy the theme folder to install folder

Add the below line to ``/theme/boost/scss/moodle.scss`` file:
```sh
@import "moodle/custom-style";
```
Add the below code to ``Site administration -> Appearance -> Additional HTML -> Within HEAD`` section:

```sh
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Nunito:ital,wght@0,200..1000;1,200..1000&display=swap" rel="stylesheet">
```


##### 1. Customize user context menu
Replace the contents of ``Site administraion -> Appearance -> Theme settings -> User menu items`` with: 

```sh
profile,moodle|/user/edit.php
```
## Feature trimming
##### Disable Messaging Feature
Go to ``Site administration -> General -> Advanced Features`` and uncheck ``Enable messaging system`` check box. 

#### Disable Notifications Feature
Go to ``Site administration -> General -> Notification settings`` and uncheck ``Web`` and ``Mobile`` items

#### Configure Navigations
Go to ``Site administration -> Appearance -> Navigation`` and uncheck the below items:

* ``Enable Dashboard`` - This hides Dashboard from top navigation
* ``Show course categories``  - This hides course category from course listing page 

### SAML Integration
Install SAML2 Plug in
TODO Add the plug in url here
Goto Plugins->Authentication->Manage Authentication
Enable SAML2
If there is a certificate related error then try regenerate the certificate
TODO mention all the config values here

### Configure User Profile Custom Fields
TODO Copy the npn profile field to moodle folder (elaborate this step)
Add the following custom prodile fields


installing the plug in can throw some permission related error. then use the command to set permission: chmod 775 /var/www/html/auth




