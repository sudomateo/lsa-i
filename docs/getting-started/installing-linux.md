# Installation

The installation of the tools for this course varies slightly depending on what operating system you are running. Although we are using the same tools, there are some extra steps to perform when running Windows. 

## Requirements

You'll need to be running one of the follow operating systems to follow these installation intructions.

* Windows 7 / 8 / 10
* macOS

!!! warning "Warning"
    
    In order to create a virtual machine, you will need to enable virtualization within the BIOS of your computer. This is often called Intel VT-x or AMD-V depending on your processor.

## Installing on Windows 10 (Version 1803 and above)

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

## Installing on Windows 7 / 8 / 10 (Version 1803 and below)

1. Install VirtualBox.
    1. Download and install [VirtualBox](https://www.virtualbox.org/wiki/Downloads).
    2. Reboot if necessary.
2. Install the VirtualBox Extension Pack.
    1. Download and install the [VirtualBox Extension Pack](https://www.virtualbox.org/wiki/Downloads).
    2. Reboot if necessary.
3. Install Vagrant.
    1. Download and install [Vagrant](https://www.vagrantup.com/downloads.html).
    2. Reboot if necessary.
4. Install cmder.
    1. Download the Full version of [cmder](http://cmder.net).
    2. Unzip the downloaded `cmder.zip` file.
    3. Copy the unzipped `cmder` folder to your Desktop.
5. Configure Vagrant.
    1. Run the `Cmder.exe` application located inside the `cmder` directory on your Desktop. This will open a terminal window.
    2. Run the command `mkdir lsa-i` to create a new directory named `lsa-i`.
    3. Download the [Vagrantfile](https://gist.github.com/sudomateo/7068f579591667283a4710ae82824766/archive/d12deecb525fc61302ee7bc457cdf3b6e911db6f.zip) for this course.
    4. Unzip the downloaded file.
    5. Copy the unzipped `Vagrantfile` into the `lsa-i` directory created above. The `lsa-i` directory should be inside your `cmder` folder on your Desktop. Ensure the file does not have a file extension. 
    6. Run the command `cd lsa-i` to change into the newly created `lsa-i` directory.
    7. Run the command `vagrant status` to confirm that the installation completed successfully. You should see output similar to the following.
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
