!SLIDE center subsection blue

# ACM

!SLIDE bullets

# ACM Overview

Automated Configuration Management is an Application Engine which configures PeopleTools in your database. ACM will read configuration defined in tables and apply that configuration to a database.

1. Configure Integration Broker
1. Deploy Search Indexes
1. Update Web Profile

~~~SECTION:notes~~~
ACM is like Puppet, for PeopleTools.
~~~ENDSECTION~~~

!SLIDE bullets

# ACM Scope

1. PeopleTools
    1. Integration Broker
    1. Search Framework
    1. Process Scheduler
    1. More!
1. Application
    1. AWE Configuration
    1. URLs
    1. ePro
    1. More!

!SLIDE bullets

# ACM Plugins

`PTEM_CONFIG` is the app engine behind Automated Configuration Management. `PTEM_CONFIG` runs ACM Plugins to configure the system.

1. Plugins are App Packages
    1. SQL
    1. PeopleCode
    1. Component Interfaces

!SLIDE bullets

# ACM Processing

There are two types of ACM Plugins: 

1. Preboot Plugins
1. Postboot Plugins

Preboot plugins can be run at anytime and do not require a running domain.

Postboot plugins require a running domain (web and app servers).

~~~SECTION:notes~~~
The DPK makes this distinction clear because each section is separate.

If the PeopleCode behind the plugin requires a domain to communicate, the plugin is a postboot plugin. E.g., configuring the Integration Broker or Search Framework requires a running web and app domain. But the Web Profile plugin is a preboot plugin because you need to configure the Web Profile before the web server starts.
~~~ENDSECTION~~~

!SLIDE bullets

# Running PTEM_CONFIG

1. Online
  1. Interactive
  1. Scheduled
1. Shell Script
1. Deployment Packages

~~~SECTION:notes~~~
There are two options to run the ACM based on what you want to accomplish. 

The online method is the best way to start and test ACM configurations. If you are running a longer ACM template, you can use the Scheduled option to run the process asynchronously. The default is Interactive, but you cannot interact with your session while the ACM template is processing.

If you are looking to use the ACM for refresh processing, you can call the ACM via shell scripts. Under `PS_HOME\utility`, the `psrunACM` scripts will show you how to call the ACM app engine. The app engine looks for a properties file under `PS_FILEDIR`, but you can override the location with the environment variable `PTEM_PROP`.

The last option is to run the ACM via Deployment Packages. We'll cover that in the DPK section. There is an important difference with the DPK and ACM. With the DPK, the ACM templates are defined in the `psft_customizations.yaml` file, not in the database. The DPK dynamically builds ACM templates from the `psft_customizations.yaml` file.
~~~ENDSECTION~~~

!SLIDE bullets

# ACM Troubleshooting

1. `PTACM_DEBUG="true"` Environment Variable
1. Use AE traces to capture the PeopleCode Execution
1. Verify Component Interface security
1. Reference the `psft_configuration.yaml` file in the DPK

~~~SECTION:notes~~~
The `psft_configuration.yaml` file has valid ACM configurations, so you can use that as a reference when building out new plugins. The Process Scheduler Config ACM plugin is not a straight forward configuration, so that's a good place to start.
~~~ENDSECTION~~~

!SLIDE bullets

# ACM on the Command Line

* Call `psae` with `PTEM_CONFIG` as the Program ID
* Use `psrunACM.bat` under `PS_HOME\utilities`
* `$SERVER ORACLE $DATABASE $USER $PASS $TEMPLATE $OPTION`
* OPTION is:
  1. EXEC - run the ACM Template
  1. IMP - Import Template
  1. EXP - Export Template

!SLIDE center subsection blue

# Demo

~~~SECTION:notes~~~
Create the _REFRESH template (clean up Search Deployment)
Run the `c:\vagrant\856-psadmin-delta-scripts\acm\refresh_db.sql` script to show a sample refresh processing for Search
~~~ENDSECTION~~~

!SLIDE bullets

# ACM and DPK

* ACM is fully supported with DPK
* Uses configuration in YAML files
* Dynamically generates ACM template files
* Does not support custom ACM Plugs App Packages

~~~SECTION:notes~~~
The ACM runs for DPK do not use the database templates, so you have to enter the ACM data in `psft_customizations.yaml`.

Also, if you have custom plugins, you need to load them into `PTEM_CONFIG` App Package. That value is hard-coded in the DPK code.
~~~ENDSECTION~~~

!SLIDE bullets

# ACM and YAML

Define Configuration

1. `component_preboot_setup_list:` Hash
1. `component_postboot_setup_list:` Hash


Define Order of Execution

1. `component_preboot_setup_order:` Array
1. `component_preboot_setup_order:` Array

!SLIDE bullets

# ACM and YAML

    @@@yaml
    component_preboot_setup_list:
      web_profile:
        run_control_id:    webprofile
        os_user:           "%{hiera('domain_user')}"

        db_settings: ...

        acm_plugin_list:
          PTWebProfileConfig:
            env.webprofilename: "%{hiera('pia_webprofile_name')}"
            env.helpurl:        "http://www.oracle.com/pls/topic/lookup?id=%CONTEXT_ID%&ctx=%{hiera('help_uri')}"

!SLIDE bullets

# Controlling ACM Runs

There are two variables that let you turn ACM on/off in YAML

1. `run_preboot_config_setup: false`
1. `run_postboot_config_setup: false`

!SLIDE bullets

# Controlling ACM Runs

1. Use Custom Facts to control ACM Runs

        @@@yaml
        run_preboot_config_setup: "%{::acm_preboot}"

1. Override fact with Environment Variable:

        @@@powershellconsole
        PS> $env:FACTER_acm_preboot="true"