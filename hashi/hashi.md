!SLIDE center title blue

# Vagabond, ps-terraform

!SLIDE center title white

![HashiCorp Logo](../_images/HashiCorp_PrimaryLogo_Black.png)

!SLIDE center title black

![HashiCorp Products](../_images/HashiCorpSuite_OpenSource_StackGraphic.png)

!SLIDE center title white

![Vagrant Logo](../_images/vagrant_image.png)

!SLIDE center title green

# Vagrant -> Workstation

!SLIDE center title purple

![Teraform Logo](../_images/Terraform_PrimaryLogo_White.png)

!SLIDE center title green

# Terraform -> Infrastructure

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
    MOS_USERNAME=‘admin@psadmin.io’
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

[README](https://github.com/psadmin-io/ps-vagabond/blob/master/README.md)

!SLIDE bullets

# ps-terraform

* Open Source project from Dan Iverson
* Automated PI Deployments in the Cloud
* Powered by Terraform, AWS and the DPK
* https://github.com/psadmin-io/ps-terraform

!SLIDE bullets

# How does ps-terraform work?

* Builds infrastructure in the Cloud
* Runs Vagabond provisioning scripts

!SLIDES bullets

# Terraform

* https://www.terraform.io
* Safely and predictably create, change, and improve infrastructure.
* Supports multiple cloud providers 
* Command line interaction

!SLIDES bullets

# Terraform commands

    @@@console
    $ cd aws
    $ terraform init
    $ terraform plan --var-file=psterraform.tgvars
    $ terraform apply --var-file=psterraform.tfvars

!SLIDES bullets

# How to get started

1. Download Terraform
1. Configure your cloud provier (AWS is supported)
1. Clone the GitHub repo
1. Use Terraform to build

[README](https://github.com/psadmin-io/ps-terraform/blob/master/README.md)
