!SLIDE center subsection grey

# Demo

!SLIDE supplemental guide

Tasks: 

1. Configure `SHELL` Process Type
1. Run a sample shell script

# Configure and Run a Shell Script from the Process Scheduler

1. Navigate to PeopleTools > Process Scheduler > Process Type
1. Add a new type called `Shell`
1. Select `ORACLE` as the Database Type and the Platform as `Linux`
1. Select `Other` as the Generic Process Type
1. For the Command Line, set it to `/u01/app/oracle/product/home/psadm2/psft.sh`
1. The Parameter List is where we pass all of the arguments to our wrapper script. 

    `%%DBNAME%% %%ACCESSID%% %%ACCESSPSWD%% %%INSTANCE%%`

1. Save the new Process Type

Next, we need to allow the new Process Types to run on your process scheduler.

1. Navigate to PeopleTools > Process Scheduler > Servers
1. Open your server definition (`PRCSxxxx` for me)
1. In the “Process Types run on this Server” grid, add the `Shell` Process Type and Save

Last, let’s configure the output format for the Shell Process Types.

1. Navigate to PeopleTools > Process Scheduler > System Settings
1. Click the Process Type Output tab
1. Select Other for the Process Type
1. Check the Active checkbox for “Web” and also the Default checkbox
1. Click the Process Output Format tab
1. Select Other and Web, and then check the Active and Default checkboxes for the “Text Files (.txt)” row

The wrapper script itself doesn’t do any process besides updating the Process Monitor tables. Next, let’s built a test script to verify we can run Shell scripts.

1. Navigate to PeopleTools > Process Scheduler > Processes
1. Click “Add a new value”
1. Select `Shell` as the Process Type
1. Set the Process Name to `SHSAMPLE``
1. Add a Description: Test Shell Script
1. Click the Process Definition Options tab
1. In the Process Security group box, set the Component to PRCSMULTI and the Process Group to TLSALL
1. Click the Override Option tab
1. Select “Append” for the Parameter List

    The append list is where we pass in commands that the psft.sh script will run for us. For our test script, we have one parameter to pass in addition to calling the script. We pass the database name to sample_shell.sh so it can print the database name.

    "/u01/app/oracle/product/home/psadm2/shell_sample.sh %%DBNAME%%"

    Make sure to wrap the parameter list in double quotes so that our wrapper script passes the entire string to our sample_shell.sh script.

1. Save the new Process Definition.

Last, let’s test our new SHSAMPLE process.

1. Navigate to PeopleTools > Process Scheduler > System Process Request
1. Add a new run control
1. Click the Run button
1. In the list of processes, select SHSAMPLE and verify the output is “Web” and “TXT”
1. Click OK