!SLIDE center subsection blue

# Headless Change Assistant

!SLIDE bullets

# Change Assistant

1. Apply Change Packages
1. Create Change Package .zip Files
1. Manage PUM Environments
1. Manage Target Environments
1. PeopleTools DB Upgrades/Patches
1. Export/Import CA Databases
1. Upload Customizations

**From the command line!**

~~~SECTION:notes~~~
Change Assistant will do much more, but these are the main features when working with Selective Adoption.

CA can do application upgrades, PeopleTools upgrades/patches, custom change packages, etc.

You can run multiple instances, from different folders, at the same time. You cannot launch two CA instances from the same installation.

One installation strategy is to install a CA per-PI, or one CA per application, and keep it at the latest version.

All of the main Change Assistant functions are available from the command line. Again, very powerful for automation.
~~~ENDSECTION~~~

!SLIDE bullets

# Command Line Support

1. `-MODE UM` is for PeopleSoft Update Manager features
1. `-INI c:\path\to\config.ini` to run commands from file

        @@@powershellconsole
        .\changeassistant.bat /?

!SLIDE bullets

# Command Line Options

1. `UPLDTGT`: Upload Target database to PUM Source
1. `CPAPPLY`: Apply Previously Created (non-PRP) Change Package
1. `PTPAPPLY`: Apply a patch to your Current PeopleTools Release
1. `IMPCFG`: Import configuration
1. `IMPCUSTDATA`: Import customer data from the data file to the new PUM source
1. `EXPCUSTDATA`: Export customer data from existing PUM source and save it as a data file
1. `UPLDCUSTDATA`: Upload customer metadata and test data.

~~~SECTION:notes~~~
There are more options, but I feel these are the most valuable. These let you automate the PI provisioning process (coupled with Vagabond). And moving data between PI instances. This is important if you want to use the PUM features we'll talk about in the next section.
~~~ENDSECTION~~~

!SLIDE center subsection blue

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
~~~ENDSECTION~~~

!SLIDE center subsection blue

# Demo

~~~SECTION:guide~~~

> *Estimated Time: 10 min*

## Upload HCMLNX to PUM Source

In this exercise, you can choose to upload manually in Change Assistant or with the `configureCA.ps1` helper script.

1. From the command line, the `configureCA.ps1` demo script has an `uploaddb` action.

        @@@powershellconsole
        PS C:\vagrant\856-psadmin-delta-scripts\ca> .\configureCA.ps1 -action uploaddb -database HCMLNX

        cmdlet configureCA.ps1 at command pipeline position 1
        Supply values for the following parameters:
        PT_VERSION: 8.56.05
        PI_VERSION: hr025
        Begin to upload target infomation to PUM source:HCMWIN
        Uploading target information ...
        Uploaded target infomation to PUM source successfully.

!SLIDE bullets incremental

# Headless PT Patches and Upgrades

* PeopleTools Patches are fully headless
* PeopleTools Upgrades can be controlled headlessly

!SLIDE bullets

# Headless PT Upgrade

    @@@powershell
    if ($STEP -eq 0) {
        . set_ca_paths
        . configure_ca
        . set_new_ps_home
    }
    . apply_ptu_project
    . remove_new_ps_home

!SLIDE bullets

#  Headless PT Upgrade

    @@@powershell
    Do {
        .\changeassistant.bat -MODE UM -ACTION PTUAPPLY  `
          -TGTENV $DATABASE -UPD PTU856 -OUT c:\temp\$DATABASE-ptu856-$STEP.log `
          -WARNINGSOK Y -EXONERR Y -RESETJOB N `
          -RESUMEJOB COMPLETECONTINUE | select-string "Running"
        
        switch ($LASTEXITCODE) {
            0 { $status = "done"; break }
            1 { Write-Output    "Open Change Assistant to review the error."; Exit 1 }
            2 { Write-Host      "Manual Stop Encountered"; Exit 2 }
            3 { Exit 3 }
            Default { Exit 4 }
        }
        $STEP++
    } while ($status -eq "running")