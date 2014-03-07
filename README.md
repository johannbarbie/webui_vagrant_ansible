37Coins web dev environment
===========================

This configuration will install the latest versions of Nginx, Node.js, Express, Yeoman, and the Yeoman Backbone.js generator. Ruby and the compass gem are installed for the yo build process.

All running on the Ubuntu 13.10 (Saucy Salamander)

Installation
------------
1. Install [Vagrant 1.3.5](http://downloads.vagrantup.com/)
2. Install [VirtualBox 4.3](https://www.virtualbox.org/wiki/Downloads)
3. Install [Ansible](http://www.ansibleworks.com/docs/intro_installation.html)

Running
-------
Running and provisioning can be handled nicely.


```
vagrant up
```
A new host key might need to be approved for ssh by tying 'yes'.
It may take up to 15 minutes to complete. 


Once you see "37web | 37web | run server ...", access the page on your host at:

```
http://192.168.111.222:9000/
```
The repository is synced to your disk, and can be accessed at src/webui/.
specifically the css file is located at src/webui/app/styles/mail.scss.
editing any file will reload the page in the browser after a few seconds.

Stop it once done:

```
ctrl+C
vagrant halt
```

Voila! You have a development enviroment with the latest and greatest Node.js, and Yeoman.

Ansible
-------
Ansible is configured to run for the vagrant host and you can see the specified private IP in `provisioning/hosts`. 

If for some reason you want to use a different IP, be aware that you will need to update the `Vagrantfile` as well as `provisioning/hosts`.

```ruby
Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  config.vm.network :private_network, ip: "192.168.111.222"
end
```

Ansible installs the following packages:
* git
* nodejs
* yeoman
* generator-angular for yeoman
* express
* nginx

The nginx services are started after provisioning takes place.

Synced Folders
--------------
By default this repo disables directory syncing. If you wish to have this environment checked in as part of the dev process you can create your source directory in the top level of the project and uncomment this line in the `Vagrantfile`:

```ruby
# config.vm.synced_folder "src/", "/home/vagrant/path/to/your/project"
```

This will sync your source folders over SSH so you can develop on your host machine.

Ansible Variables
-----------------
The file `provisioning/group_vars/all` contains configurations for your install. This will allow you to configure project directories and things like nginx hostname and the port node js will run on.

VM Configuration
----------------
For more on VM configuration options, check out the docs at [Vagrant](http://docs.vagrantup.com/v2/virtualbox/configuration.html)
