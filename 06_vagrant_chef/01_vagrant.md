!SLIDE section_slide
# Vagrant

## A Remote Control for VirtualBox



!SLIDE section_slide
# Some Examples



!SLIDE code_slide

# create vm with Centos 6.5

    $ vagrant init box-cutter/centos65
    $ vagrant up



!SLIDE code_slide

# ssh into a running vm

    $ vagrant ssh



!SLIDE code_slide

# stop a running vm

    $ vagrant halt



!SLIDE code_slide

# delete a vm

    $ vagrant destroy



!SLIDE section_slide

# Vagrant Terminology

* Host and Guest
* Boxes
* Providers
* Provisioners
* Shared / Synced Folders
* Vagrantfile



!SLIDE

# Vagrant Boxes

## VM images with "Some Extras"

* operating system (e.g. Ubuntu)
* a sudo user `vagrant`
* an ssh server running
* a known ssh key for the vagrant user



!SLIDE

# Host &amp; Guest

* **Host** - the machine that starts Vagrant
* **Guest** - the virtual machine started by the host



!SLIDE

# Provisioner

## Strategy for HOW to provisioning your box

* Shell-Provisioner
* Chef-Provisioner
* Puppet-Provisioner
* Ansible-Provisioner



!SLIDE

# Provider

## Strategy for WHERE to provision your box

* VirtualBox (default)
* VMWare Fusion ($$$)
* Amazon AWS
* KVM



!SLIDE

# Vagrantfile

* Configures a Vagrant environment
  * which box to use
  * networking
  * shared / synced folders
  * provisioning
* It's Ruby - PANIC
* It's Ruby DSL - so DON'T PANIC

!SLIDE code_slide

    @@@ ruby
    # A most basic Vagrantfile

    Vagrant.configure(2) do |config|

      config.vm.box = "box-cutter/centos65"

    end


!SLIDE code_slide

# Basic schema of a Vagrantfile
    @@@ ruby

    Vagrant.configure('2') do |config|
      config.vm.define :box_name do |box_name|
        # Box setup
        ...
        # VM settings
        ...
        # synced folder(s)
        ...
        # Network settings
        ...
        # SSH settings
        ...
        # Provisioning settings
        ...
      end
    end



!SLIDE code_slide
# Box setup

    @@@ ruby
    Vagrant.configure('2') do |config|
      config.vm.define :box_name do |box_name|

        box_name.vm.box = 'ubuntu/precise64'
        box_name.vm.box_url = \
          "http://.../precise64.box"

        ...

      end
    end



!SLIDE code_slide
# VM settings

    @@@ ruby
    box_name.vm.provider 'virtualbox' do |v|
      v.name = 'NAME_FOR_YOUR_VM'
      v.customize [
                    'modifyvm', :id,
                    '--memory', 2048,
                    '--cpus', 1
                  ]
    end



!SLIDE code_slide
# Synced folders

    @@@ ruby
    box_name.vm.synced_folder \
      '.', '/vagrant', \
       id: 'vagrant-root', disabled: true

    box_name.vm.synced_folder \
      '.', '/var/vagrant/, \
      :nfs => true, :nfs_version => 3



!SLIDE code_slide
# Network settings

    @@@ ruby
    box_name.vm.hostname = 'boxname.vagrant.dev'
    box_name.vm.network :private_network, \
      ip: '10.20.30.50', netmask: '255.255.255.0'



!SLIDE code_slide
# SSH settings

    @@@ ruby
    box_name.ssh.forward_agent = true



!SLIDE code_slide
# Provisioning settings

    @@@ ruby
    box_name.vm.provision :shell do |s|
      s.inline = 'sudo /usr/bin/chef-client ' \
       '-z -o recipe[env_application_dev] ' \
       '-c /var/vagrant/solo.rb'
    end



!SLIDE code_slide

# Anatomy of a Vagrant project
## Provisioned by Chef
    @@@

    .
    ├── cookbooks
    ├── Gemfile
    ├── README.md
    ├── Rakefile
    ├── Vagrantfile
    └── solo.rb
