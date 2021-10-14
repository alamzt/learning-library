# Setting Up Oracle Cloud Infrastructure for Java Management Service

Before you can use the Java Management Service (JMS), you must ensure that your Oracle Cloud Infrastructure environment is set up correctly to allow the agent and supporting services to work with JMS.

This section describes the steps to set up your Oracle Cloud Infrastructure tenancy for the Java Management Service. You may choose to use either the Onboarding Wizard or the Manual Setup Route to configure OCI. 

Before you begin, review the prerequisites and the overview of the steps. 

Estimated Lab Time: 15 min

### Objectives

Successful onboarding to Java Management Service using the:

**Onboarding Wizard** (Recommended)
1. Sign in to Oracle Cloud Infrastructure.
2. Activate the Onboarding Wizard.
3. Ensure that the resources are created.

**or**

**Manual Setup** (Start with STEP 2)
1. Sign in to Oracle Cloud Infrastructure.
2. Create a compartment for your JMS resources.
3. Create a new tag namespace.
4. Create a new tag key.
5. Create a user group for your JMS users.
6. Create one or more user accounts for your JMS users.
7. Create policies for your user group to access and manage JMS fleets, management agents, and agent install keys, metrics, and tag namespaces.
8. Create a dynamic group of all agents.
9. Create policies for agent communication.
&nbsp;

### Prerequisites
You will need a free-tier OCI account to complete this lab. If you do not have one, you may sign up [here](https://www.oracle.com/cloud/free/).

## **STEP 1**: Onboarding Wizard

### Activate the Onboarding Wizard (Recommended for first-timers)
1. Sign in to the Oracle Cloud Console as an administrator using the credentials provided by Oracle, as described in [Signing into the Console](https://docs.oracle.com/en-us/iaas/Content/GSG/Tasks/signingin.htm).
See [Using the Console](https://docs.oracle.com/en-us/iaas/Content/GSG/Concepts/console.htm) for more information.
&nbsp;

2. In the Oracle Cloud Console, open the navigation menu and click **Observability & Management**. Click **Java Management**.
![image of console navigation to java management](/Lab1/images/console-navigation-java-management.png)
    a) Select the root compartment where a new compartment will be created by the Onboarding Wizard.
    
    b) Click on the **Inspect Prerequisites** button.
    ![image of fleets main page](/Lab1/images/fleets-main-page.png)

    c) Click **Allow** and the Onboarding Wizard will install all necessary prerequisites in OCI that JMS needs.
    ![image of fleets setup message](/Lab1/images/fleets-setup-jms.png)

    d) You will see a message informing you that the prerequisites have been successfully set-up.
    ![image of fleets setup success message](/Lab1/images/fleets-jms-success.png)


### Ensure that resources are created (Optional)

3. You can check that the prerequisites have been created through your OCI console.

    a) In the Oracle Cloud Console, open the navigation menu and click **Identity & Security**. Under **Identity**, click **Compartments**.
    ![image of console navigation to compartments](/Lab1/images/console-navigation-compartments.png)

    b) You can see the new compartment labelled `Fleet_Compartment` that was created by the Onboarding Wizard.
    ![image of new compartment](/Lab1/images/new-compartment.png)

    c) In the Oracle Cloud Console, open the navigation menu and click **Identity & Security**. Under **Identity**, click **Groups**.
    ![image of console navigation to groups](/Lab1/images/console-navigation-groups.png)

    d) You can see the new user group labelled `FLEET_MANAGERS`.
    ![image of new group](/Lab1/images/new-group.png)

    e) In the Oracle Cloud Console, open the navigation menu and click **Identity & Security**. Under **Identity**, click **Dynamic Groups**.
    ![image of console navigation to dynamic groups](/Lab1/images/console-navigation-dynamic-groups.png)

    f) You can see the new dynamic group labelled `JMS_DYNAMIC_GROUP`.
    ![image of new group](/Lab1/images/new-dynamic-group.png)

    g) In the Oracle Cloud Console, open the navigation menu and click **Identity & Security**. Under **Identity**, click **Policies**.
    ![image of console navigation to policies](/Lab1/images/console-navigation-policies.png)

    h) You can see the new policy labelled `JMS_Policy`.
    ![image of new jms policy](/Lab1/images/new-jms-policy.png)

    i) In the Oracle Cloud Console, open the navigation menu and click **Governance & Administration**. Under **Governance**, click **Tag Namespaces**.
    ![image of console navigation to tag namspaces](/Lab1/images/console-navigation-tag-namespaces.png)

    j) You can see the new tag namespace and tag key.
    ![image of new tag namspace and tag key](/Lab1/images/new-tag-namespace.png)


## **STEP 2**: Manual Setup (Optional if already completed STEP 1)
### Create Compartment

1. Sign in to the Oracle Cloud Console as an administrator using the credentials provided by Oracle, as described in [Signing into the Console](https://docs.oracle.com/en-us/iaas/Content/GSG/Tasks/signingin.htm).
See [Using the Console](https://docs.oracle.com/en-us/iaas/Content/GSG/Concepts/console.htm) for more information.
&nbsp;

2. Create a compartment for your JMS resources.

    When you sign up for OCI, Oracle creates your tenancy with a root compartment that holds all of your cloud resources. You can think of the root compartment like the root folder in a file system. Oracle recommends that you set up a dedicated compartment for each project so you can associate a compartment with a particular activity or task.
    &nbsp;
    a. In the Oracle Cloud Console, open the navigation menu and click **Identity & Security**. Under **Identity**, click **Compartments**.
    ![image of console navigation to compartments](/Lab1/images/console-navigation-compartments.png)
    &nbsp;
    b. Click **Create Compartment**.
    ![image of compartments main page](/Lab1/compartments-main-page.png)
    &nbsp;
    c. In the Create Compartment dialog box, enter a name for the compartment (for example, `Fleet_Compartment`), and a description. The compartment name is required when you create policies. (See later.)
    &nbsp;
    d. Specify the parent compartment: select the root compartment for your tenancy from the drop-down list.
    ![image of create compartments page](/Lab1/images/compartment-create-example.png)
    &nbsp;
    e. Click **Create Compartment**.
    &nbsp;
    f. Find your new compartment in the table of compartments, then hover over the compartment's OCID. Click **Copy** to copy the OCID into the clipboard and then paste it into a text editor. You will require it in a later step.
    &nbsp;
    ![image of compartments main page after creation](/Lab1/images/compartment-main-page-after-create.png)
    &nbsp;
    For more information, see [Setting Up Your Tenancy](https://docs.oracle.com/en-us/iaas/Content/GSG/Concepts/settinguptenancy.htm) and [Managing Compartments](https://docs.oracle.com/en-us/iaas/Content/Identity/Tasks/managingcompartments.htm). 
&nbsp;

### Create Tag Namespace

3. Create a new tag namespace.

    a. In the Oracle Cloud Console, open the navigation menu and click **Governance & Administration**. Under **Governance**, click **Tag Namespaces**.
    ![image of console navigation to tag namespaces](/Lab1/images/console-navigation-tag-namespaces.png)
    &nbsp;
    b. Click **Create Namespace Definition**.
    ![image of tag namespaces main page](/Lab1/images/tag-namespaces-main-page.png)
    &nbsp;
    c. In the Create Namespace Definition dialog box select the root compartment for your tenancy from the drop-down list.
    &nbsp;
    d. In the Namespace Definition Name field, enter `jms`.
    &nbsp;
    e. In the Description field, enter `For OCI Java Management use only`.
    ![image of tag namespaces create page](/Lab1/images/tag-namespaces-create-example.png)
    &nbsp;Install Spring Boot on an Oracle Linux Instance
    f. Click **Create Namespace Definition**.
    &nbsp;
    For more information, see [Managing Tags and Tag Namespaces](https://docs.oracle.com/en-us/iaas/Content/Tagging/Tasks/managingtagsandtagnamespaces.htm).
    &nbsp;

4. Create a new tag key definition in the new tag namespace.
    a. In the Oracle Cloud Console, open the navigation menu and click **Governance & Administration**. Under **Governance**, click **Tag Namespaces**.
    &nbsp;
    b. From the list of namespaces, click **jms**.
    ![image of tag namespaces main page after creation](/Lab1/images/tag-namespaces-main-page-after-creating.png)
    &nbsp;
    c. Click **Create Tag Key Definition**.
    &nbsp;
    d. In the Create Tag Key Definition dialog box, enter the name for the new tag key: `fleet_ocid` and its description: `Use to tag a management agent with JMS fleet membership.`.
    ![image of tag key create page](/Lab1/images/tag-namespaces-jms-tag-key-definition.png)
    &nbsp;
    e. Click **Create Tag Key Definition**.
    &nbsp;

### Create User Group

5. Create a user group.
    a. In the Oracle Cloud Console, open the navigation menu and click Identity & Security. Under Identity, click Groups. 
    ![image of console navigation to groups](/Lab1/images/console-navigation-groups.png)
    &nbsp;
    b. Click **Create Group**.
    ![image of groups main page](/Lab1/images/groups-main-page.png)
    &nbsp;
    c. In the Create Group dialog box, enter a name for the group (for example, `FLEET_MANAGERS`), and a description.
    ![image of groups create page](/Lab1/images/groups-create-example.png)
    &nbsp;
    d. Click **Create**.
    &nbsp;
    For more information, see [Managing Groups](https://docs.oracle.com/en-us/iaas/Content/Identity/Tasks/managinggroups.htm).
    &nbsp;

6. Create user accounts for each of your users by following these instructions: [Adding Users](https://docs.oracle.com/en-us/iaas/Content/GSG/Tasks/addingusers.htm).
For more information, see [Managing Users](https://docs.oracle.com/en-us/iaas/Content/Identity/Tasks/managingusers.htm).
&nbsp;

### Create Policies

7. Create policies for the user group to access and manage JMS fleets, management agents, agent install keys, metrics, and tag namespaces. 
A policy allows members of a user group to access and manage OCI resources.
&nbsp;
    a. In the Oracle Cloud Console, open the navigation menu and click **Identity & Security**. Under **Identity**, click **Policies**.

    b. Click **Create Policy**.
    c. In the Create Policy dialog box, enter a name for the policy (for example, `JMS_Policy`), and a description.
    d. Select the root compartment for your tenancy from the drop-down list.
    e. Click **Show manual editor**.
    f. In the text box, enter the following statements:
    ```
        <copy>ALLOW GROUP FLEET_MANAGERS TO MANAGE fleet IN COMPARTMENT Fleet_Compartment
        ALLOW GROUP FLEET_MANAGERS TO MANAGE management-agents IN COMPARTMENT Fleet_Compartment
        ALLOW GROUP FLEET_MANAGERS TO MANAGE management-agent-install-keys IN COMPARTMENT Fleet_Compartment
        ALLOW GROUP FLEET_MANAGERS TO READ METRICS IN COMPARTMENT Fleet_Compartment
        ALLOW GROUP FLEET_MANAGERS TO MANAGE tag-namespaces IN TENANCY</copy>
    ```
    ![image of policies create page](/Lab1/images/policies-create-example.png)
    &nbsp;
    g. Click **Create**.
&nbsp;

### Create Dynamic Group

8. Create a dynamic group of all agents. To interact with the Oracle Cloud Infrastructure service end-points, users must explicitly consent to let the management agents work with JMS. 
    
    a. In the Oracle Cloud Console, open the navigation menu and click **Identity & Security**. Under **Identity**, click **Dynamic Groups**.
    ![image of console navigation to dynamic groups](/Lab1/images/console-navigation-dynamic-groups.png)
    &nbsp;
    b. Click **Create Dynamic Group**.
    ![image of dynamic groups main page](/Lab1/images/dynamic-groups-main-page.png)
    &nbsp;
    c. In the Create Dynamic Group dialog box, enter a name for the dynamic group (for example, `JMS_DYNAMIC_GROUP`), a description, and a matching rule.
    For **RULE 1**, enter
    ```
    ALL {resource.type='managementagent', resource.compartment.id='<fleet_compartment_ocid>'}
    ```
    Replace `<fleet_compartment_ocid>` with the OCID of the compartment that you created in step 2. (You should have pasted it into a text editor.) 
    ![image of dynamic groups create page](/Lab1/images/dynamic-groups-create-example.png)
    &nbsp;
    d. Click **Create**.
For more information, see [Managing Dynamic Groups](https://docs.oracle.com/en-us/iaas/Content/Identity/Tasks/managingdynamicgroups.htm). 
&nbsp;

### Create Policies for JMS Agent

9. Create policies for agent communication. 
    These policies allow the management agents to interact with JMS, upload data to OCI Monitoring service, and use tag namespaces.

    a. In the Oracle Cloud Console, open the navigation menu and click **Identity & Security**. Under **Identity**, click **Policies**.
    b. Click **Create Policy**.
    c. In the Create Policy dialog box, enter a name for the policy (for example, `JMS_Agent_Policy`), and a description.
    d. Select the root compartment for your tenancy from the drop-down list.
    e. Click **Show manual editor**.
    f. In the text box, enter the following statements:
    ```
    <copy>ALLOW DYNAMIC-GROUP JMS_DYNAMIC_GROUP TO MANAGE management-agents IN COMPARTMENT Fleet_Compartment
    ALLOW DYNAMIC-GROUP JMS_DYNAMIC_GROUP TO USE METRICS IN COMPARTMENT Fleet_Compartment
    ALLOW DYNAMIC-GROUP JMS_DYNAMIC_GROUP TO USE tag-namespaces IN TENANCY</copy>
    ```
    ![image of create jms policy page](/Lab1/images/policies-jms-create-example.png)
    &nbsp;
    g. Click **Create**.

## Want to Learn More?

You may proceed to the next lab on how to setup a Fleet and a Java application.

If you encounter further issues, review the [Troubleshooting](https://docs.oracle.com/en-us/iaas/jms/doc/troubleshooting.html#GUID-2D613C72-10F3-4905-A306-4F2673FB1CD3) page.

Alternatively, you may seek help from [Getting Started with Java Management Service](https://docs.oracle.com/en-us/iaas/jms/doc/getting-started-java-management-service.html).

You may also review [Getting Help and Contacting Support](https://docs.oracle.com/en-us/iaas/Content/GSG/Tasks/contactingsupport.htm) in the OCI documentation.

If you are still unable to resolve your issue, you may open a a support service request using the **Help** menu in the OCI console.


## Acknowledgements

- **Author** - Alvin Lam, Java Management Service
- **Last Updated By/Date** - Alvin Lam, November 2021
