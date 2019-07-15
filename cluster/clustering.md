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
    * User Preferences 

~~~SECTION:notes~~~

~~~ENDSECTION~~~

!SLIDE bullets

# Setting up Nodes

1. Setting up PeopleSoft Interaction Hub with PeopleSoft Applications (Doc ID 1545044.1)
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


~~~SECTION:notes~~~
~~~ENDSECTION~~~

# CheckToken

1. IN web profile - auth sites
    1. CheckToken - Allow Domain Compare 
1. LB issues
    1. Fixed in 8.57.05?
    1. Disable in Web PRofile (WebCheckToken)
    1. E-PIA: PT 8.56x SSO Troubleshooting Tips due to CheckTokenID feature (Doc ID 2427220.1)


~~~SECTION:notes~~~

~~~ENDSECTION~~~


!SLIDE bullets

# Setting up IB Network

1. TODO
1. This sets up SSO security?!
1. Also a lot of Service Operations

~~~SECTION:notes~~~

~~~ENDSECTION~~~

!SLIDE bullets

# User Security

* Needs to be in both DBs
* Needs security to SSOTester iScript

~~~SECTION:notes~~~

~~~ENDSECTION~~~

!SLIDE bullets

# Unified Navigation

~~~SECTION:notes~~~

~~~ENDSECTION~~~

!SLIDE center subsection grey

# Demo

~~~SECTION:notes~~~

* 

~~~ENDSECTION~~~