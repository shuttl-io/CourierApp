# Courier Application Doc Site
The public repository for Courier's Documentation

## Installing

1. Select your platform:
    1. [Linux 64 bit](downloads.courierconfig.com/latest/linux/amd64/linux_amd64.zip)
    2. [Linux 32 bit](downloads.courierconfig.com/latest/linux/386/linux_386.zip)
    3. [Mac OS Intel](downloads.courierconfig.com/latest/darwin/amd64/darwin_amd64.zip)
    4. [Windows 64 bit](downloads.courierconfig.com/latest/windows/amd64/windows_amd64.zip)
    5. [Windows 32 bit](downloads.courierconfig.com/latest/windows/386/windows_386.zip)
2. Unzip the file
3. Execute the Courier executable in the root of this folder

## Quick Start

This tool supports both CLI interactions as well as a full GUI application. However, some administrative tasks can only be performed in the GUI application. These include things like creating an organization, or managing users. 

### Quick help

Running `courier --help` will get you help. If you want help on a specific command run `courier <command> --help`. EX `courier write --help`
 
### Creating a key for yourself
 
The first step is to create a key for your self to be able to read others secret. 
1. In the CLI: `courier keys generate --name=<key name>`
2. In the GUI: `keys > Create New`

We don't suggest that you share keys. You should generate a new key for each user and machine that needs access.

### Create an application

Next you need to have to create an application for your organization:
1. In the CLI: `courier application init`
2: In the GUI: `select organization > ... in the application list > create new`

This command creates a courier.config file that locks the ID for the application and the name to the current directory. This can safely be added to source control

### Create an environment

After you have an application you need to create an environment:
1: In the CLI: `courier env new`

### Write a configuration value

`courier config write -e <Env name> -n <Config Name EG: DB_PASSWORD> -v <Config Value EG: My password>`

### Reading

`courier config read -e <Env name>`

### Execute

`courier exec <ENV NAME> --key_id=<APPLICATION KEY ID> -- CMD`

This command will also watch for updates. If someone (or you) updates the configuration, it will notify the command of updates by an OS signal (SIGHUP). If you fail to handle this command, Courier will just restart the command. You can also chose to handle the signal to reload the configuration your self if you chose to. If you want to request a reload, you could also send the parent PID a SIGHUP signal.

## Concepts

Courier is built to help you manage, share and deploy application configuratons easily. Each user is a seperate entity that can be invited to an organization. An organization is a collection of applications. An application is meant to be a unit of code that operates in different environments. An environment is a place that your code runs in. This could be a production, QA, dev, a personal environment, etc. 
