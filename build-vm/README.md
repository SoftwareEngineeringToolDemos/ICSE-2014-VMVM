Instructions to set up VM using VirtualBox and Vagrant
------

Environment
------
__Virtual Box used:__ [nritholtz/ubuntu-14.04.1](https://vagrantcloud.com/nritholtz/boxes/ubuntu-14.04.1)  
Ubuntu 14.04.1 32-bit box with Guest Additions, Java 1.7, Ant, Maven and Git


Steps to spin-up this Virtual Machine
------

1. Download and install [Vagrant](https://www.vagrantup.com/)
2. Download and install [VirtualBox](https://www.virtualbox.org/wiki/Downloads)
3. Download _Vagrantfile_ from [build-vm](https://github.com/SoftwareEngineeringToolDemos/ICSE-2014-VMVM/tree/master/build-vm) directory to host machine.
4. Using Command Prompt (Windows) or Teminal (Linux) navigate to folder where _Vagrantfile_ is located
5. Run command "__vagrant up__"
6. Please wait for Vagrant to download the base VM box and configure it for use.
7. Files on Desktop will contain all necessary information needed to use tool VMVM.
8. If needed, in Guest Machine use credentials:  
username: __vagrant__  
password: __vagrant__



Acknowledgements
-----
https://www.digitalocean.com/community/tutorials/how-to-install-java-on-ubuntu-with-apt-get
https://vagrantcloud.com/nritholtz/boxes/ubuntu-14.04.1


