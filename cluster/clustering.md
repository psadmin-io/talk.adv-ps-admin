!SLIDE center subsection blue

# Clustered Applications

!SLIDE bullets

# What is a PeopleSoft Cluster?

* Multiple connected PeopleSoft environments
* Creates seamless, connected UI
* Starting 8.56+, no longer need Interaction HUB

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
    * User Preferences 

~~~SECTION:notes~~~

~~~ENDSECTION~~~

!SLIDE bullets

# Setting up Nodes

* "Setting up Interaction Hub..." Doc
    *  Doc ID 1545044.1
* Node config even more important 
* Both Local and Portal Host Nodes
* Set CheckToken and have a strong password/cert

~~~SECTION:notes~~~
1. In HUB (Gateway)
    1. HUB/EMPL
        1. Portal Host Node = unchecked
        1. Network NOde Name = ' '
    1. FMS
        1. Portal Host Node = checked
        1. Network NOde Name = ' '
    1. ERP
        1. Portal Host Node = checked
        1. Network NOde Name = 'FMS'
1. In FMS (Content Provider)
    1. HUB/EMPL
        1. Portal Host Node = unchecked
        1. Network NOde Name = ' '
    1. FMS
        1. Portal Host Node = checked
        1. Network NOde Name = ' '
    1. ERP
        1. Portal Host Node = checked
        1. Network NOde Name = 'FMS' 

~~~ENDSECTION~~~

!SLIDE bullets

# CheckToken

* read this...
    * https://psadmin.io/2017/10/25/understanding-the-check-token-id-in-peopletools-8-56/

~~~SECTION:notes~~~

~~~ENDSECTION~~~

!SLIDE bullets

# CheckToken

* ... or not and disable.
    * Web Profile custom property
        WebCheckToken=false
    * E-PIA: PT 8.56x SSO Troubleshooting Tips due to CheckTokenID 
        Doc ID 2427220.1

!SLIDE bullets

# IB Node Network

* More than just managing/monitoring now
* Used by different federated features
* Auto configures multiple things
    * SSO
    * Service Operations
    * Routings

~~~SECTION:notes~~~

~~~ENDSECTION~~~

!SLIDE bullets

# User Security

* Needs to be in both DBs
* Needs security to SSOTester iScript
    TODO - what is the exact script name and delivered security

~~~SECTION:notes~~~

~~~ENDSECTION~~~

!SLIDE bullets

# Unified Navigation

* Homepages and Tiles combine
* Recent Places
* Back Button
* Search
* Navigation

~~~SECTION:notes~~~

~~~ENDSECTION~~~

!SLIDE center subsection grey

# Demo

~~~SECTION:notes~~~

~~~ENDSECTION~~~

!SLIDE supplemental guide

# Clustered Applications Demo

* Node setup
* Show CheckToken setting on node and disable in WebProfile
* IB Node Network
    * show list, unadd FN
    * show sso setup and node routing count
    * add FM
    * show sso setup and node routing count
* User Security
    * TODO
* Uni Nav
    * Show homepage/tile merge
        * TODO how best to do this?
    * Show remote nav
    * Show recent places
    * Show Node switch in URL hack
