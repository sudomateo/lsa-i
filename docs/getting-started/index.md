# Overview

In this course we will be using the CentOS Linux distribution. [CentOS](https://www.centos.org/) is essentially a free clone of Red Hat Enterprise Linux whose development is sponsored by Red Hat, Inc. Since CentOS and Red Hat Enterprise Linux are so similar, they are often both referred to as Enterprise Linux or just "EL". CentOS is a popular choice for companies using Linux in a production environment due to its focus on stability and lengthy support periods.

To run the CentOS operating system as a virtual machine, we will be using [VirtualBox](https://www.virtualbox.org/). Virtualbox is a virtual machine hypervisor used to install and use multiple operating systems on your workstation. 

In order to provide a standard virtual machine image of CentOS for this course, we will be using [Vagrant](https://www.vagrantup.com/). Vagrant is a program developed by [HashiCorp](https://www.hashicorp.com/) designed to manage the entire lifecycle of virtual machines running on your workstation.

In short, Vagrant will configure the CentOS machine to run on VirtualBox. This will eliminate the need to download any ISOs and manually install CentOS. If you're comfortable running basic commands on the command line, using Vagrant should be a breeze.
