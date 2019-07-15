!SLIDE bullets incremental

# Process Scheduler

* Great for running SQR, AE, XMLP, COBOL
* But wait, there's more!
* You can add more Types

!SLIDE bullets

# Shell Scripts

We have shell scripts that do:

* Interfaces
* Refresh processing
* Monitoring

!SLIDE bullets incremental

# Integrate Shell Scripts 

A wrapper script to:

* Update the Process Monitor status
* Execute the specific script
* Update the Process Monitor status

Thanks to David Kurtz for the Shell version. Powershell version on psadmin.io GitHub

!SLIDE bullets

# Add a New Script

* New Process Scheduler Type: `SHELL` or `POWERSHELL`
* New Process Definitions
* Execute through PeopleSoft and Process Monitor

!SLIDE bullets incremental

# Powershell Use Case

**ACM runs after a refresh**

1. Refresh a DB
1. Refresh SQL inserts a job in Process Monitor
1. Booted scheduler will run the ACM template

~~~SECTION:notes~~~
We wanted to run the ACM after a refresh.

Current State: We have a job scheduled at 4:00am after the refresh. Assumes the db refresh is on time and without error.

ACM Issue: You can run ACM as a scheduled job, but it expects an exported properties file to exist in PS_FILEDIR. We store our ACM templates in the DB and managing the file adds complexity. But, if we run from the command line, the ACM AE will auto-export the properties file from the db. We happen to have a powershell script that the DPK generates that will run our `_REFRESH` ACM template from the command line.

Future State: The refresh SQL will insert a new job in the process scheduler tables. Then, when the scheduler starts, it will pick up the new job. The new job is a `POWERSHELL` script that the process scheduler will run.
~~~ENDSECTION~~~