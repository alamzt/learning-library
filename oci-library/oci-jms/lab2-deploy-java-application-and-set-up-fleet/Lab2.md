# Deploy a Java Application (using Linux) and Set Up a Fleet

## Introduction

This lab walks you through the steps to deploy a simple Java application in a compute instance (using Linux) and set up a new fleet in Java Management Service (JMS) and . 

Estimated Lab Time: 15 minutes

### Objectives
In this lab, you will:

- Deploying a simple Java application
- Set up a Java Management Service Fleet 
- Monitor the Java runtime(s) and Java application(s) in JMS

### Prerequisites:
- You have signed up for an account with Oracle Cloud Infrastructure and have received your sign-in credentials.
- You are using a Linux Operating system or virtual machine for this workshop.
- Access to the cloud environment and resources configured in Lab 1 

## **STEP 1**: Deploy a simple Java application 

1. Install your Oracle Linux Instance

Use the Create a VM Instance wizard to create a new compute instance. The wizard does several things when installing the instance:
    - Creates and installs a compute instance running Oracle Linux.
    - Creates a VCN with the required subnet and components needed to connect your Oracle Linux instance to the internet.
    - Creates an `ssh` key pair you use to connect to your instance.

To get started installing your instance with the **Create a VM Instance** wizard, follow these steps:
    a) From the main landing page, select **Create a VM Instance** wizard. 
    ![image of quick actions menu on the main landing page](/Lab2/images/01action-menu.png)
    The **Create Compute Instance** page is displayed. It has a section for **Placement**, **Image and shape**, **Networking**, **Add SSH keys**, and **Boot volume**.
&nbsp;
    b) Choose the **Name** and **Compartment**. Select the compartment created previously. 
    **Initial Options**
        - **Name**: `<name-for-the-instance>`
        - **Create in compartment**: `<your-compartment>`

  Enter a value for the name or leave the system supplied default.

  c) Review the Placement settings. Take the default values provided by the wizard. The following is sample data. The actual values change over time or differ in a different data center.

  **Placement**
    - **Availability domain**: AD-1 (For Free Tier, use **Always Free Eligible** option)
    - **Capacity type**: On-demand capacity
    - **Fault domain**: Oracle chooses the best placement

  d) Review the **Image and shape** settings. Take the default values provided by the wizard.

  **Image**
    - **Image**: Oracle Linux 7.9
    - **Image build**: 2020.11.10-1

  **Shape**
    - **Shape**: VM.Standard.E2.1.Micro
    - **OCPU count**: 1
    - **Memory (GB)**: 1
    - **Network bandwidth (Gbps)**: 0.48

  e) Review the Networking settings. Take the default values provided by the wizard.

  - **Virtual cloud network**: vcn-'date'-'time'
    - **Subnet**: vcn-'date'-'time'
    - **Assign a public IPv4 address**: Yes

  f) Review the **Add SSH** keys settings. Take the default values provided by the wizard.

  - Select the **Generate a key pair for me** option.
  - Click **Save Private Key** and **Save Public Key** to save the private and public SSH keys for this compute instance.

  If you want to use your own SSH keys, select one of the options to provide your public key. Put your private and public key files in a safe location. You cannot retrieve keys again after the compute instance has been created.

  g)  Review the **Boot volume** settings. Take the default values provided by the wizard. Leave all check boxes **unchecked**.

  h) Click **Create** to create the instance. Provisioning the system might take several minutes.

  You have successfully created an Oracle Linux instance.

2. Access instance via SSH
&nbsp;
    a) Open the navigation menu and click **Compute**. Under **Compute**, click **Instances**.
    &nbsp;
    ![image of console navigation to instance](/Lab2/images/console-navigation-instance.png)
    &nbsp;
    b) Click the link to the instance you created in the previous step.
    From the **Instance Details** page look under the **Instance Access** section. Write down the public IP address the system created for you. You use this IP adddress to connect to your instance.
    c) Open a **Terminal** or **Command Prompt** window.
    d) Change into the directory where you stored the ssh encryption keys you created.
    e) Connect to your instance with this SSH command
        
    ```
    ssh -i <your-private-key-file> opc@<x.x.x.x>
    ```    
    Since you identified your public key when you created the instance, this command logs you into your instance. You can now issue sudo commands to install and start your server.
&nbsp;
3. Install JDK 8 in your instance.
&nbsp;
    a) Install OpenJDK 8 using `yum`.
    ```
    sudo yum install java-1.8.0-openjdk-devel
    java -version
    ```
    b) Set `JAVA_HOME` in `.bashrc`.
    Update the file:
    ```
    vi ~/.bashrc
    ```
    In the file, append the following text and save the file:
    ```
    # set JAVA_HOME
    export JAVA_HOME=/etc/alternatives/java_sdk
    ```
    Activate the preceding command in the current window.
    ```
    source ~/.bashrc
    ```
Java is installed.

4. Build your Java application:

  a) In the **Terminal** or **Command Prompt** window, create a java file by entering this command 
  
  ```
  sudo nano HelloWorld.java
  ``` 

  b) In the file, paste the following text:
```
public class HelloWorld {
  public static void main(String[] args){
    System.out.println("This is my first program in java");
    int number=15;  
    System.out.print("List of even numbers from 1 to "+number+": ");  
    for (int i=1; i<=number; i++) {  
    //logic to check if the number is even or not  
    //if i%2 is equal to zero, the number is even  
    if (i%2==0)   
    {System.out.println(i);}
    }  
  }//End of main
}//End of HelloWorld Class
```

  c) To save the file, type **CTRL+x**. Before exiting, nano will ask you if you wish to save the file: Type **y** to save and exit, type n to abandon your changes and exit.

  d) To compile the program, type the following command and hit enter. 

  ```
  javac HelloWorld.java
  ```

  e) To run the program, type the following command and hit enter:
  ```
  java HelloWorld
  ```

  f) If all goes well, you will see the following response 
  ```
  This is my first program in java
  List of even numbers from 1 to 15
  2
  4
  6
  8
  10
  12
  14
  ```

  The java application is now deployed in your compute instance. 

## **STEP 2**: Set Up Java Management Service Fleet

1. In the Oracle Cloud Console, open the navigation menu, click **Observability & Management**, and then click **Java Management**.![image of console navigation to java management service](/Lab2/images/console-navigation-jms.png)
&nbsp;

2. Create a Fleet
  
    a) Click **Create Fleet**.![image of create fleet](/Lab2/images/create-fleet-create-new.png)
    &nbsp;
    b) In the Create Fleet dialog box, enter a name for the Fleet Name (for example, `Fleet_1`), and a description. 
    
    - Select **Create New Management Agent Configuration**.
    
    - Click **Show Advanced Options** to enter an alternative name for the management agent install key.![image of create fleet](/Lab2/images/create-fleet-example.png)
    
    &nbsp;
    c) Under **Advanced Options** 
    &nbsp;
    ![image of advanced options](/Lab2/images/create-fleet-advanced-configuration.png)
    - Deselect **Use Fleet Name** for Install Key Name then enter an alternative name for the management agent install key, for this example, enter "mgmt_agent_key". 
    &nbsp;
    - In the **Maximum Installs** field, specify a number that indicates the maximum number of installations that can be associated with the key. The default value is 1000, for this example enter **5**.
     &nbsp;
    - In the **Valid For** field, specify a number that indicates the period for which the key is valid. The default value is 1 Year. 
     &nbsp;
    - In the **Tag Fleet** section, click the dropdown and select **jms**. Under **Tag Value**, add the Fleet OCID. You can check the fleet ocid by clicking the fleet. 
      ![image of fleet ocid](/Lab2/images/fleet_ocid.png)
     &nbsp;
    - Click **Next**.You are prompted to review the fleet information and management agent configuration. If you wish to modify your choices, click **Previous**.
    &nbsp;
 
    d) Click **Create**. This creates a new fleet and a new management agent install key using the information you provided. 
     &nbsp;
    ![image of create fleet confirm creation](/Lab2/images/create-fleet-create.png) &nbsp;
    e) Click the link to download the management agent software for your host. 
     &nbsp;
     ![image of download management agent software](/Lab2/images/download-management-agent-software-new.png)
     &nbsp;

    - Click **Download** to download the response file.
    &nbsp;
       ![image of download management agent software](/Lab2/images/download-management-agent-software-os.png)
&nbsp;

**Shutdown Compute**
- Do remember to stop your compute instance after you are done running it to conserve resources and reduce charges. 
- If you are using an always free tier compute instance, there are no associated charges
## Want to Learn More?

If you encounter further issues, review the [Troubleshooting](https://docs.oracle.com/en-us/iaas/jms/doc/troubleshooting.html#GUID-2D613C72-10F3-4905-A306-4F2673FB1CD3) page.
&nbsp;
Alternatively, you may seek help for
[Fleet Management](https://docs.oracle.com/en-us/iaas/jms/doc/fleet-management.html)

&nbsp;
You may also review [Getting Help and Contacting Support](https://docs.oracle.com/en-us/iaas/Content/GSG/Tasks/contactingsupport.htm) in the OCI documentation.
&nbsp;
If you are still unable to resolve your issue, you may open a a support service request using the **Help** menu in the OCI console. 

## Acknowledgements
* **Author** - Esther Neoh, Java Management Service
* **Last Updated By/Date** - Esther Neoh, November 2021
