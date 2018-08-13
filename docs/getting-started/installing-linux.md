# Installation

The installation of the tools for this course varies slightly depending on what operating system you are running. Although we are using the same tools, there are some extra steps to perform when running Windows. 

## Requirements

You'll need to be running one of the follow operating systems to follow these installation intructions.

* Windows 10
* macOS

!!! note "Note"
    You can also run a distribution of Linux such as CentOS or Ubuntu, but then you might not be the target audience for this course.

## Installing on Windows 10

1. Enable the SSH Client.
    1. Open Settings.
    2. Search for "manage optional features".
    3. Select "Manage optional features".
    4. Select "Add a feature".
    5. Install the "OpenSSH Client" feature.
    6. Reboot if necessary.
2. Install VirtualBox.
    1. Download and install [VirtualBox](https://www.virtualbox.org/wiki/Downloads).
    2. Reboot if necessary.
3. Install the VirtualBox Extension Pack.
    1. Download and install the [VirtualBox Extension Pack](https://www.virtualbox.org/wiki/Downloads).
    2. Reboot if necessary.
4. Install Vagrant.
    1. Download and install [Vagrant](https://www.vagrantup.com/downloads.html).
    2. Reboot if necessary.
5. Configure Vagrant.
    1. Open the Command Prompt.
    2. Run the command `mkdir lsa-i` to create a new directory named `lsa-i`.
    3. Run the command `cd lsa-i` to change into the newly created `lsa-i` directory.
    4. Run the command `curl -LO https://raw.githubusercontent.com/sudomateo/lsa-i/master/Vagrantfile` to download the Vagrantfile for this course.
    5. Run the command `vagrant status` to confirm that the installation completed successfully. You should see output similar to the following.
```
$ vagrant status
Current machine states:

lsa-i                     not created (virtualbox)

The environment has not yet been created. Run `vagrant up` to
create the environment. If a machine is not created, only the
default provider will be shown. So if a provider is not listed,
then the machine is not created for that environment.
```

## Installing on macOS

1. Install VirtualBox.
    1. Download and install [VirtualBox](https://www.virtualbox.org/wiki/Downloads).
    2. Reboot if necessary.
2. Install the VirtualBox Extension Pack.
    1. Download and install the [VirtualBox Extension Pack](https://www.virtualbox.org/wiki/Downloads).
    2. Reboot if necessary.
3. Install Vagrant.
    1. Download and install [Vagrant](https://www.vagrantup.com/downloads.html).
    2. Reboot if necessary.
4. Configure Vagrant.
    1. Open the Terminal application.
    2. Run the command `mkdir lsa-i` to create a new directory named `lsa-i`.
    3. Run the command `cd lsa-i` to change into the newly created `lsa-i` directory.
    4. Run the command `curl -LO https://raw.githubusercontent.com/sudomateo/lsa-i/master/Vagrantfile` to download the Vagrantfile for this course.
    5. Run the command `vagrant status` to confirm that the installation completed successfully. You should see output similar to the following.
```
$ vagrant status
Current machine states:

lsa-i                     not created (virtualbox)

The environment has not yet been created. Run `vagrant up` to
create the environment. If a machine is not created, only the
default provider will be shown. So if a provider is not listed,
then the machine is not created for that environment.
```
