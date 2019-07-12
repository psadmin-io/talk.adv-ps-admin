!SLIDE center subsection blue

# PeopleSoft Cluster Administration

!SLIDE bullets

# What is a PeopleSoft Cluster?

!SLIDE bullets

* Multiple connected PeopleSoft environments
* Creates seamless, connected UI
* Starting 8.56+, no longer need Interaction HUB
* TODO

~~~SECTION:notes~~~

~~~ENDSECTION~~~

!SLIDE bullets

# What does it get us?

* Consolidated Homepages and Tiles
* Remote Registry
* Federated Features
    * Search
    * Approvals
    * Notifications
    * User Personalizations
* TODO

!SLIDE bullets

# Topics Ideas

1. How to setup nodes
1. How to setup IB Network
1. How back button history works
1. Federated Push Notifications
    1. jolt failover string
    1. IB app server issue
1. Federated approvals tile
1. Federated preferences
1. UniNav Homepages/Tiles




!SLIDE center subsection grey

# Demo

~~~SECTION:guide~~~

> *Estimated Time: 10 min*

## Configure Change Assistant from the command line

        @@@powershellconsole
        PS C:\> New-Item -Path c:\psft\ca\output -ItemType Directory
        PS C:\> New-Item -Path c:\psft\ca\stage -ItemType Directory
        PS C:\> New-Item -Path c:\psft\ca\download -ItemType Directory
        
We can configure Change Assistant from the GUI, or from the command line. Since we will be configuring Change Assistant each time a new PeopleSoft Image is released, let's focus on using the command line so we can automate this process.

Let's use a script to default the common values and so we reuse the command line option for new installations.

        @@@powershellconsole
        PS C:\vagrant\\856-psadmin-delta-scripts\ca> .\configureCA.ps1 -action options -pt_version 8.56.05 -pi_version hr025
        Update Manager Options updated successfully.

> The powershell script can be modified to fit your installation patterns, but its a handy tool to simplify CA deployments.
