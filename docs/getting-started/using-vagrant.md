# Using Vagrant

Now that we've installed the tools needed to run the Linux instance for this course, we'll take a look at how to use Vagrant to manage the entire lifecycle of the Linux virtual machine.

Vagrant relys on a Vagrantfile to function. Vagrant reads this file to determine how to configure the virtual machine. You should already have a Vagrantfile in your current directory from the installation instructions. If you delete this file by mistake, be sure to download it again.

The following sections assume that you are in the Command Prompt or Terminal and inside the directory where your Vagrantfile is located. This should be the `lsa-i` directory if you have followed the installation instructions from this course.

## `vagrant init`

The `vagrant init` command creates a default Vagrantfile in your current directory. We won't need to use this command since we already have our Vagrantfile from the installation instructions earlier.

!!! warning "Warning"
    If you run this command, you may overwrite your custom Vagrantfile. If you do that you'll have to download the custom Vagrantfile from the installation instructions.

## `vagrant status`

Running the `vagrant status` command shows you the status of your virtual machine. If you are unsure whether the virtual machine is created, started, stopped, or destroyed, this is the command to use.

!!! example "Example"
    ```
    $ vagrant status
    Current machine states:

    lsa-i                     not created (virtualbox)

    The environment has not yet been created. Run `vagrant up` to
    create the environment. If a machine is not created, only the
    default provider will be shown. So if a provider is not listed,
    then the machine is not created for that environment.
    ```

## `vagrant up`

The `vagrant up` command starts the virtual machine using the Vagrantfile as configuration. Running this command will create a virtual machine in VirtualBox and start the virtual machine. The Vagrantfile used in this course will make two disk files in your current directory to be used as supplemental hard drives for the virtual machine.

!!! example "Example"
    ```
    $ vagrant up
    Bringing machine 'lsa-i' up with 'virtualbox' provider...
    ==> lsa-i: Importing base box 'centos/7'...
    ==> lsa-i: Matching MAC address for NAT networking...
    ==> lsa-i: Checking if box 'centos/7' is up to date...
    ==> lsa-i: Setting the name of the VM: lsa1_lsa-i_1534122251344_30397
    ==> lsa-i: Clearing any previously set network interfaces...
    ==> lsa-i: Preparing network interfaces based on configuration...
        lsa-i: Adapter 1: nat
    ==> lsa-i: Forwarding ports...
        lsa-i: 80 (guest) => 8080 (host) (adapter 1)
        lsa-i: 22 (guest) => 2222 (host) (adapter 1)
    ==> lsa-i: Running 'pre-boot' VM customizations...
    ==> lsa-i: Booting VM...
    ==> lsa-i: Waiting for machine to boot. This may take a few minutes...
        lsa-i: SSH address: 127.0.0.1:2222
        lsa-i: SSH username: vagrant
        lsa-i: SSH auth method: private key
        lsa-i: 
        lsa-i: Vagrant insecure key detected. Vagrant will automatically replace
        lsa-i: this with a newly generated keypair for better security.
        lsa-i: 
        lsa-i: Inserting generated public key within guest...
        lsa-i: Removing insecure key from the guest if it's present...
        lsa-i: Key inserted! Disconnecting and reconnecting using new SSH key...
    ==> lsa-i: Machine booted and ready!
    ==> lsa-i: Checking for guest additions in VM...
        lsa-i: No guest additions were detected on the base box for this VM! Guest
        lsa-i: additions are required for forwarded ports, shared folders, host only
        lsa-i: networking, and more. If SSH fails on this machine, please install
        lsa-i: the guest additions and repackage the box to continue.
        lsa-i: 
        lsa-i: This is not an error message; everything may continue to work properly,
        lsa-i: in which case you may ignore this message.
    ==> lsa-i: Setting hostname...
    ```

## `vagrant halt`

The `vagrant halt` command stops the virtual machine without destroying anything. This is useful if you want to poweroff your workstation while saving the progress on your virtual machine. 

!!! example "Example"
    ```
    $ vagrant halt
    ==> lsa-i: Attempting graceful shutdown of VM...
    ```

## `vagrant destroy`

The `vagrant destroy` command destroys the virtual machine and all related disk files. This is useful when you want to delete everything related to your virtual machine. Common practice is to use `vagrant destroy` followed by a `vagrant up` to reset your virtual machine to a clean state. It's suggested to do this prior to the start of each section to ensure a clean virtual machine.

!!! example "Example"
    ```
    $ vagrant destroy
        lsa-i: Are you sure you want to destroy the 'lsa-i' VM? [y/N] y
    ==> lsa-i: Forcing shutdown of VM...
    ==> lsa-i: Destroying VM and associated drives...
    ```

## `vagrant ssh`

The `vagrant ssh` command is used to connect to your virtual machine via SSH. This will log you into the virtual machine and place you in the shell of the virtual machine. This is how we will connect to our virtual machine to perform work in the course. This can only be used once the virtual machine is running after using `vagrant up`.

!!! example "Example"
    ```
    $ vagrant ssh
    [vagrant@lsa-i ~]$ echo "I'm inside the virtual machine."
    I'm inside the virtual machine.
    ```
