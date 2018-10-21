!SLIDE center subsection blue

# Vagabond / ps-terraform

!SLIDE bullets

# Vagabond

* Open Source project from JR Bing
* Automated PI Deployments
* Powered by Vagrant, VirtualBox and the DPK
* https://github.com/psadmin-io/ps-vagabond
* `vagrant up` and grab lunch

!SLIDE bullets

# How does Vagabond work?

* Create a new VBox VM (OEL 7 or Windows 2012 R2)
* Downloads .zip files from MOS
* Executes the DPK Bootstrap Script
* Copy in `psft_customizations.yaml` / Custom DPK Modules
* Run `puppet apply`

!SLIDE bullets

# Vagrant

* https://www.vagrantup.com
* Front-end for Virtualization Platforms
* Supports VBox, VMware, Hyper-V, AWS and more
* Command line interaction

!SLIDE bullets

# Vagrant Commands

    @@@console
    vagrant init jrbing/vagabond
    vagrant up
    vagrant provision
    vagrant halt
    vagrant ssh / vagrant rdp
    vagrant snapshot

!SLIDE bullets

# config.rb

    @@@ruby
    MOS_USERNAME=‘dan@psadmin.io’
    MOS_PASSWORD='password'
    PATCH_ID='25242817'

!SLIDE bullets

# Provisioners

* Linux  —> shell
* Windows —> 
  * download
  * bootstrap-ps
  * yaml
  * dpk-modules
  * puppet
  * client

!SLIDE bullets

# Provisioners

* Vagabond for Window can apply a PeopleTools Patch
* Download Patch .zip files
* Install Client Tools and Change Assistant
* Cleanup existing PS_HOME/Middleware
* Deploy new PS_HOME/Middleware
* Build CA Environment and apply the PTP project
* Build new domains

!SLIDE bullets

# Provisioners

* Windows —> 
  * download-ptp
  * bootstrap-ptp
  * client
  * dpk-modules
  * apply-ptp

!SLIDE bullets

# Advanced config.rb

    @@@ruby
    OPERATING_SYSTEM = 'WINDOWS'
    APPLY_PT_PATCH='true'
    PTP_PATCH_ID='26201347'
    DPK_ROLE = '::io_role::io_tools_demo'
    FQDN='psvagabond'
    CA_SETTINGS = {
      :setup  => 'true',
      :path   => 'C:\Program Files\PeopleSoft\Change Assistant',
      :type   => 'upgrade', # new upgrade uninstall
      :backup => 'backup' # backup nobackup
    }
    PTF_SETUP = ‘true'

!SLIDE bullets

# How to get started

* Install VirtualBox
* Install Vagrant
* Clone/Download the Git Repository 
  * `git clone https://github.com/psadmin-io/ps-vagabond pi-hr-022`
* Enter your MOS Credentials/Patch ID in `config.rb`
* `vagrant up`