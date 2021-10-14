# Setting Up of Management Agent

## Introduction

This lab walks you through the steps to install a management agent on your compute instance host and set up tagging for the agent and compute instance to allow java usage tracker by the Java Management Service (JMS).

Estimated Lab Time: 15 minutes

### Objectives
In this lab, you will:

- Configure a response file
- Install a management agent on a Linux / Windows compute instance host
- Verify management agent
- Configure Java Usage Tracker
- Tag Management Agent and Compute Instance

### Prerequisites:
- You have signed up for an account with Oracle Cloud Infrastructure and have received your sign-in credentials.
- You are using a Linux Operating system or virtual machine for this workshop.
- Access to the cloud environment and resources configured in Lab 2 

## **STEP 1**: Configure a Response File

1. Edit response file
a) Add "CredentialWalletPassword" Parameter and assign a suitable password. 

  The password minimum length is 8 characters with the following specifications:

  - At least one lower case character (a-z)
  - At least one upper case character (A-Z)
  - At least one digit (0-9)
  - At least one special character from the following list: '!', '@', '#', '%', '^', '&', '*'
b) Save the response file as "input.rsp"
c) The last line in the file `Service.plugin.jms.download=true` will download and enable the JMS plugin 
  ![image of input rsp file](/Lab3/images/inputrsp_new.png)

2. Transfer of files to Compute Instance
 There are a few ways to transfer the management agent software and response file into the compute instance environment. 
 - can we just ask folks to use cloudshell, let's not give them too many options and then they will be stuck here to find out the options.
 - Clone a public Github Repository containing the files
 - Utilise scp (secure copy) command line functionality to securely copy the files from your local machine to the host compute instance. 
 - Download files into compute instance from an external hosted location using the wget command line functionality

## **STEP 2**: Install Management Agent

Install Management Agent (If your host is Windows, Skip to For **Windows** Section)

For **Linux**

  a) Login as a user with `sudo` privileges. 
    &nbsp;
    b) Navigate to the directory where you have downloaded the management agent software RPM file and run the following command to install the `RPM` file: 

  ```
  sudo rpm -ivh <rpm_file_name.rpm>
  ```

  For example: `sudo rpm -ivh oracle.mgmt_agent-<VERSION>.rpm`
    &nbsp;

  The output will look similar to the following: 

  ```
    Preparing... ################################# [100%]
    
    Checking pre-requisites

    Checking if any previous agent service exists
      Checking if OS has systemd or initd
      Checking available disk space for agent install
      Checking if /opt/oracle/mgmt_agent directory exists
      Checking if 'mgmt_agent' user exists
      'mgmt_agent' user already exists, the agent will proceed installation without creating a new one.
      Checking Java version
      JAVA_HOME is not set. Trying default path
      Java version: 1.8.0_231 found at /usr/bin/java
    
    Updating / installing...
        1:oracle.mgmt_agent-<VERSION>202################################# [100%]

    Executing install
      Unpacking software zip
      Copying files to destination dir (/opt/oracle/mgmt_agent)
      Initializing software from template
      Creating 'mgmt_agent' daemon
      Agent Install Logs: /opt/oracle/mgmt_agent/installer-logs/installer-log-0
      Setup agent using input response file (run as any user with 'sudo' privileges)
      Usage:sudo
      /opt/oracle/mgmt_agent/agent_inst/bin/setup.sh opts=[RESPONSE_FILE]
    Agent install successful
  ```
  The agent installation process does the following:

  - A new user called `mgmt_agent` is created. This will be the management agent user. If `mgmt_agent` user already exists, the agent installation process will use it to install the agent software.  
    &nbsp;
  - When `mgmt_agent` daemon is created, the hard and soft nofile ulimit are set to 5000.
     &nbsp;
  - All agent files are copied and installed by mgmt_agent user. The agent install base directory is the directory where the agent is installed. The directory is created as part of the agent installation process under `/opt/oracle/mgmt_agent` directory.
     &nbsp;
  - By default, the `mgmt_agent` service is enabled and started automatically after the agent installation.
     &nbsp;    

  c) Configure the management agent by running the `setup.sh` script using a response file. 

  ```
  sudo /opt/oracle/mgmt_agent/agent_inst/bin/setup.sh opts=<full_path_of_response_file>
  ```

  The output will look similar to the following: 

  ```
  sudo /opt/oracle/mgmt_agent/agent_inst/bin/setup.sh opts=<user_home_directory>/input.rsp
    Executing configure
      Generating communication wallet
      Parsing input response file
      Validating install key
      Generating security artifacts
      Registering management agent
      Configuration Logs: /opt/oracle/mgmt_agent/configure-logs
    Agent configuration successful

    Starting agent...
    Agent started successfully
    In future agent can be started by directly running: sudo systemctl start mgmt_agent
    Please make sure that you delete input.rsp or store it in a secure location.
  ```
For **Windows** 

To install the management agent software on Windows, perform the following steps:

  a) Extract the management agent software.

  Navigate to the directory where you have downloaded the management agent software `ZIP` file and unzip it to any preferred location.

  b) Login as an Administrator user and open a Command Prompt window. To install a management agent on Windows 10, you must first create a system environment variable `OVERRIDE_VERSION_CHECK` with value `true`. 
  
  c) Install and configure the management agent by running the `install.bat` script using a response file.

  ```
  installer.bat <full_path_of_response_file>
  ```

  The output will look similar to the following: 

  ```
  C:\Users\test_agent>installer.bat C:\Users\input.rsp //Need to add the additional work if using Windows 10 to bypass the checks
Checking pre-requisites

        Checking if previous agent service exists
        Checking if C:\Oracle\mgmt_agent\agent_inst directory exists
        Checking if C:\Oracle\mgmt_agent\200820.0751 directory exists
        Checking available disk space for agent install
        Checking Java version
                Java version: 1.8.0_261 found at C:\Program Files\Java\jdk1.8.0_261
 
Executing install
        Unpacking software zip
        Copying files to destination dir (C:\Oracle\mgmt_agent)
        Initializing software from template
        Creating mgmt_agent service 

Agent install successful 

Executing configure

        Parsing input response file
        Generating communication wallet
        Validating install key
        Generating security artifacts
        Registering Management Agent

The mgmt_agent service is starting....
The mgmt_agent service was started successfully.


Agent setup completed and the agent is running
In the future agent can be started by directly running: NET START mgmt_agent
Please make sure that you delete C:\Users\input.rsp or store it in secure location.
  ```

The agent installation process does the following:

  - A new directory is created as part of the agent installation process: `C:\Oracle\mgmt_agent`.
  - The agent install base directory is the directory where the agent will be installed. By default, the agent is installed under `C:\Oracle directory`. This default directory can be changed by setting the `AGENT_INSTALL_BASEDIR` environment variable before running the `install.bat` script.
  - Log files from the agent installation are located under `C:\Oracle\mgmt_agent\installer-logs` directory.

## **STEP 3**: Verify Management Agent Installation
&nbsp;
    a) In the Oracle Cloud Console, open the navigation menu, click **Observability & Management**, and then click **Agents** under **Management Agent**.![image of management agent overview](/Lab3/images/management-agent-overview.png)
&nbsp;
    b) From the Agents list, look for the agent that was recently installed. ![image of management agent list](/Lab3/images/management-agent-list.png)

## **STEP 4**: Configure Java Usage Tracker

For **Linux**:
Execute the following command:
```
VERSION=$(sudo ls /opt/oracle/mgmt_agent/agent_inst/config/destinations/OCI/services/jms/)

sudo bash /opt/oracle/mgmt_agent/agent_inst/config/destinations/OCI/services/jms/"${VERSION}"/scripts/setup.sh
```

This script creates the file `/etc/oracle/java/usagetracker.properties` with appropriate permissions. By default, the file contains the following lines:    
```
com.oracle.usagetracker.logToFile = /var/log/java/usagetracker.log
com.oracle.usagetracker.additionalProperties = java.runtime.name
```

For **Windows**:
Open a command prompt as an administrator, and run the following commands.

```
dir /b C:\Oracle\mgmt_agent\agent_inst\config\destinations\OCI\services\jms >%TEMP%\version.txt
set /p VERSION=<%TEMP%\version.txt
powershell -ep Bypass C:\Oracle\mgmt_agent\agent_inst\config\destinations\OCI\services\jms\%VERSION%\scripts\setup.ps1
```

This script creates the file `C:\Program Files\Java\conf\usagetracker.properties` with appropriate permissions. By default, the file contains the following lines:

```
com.oracle.usagetracker.logToFile = C:\ProgramData\Oracle\Java\usagetracker.log
com.oracle.usagetracker.additionalProperties = java.runtime.name
```
If successful, you should see a message similar to
```
[C:\ProgramData\Oracle\Java\] folder has been created.
[C:\ProgramData\Oracle\Java\usagetracker.log] file has been created.
[C:\ProgramData\Oracle\Java\usagetracker.log] permissions has been set.
[C:\Program Files\Java\conf\] folder has been created.
```
## **STEP 5**: Tag compute instance and mangements agent with the Fleet OCID.

  a) In the Oracle Cloud Console, open the navigation menu and click **Compute**. Under **Compute**, click **Instances**.
    ![image of console navigation to instance](/Lab3/images/console-navigation-instance.png)
    &nbsp;
  b) Select the instance created in the previous steps
  c) Click **More Actions**, then **Add Tags**.
  d) Select the `jms` tag created in the previous Lab and select `fleet_ocid` for the **Tag Key** field.
  e) Click **Add Tags**.
  f) In the Oracle Cloud Console, open the navigation menu and click **Observability & Management**. Click **Agents**.
    ![image of console navigation to agents](/Lab3/images/console-navigation-agents.png)
    &nbsp;
  g) Select the compartment that the management agent is contained in.
    ![image of agents main page](/Lab3/images/agents-main-page.png)
  h) Select the management agent to view more details.
  i) Click **Add Tags**.
    ![image of agents details page](/Lab3/images/agent-details-page.png)
  j) Select the `jms` tag created in the previous Lab and select `fleet_ocid` for the **Tag Key** field.
  k) Click **Add Tags**.

  JMS has now been linked to the management agent and will collect information on your Java runtimes. As the management agent will scan the instance periodically, the information may not appear immediately. To change the frequency, see steps 'l' to 'o'.

  l) In the Oracle Cloud Console, open the navigation menu and click **Observability & Management**. Click **Java Management**.
    ![image of console navigation to java management](/Lab3/images/console-navigation-java-management.png)
    &nbsp;
  m) Select the compartment that the fleet is in and click the fleet.
  n) Click on **Modify Agent Settings**.
    ![image of fleet details page](/Lab3/images/fleet-details-page.png)
    &nbsp;
  o) Change the **Java Runtime Discovery** and **Java Runtime Usage** to the desired value.
    ![image of modify agent settings page](/Lab3/images/fleet-modify-agent-settings.png)


If tagging and installation of management agents is successful, Java Runtimes will be indicated on the Fleet Main Page. 

![image of successful installation](/Lab3/images/successful-installation.png)

## Want to Learn More?

If you encounter further issues, review the [Troubleshooting](https://docs.oracle.com/en-us/iaas/jms/doc/troubleshooting.html#GUID-2D613C72-10F3-4905-A306-4F2673FB1CD3) page.
&nbsp;
Alternatively, you may seek help for
[Installation of Management Agents](https://docs.oracle.com/en-us/iaas/management-agents/doc/install-management-agent-chapter.html)
[JMS Plugin for Management Agents](https://docs.oracle.com/en-us/iaas/jms/doc/installing-management-agent-java-management-service.html).
&nbsp;
You may also review [Getting Help and Contacting Support](https://docs.oracle.com/en-us/iaas/Content/GSG/Tasks/contactingsupport.htm) in the OCI documentation.
&nbsp;
If you are still unable to resolve your issue, you may open a a support service request using the **Help** menu in the OCI console. 

## Acknowledgements
* **Author** - Esther Neoh, Java Management Service
* **Last Updated By/Date** - Esther Neoh, November 2021
