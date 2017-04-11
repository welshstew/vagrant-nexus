vagrant-nexus
=============

Project to set up Sonatype Nexus via Vagrant / Puppet.

With added libvirt-ness

Quick start
-----------

* `git clone git@github.com:welshstew/vagrant-nexus.git`
* `cd vagrant-nexus`
* `git submodule init`
* `git submodule update`
* `vagrant up`
* ...wait...
* Nexus should be available on `http://192.168.42.50:8081/nexus/`

Working folder
--------------
By default, Nexus' working folder is synchronized to the host machine. This allows for some flexibility - for instance, you can recreate the Vagrant VM without losing all artifacts. If you do not want this, remove the corresponding line in `Vagrantfile`. 
