# Packer templates for Ubuntu

### Overview

This repository contains templates for Ubuntu that can create Vagrant boxes
using Packer.

### Build
    make virtualbox/ubuntu1404-servox

### Integrate
First you need to add your new box to your list of vagrant boxes
    vagrant box add servox ./path/to/box

The you need to change up the `Vagrantfile` for your dev environment.
  * [Vagrant Documentation](https://docs.vagrantup.com/v2/multi-machine/index.html)

  Servox example
```ruby
config.vm.define "servox" do |servox|
	servox.vm.box = "servox"
	servox.vm.network "private_network", ip: "192.168.50.100"
	servox.vm.synced_folder "./services", "/srv/services", type: "nfs"
end
```

And here is a convenient bash script
```bash
vagrant ssh -c "docker-compose \$1"
```

  * Save it to /usr/local/bin/servox
  * chmod +x /usr/local/bin/servox

Now you can run docker compose commands without vagrant ssh'ing into the service box.
