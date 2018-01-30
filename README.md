# Encampment Installer

## How to Install

Using composer the following will download the project in the current directory. 

```
$ composer create-project badcamp/campdistro-installer:dev-master drupalcamp
```

## Docksal

This project was built with Docksal in mind. Quicker to get set up. Quicker to start working.

For instructions on how to [install docksal](https://docs.docksal.io/en/master/getting-started/env-setup/) navigate to their [docs](https://docs.docksal.io/)
where you can get more information.

### Initializing

After you have docksal all installed you can run the following command and it will install everything you need in order to get
the project working locally.

```
$ fin init 
```

Once this has been completed you should be able to access the site using [http://camp.docksal](http://camp.docksal)

**NOTE**: Make sure you only run this command once otherwise it will wipe your local database everytime.

### Status of Project

```
$ fin status
```

When everything is up you should see that all of your containers are up and running.

```
➜  camp git:(master) ✗ fin status
   Name                 Command             State             Ports           
------------------------------------------------------------------------------
camp_cli_1    /opt/startup.sh supervisord   Up      22/tcp, 9000/tcp          
camp_db_1     /entrypoint.sh mysqld         Up      0.0.0.0:32814->3306/tcp   
camp_mail_1   MailHog                       Up      1025/tcp, 80/tcp, 8025/tcp
camp_web_1    httpd-foreground              Up      443/tcp, 80/tcp           
```

### Starting a Project

To start a project

```
$ fin start
```

### Stopping a Project

```
$ fin stop
``` 

### Restarting a Project

```
$ fin restart
```

You should get something resembling the following.

```
➜  camp git:(master) ✗ fin restart
Stopping services...
Stopping camp_web_1  ... done
Stopping camp_cli_1  ... done
Stopping camp_db_1   ... done
Stopping camp_mail_1 ... done
Starting services...
Starting camp_db_1 ... 
Starting camp_mail_1 ... 
Starting camp_mail_1
Starting camp_db_1
Starting camp_cli_1 ... 
Starting camp_cli_1 ... done
Starting camp_web_1 ... 
Starting camp_web_1 ... done
Waiting for camp_cli_1 to become ready...
Waiting for camp_cli_1 to become ready...
```

### Tools

Located within this are wrappers to interact with different services. There are a few of them listed for comment

#### Composer

```
$ fin composer [arguments]
```

#### Behat

```
$ fin behat [arguments] 
```

#### PHPUnit

```
$ fin phpunit [arguments]
```

#### Drupal Console

For more information. Consult with the Documenation on Docksal.io [here](https://docs.docksal.io/en/master/tools/drupal-console/).

```
$ fin drupal [arguments]
```

#### Drush

For more information. Consult with the Documenation on Docksal.io [here](https://docs.docksal.io/en/master/tools/drush/).

```
$ fin drush [arguments]
```

### PHP Configuration

In the project are basic php.ini and php-cli.ini files. These can allow you to configure how PHP is set for your environments.

**Settings used for FPM Service**
```
.docksal/etc/php/php.ini
```

**Settings used for Command Line**
```
.docksal/etc/php/php-cli.ini
```

After making the change make sure to run a `fin restart cli` so PHP can start using the new settings that you configured.

#### XDebug

In `docksal-local.env` add the following:

```
XDEBUG_ENABLED=1
```

After run `fin restart cli` so that the settings can take effect. For more information consult with [Docksal Documentation](https://docs.docksal.io/en/master/tools/xdebug/) 
