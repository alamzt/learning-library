# Utilising JMS SDK

## Introduction

This lab walks you through the steps to set up the configuration on your local host mahcine to access a Java Management Service (JMS) API. 

Estimated Lab Time: 10 minutes

### Objectives
In this lab, you will:

- Generate an API Signing Key 
- Install Oracle Cloud Interface (OCI)
- Access SDK for JMS (Java and Python Examples)

### Prerequisites:
- You have signed up for an account with Oracle Cloud Infrastructure and have received your sign-in credentials.
- You are using a Linux Operating system or virtual machine for this workshop.

## **STEP 1**: Generate an API Signing Key

If you have generated your own keys, refer to the public documentation on how to [upload them](https://docs.oracle.com/en-us/iaas/Content/API/Concepts/apisigningkey.htm) and the public key fingerprint.

a) Open the Profile menu, click the **Profile icon** and click User Settings.
![image of profile menu](/Lab4/images/user-profile.png)
&nbsp;
![image of user settings](/Lab4/images/user-settings.png)

b) Click **API Keys**
![image of create api key](/Lab4/images/api-key.png)

c) Click **Add API Key**

![image of add api key](/Lab4/images/add-api-key.png)

d) Download private and public key. Click **Add**

![image of download api key](/Lab4/images/api-key-download.png).

e) The key is added and the **Configuration File Preview** is displayed. Click **Copy** to copy the file snippets and paste it into a text file. Save the file as **config**.

The file snippet includes required parameters and values you'll need to create your configuration file. 
![image of configuration file](/Lab4/images/config-file-preview.png)

f) Create a folder called **.oci** in the Home directory and save the **config file** and **private key** there. 
![image of configuration file in .oci folder](/Lab4/images/config-file-oci-location.png)

g) Set the root user with **Read-only** permissions. No other user should have permissions. 
![image of configuration file permissions](/Lab4/images/config-file-permissions.png) 

h) An API Key is succesfully created
![image of auccessful api key creation](/Lab4/images/api-key-created.png) 


## **STEP 2**: Install OCI Command Line Interface (CLI)

For Linux and Unix

- Open a terminal.
- To run the installer script, run the following command.
```
bash -c "$(curl -L https://raw.githubusercontent.com/oracle/oci-cli/master/scripts/install/install.sh)"
```
- Respond to the Installation Script prompts

For Oracle Linux 8 

Use dnf to install the CLI
```
sudo dnf -y install oraclelinux-developer-release-el8
sudo dnf install python36-oci-cli 

```

For Oracle Linux 7 

Use yum to install the CLI
```
sudo yum install python36-oci-cli
```

Mac OS X
To install the CLI on Mac OS X with [Homebrew](https://docs.brew.sh/Installation):

```
brew update && brew install oci-cli
```

Windows
1. Open the PowerShell console using the **Run as Administrator** option.

2. The installer enables auto-complete by installing and running a script. To allow this script to run, you must enable the RemoteSigned execution policy.

To configure the remote execution policy for PowerShell, run the following command.

```
Set-ExecutionPolicy RemoteSigned
```

3. Force PowerShell to use TLS 1.2 for Windows 2012 and Windows 2016: [Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12 

4. Download the installer script:
```
Invoke-WebRequest https://raw.githubusercontent.com/oracle/oci-cli/master/scripts/install/install.ps1 -OutFile install.ps1 
```

5. Run the installer script with or without prompts:
a) To run the installer script with prompts, run the following command:
```
iex ((New-Object System.Net.WebClient).DownloadString('https://raw.githubusercontent.com/oracle/oci-cli/master/scripts/install/install.ps1'))
```
b) To run the installer script without prompting the user, accepting the default settings, run the following command:
```
install.ps1 -AcceptAllDefaults
```

#### Verify that CLI is installed

To get a namespace, run the following command.
```
oci os ns get 

```

If successful, the following will be returned, with xx as your unique namespace. 

`{
  "data": "xx"
}
`
## **STEP 3**: Access SDK for JMS
1. Access Java SDK for JMS
- Download the [SDK](https://github.com/oracle/oci-java-sdk/releases) and extract it

- Access the a sample [API](https://docs.oracle.com/en-us/iaas/api/#/en/jms/20210610/Fleet/ChangeFleetCompartment)
&nbsp;
![image of java sdk example code](/Lab4/images/java-sdk-example-code.png)

- Copy the example SDK code into a .java File in the SDK downloaded. Ensure the file path for the newly created file adheres to the sample SDK code. 
![image of java sdk filepath](/Lab4/images/java-sdk-filepath.png)

- Run it
![image of java sdk run](/Lab4/images/java-sdk-run.png)

- A response is generated
![image of java sdk output](/Lab4/images/java-sdk-response.png)


2. Access Python SDK for JMS
- Download the [SDK](https://github.com/oracle/oci-python-sdk/releases) and extract it

- Access the a sample [API](https://docs.oracle.com/en-us/iaas/api/#/en/jms/20210610/Fleet/ChangeFleetCompartment)
![image of python sdk example code](/Lab4/images/python-sample-code.png)

- Copy the example SDK code into a .py File in the SDK downloaded. Ensure the file path for the newly created file adheres to the sample SDK code. Run it
![image of python sdk example code](/Lab4/images/python-sdk-response.png)

The steps above can be applied for the Typescript, .NET, Ruby and GO SDKs

Download SDKs
[Typescript](https://github.com/oracle/oci-typescript-sdk/releases)
[.NET](https://github.com/oracle/oci-dotnet-sdk/releases)
[Ruby](https://github.com/oracle/oci-ruby-sdk/releases)
[GO](https://github.com/oracle/oci-go-sdk/releases)


## Want to Learn More?

If you encounter further issues, review the [Troubleshooting](https://docs.oracle.com/en-us/iaas/jms/doc/troubleshooting.html#GUID-2D613C72-10F3-4905-A306-4F2673FB1CD3) page.
&nbsp;
Alternatively, you may seek help for
[API Key](https://docs.oracle.com/en-us/iaas/Content/API/Concepts/apisigningkey.htm)
[SDK Configuration](https://docs.oracle.com/en-us/iaas/Content/API/Concepts/sdkconfig.htm)
[Using the CLI](https://docs.oracle.com/en-us/iaas/Content/API/SDKDocs/cliusing.htm).
[Java SDK](https://docs.oracle.com/en-us/iaas/Content/API/SDKDocs/javasdk.htm)
[Python SDK](https://docs.oracle.com/en-us/iaas/Content/API/SDKDocs/pythonsdk.htm)
[.NET SDK](https://docs.oracle.com/en-us/iaas/Content/API/SDKDocs/dotnetsdk.htm)
[Ruby SDK](https://docs.oracle.com/en-us/iaas/Content/API/SDKDocs/rubysdk.htm)
[GO SDK](https://docs.oracle.com/en-us/iaas/Content/API/SDKDocs/gosdk.htm)
[Typescript SDK](https://docs.oracle.com/en-us/iaas/Content/API/SDKDocs/gosdk.htm)
&nbsp;
You may also review [Getting Help and Contacting Support](https://docs.oracle.com/en-us/iaas/Content/GSG/Tasks/contactingsupport.htm) in the OCI documentation.
&nbsp;
If you are still unable to resolve your issue, you may open a a support service request using the **Help** menu in the OCI console. 

## Acknowledgements
* **Author** - Esther Neoh, Java Management Service
* **Last Updated By/Date** - Esther Neoh, November 2021
