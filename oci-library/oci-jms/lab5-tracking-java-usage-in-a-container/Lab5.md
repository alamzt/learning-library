# Tracking Java Usage in a Container

## Introduction
You can use Java Management Service to track Java usage in a container. If you have already installed Docker on your compute instance and already pulled a Docker container with Java, you may skip STEP 1 and start at STEP 2.

Estimated Lab Time: 10 minutes

### Objectives
In this lab, you will:

- Launch an instance using the Oracle Cloud Developer Image
- Configure Java Usage Tracker Location
- Verify Configuration


### Prerequisites
Ensure that Docker and a Management Agent has been installed in your compute instance. Refer to Lab 3 of this series for installation of a Management Agent. You should also have a DockerHub account. You may sign up for a free account [here](https://hub.docker.com/).

## **STEP 1** Launch an instance using the Oracle Cloud Developer Image
The following steps will guide you on how to launch a new compute instance using the Oracle Cloud Developer Image. 

1. In the Oracle Cloud Console, open the navigation menu, click **Marketplace**, and then click **All Applications** under **Marketplace**.![image of console navigation to marketplace](/Lab5/images/console-navigation-marketplace.png)
&nbsp;

2. Using the search bar, type `oracle cloud developer` and select the **Oracle Cloud Developer Image** that appears in the search result.
![image of marketplace search results](/Lab5/images/marketplace-search-results.png)
&nbsp;

3. Select the compartment that you want the the image to be installed in, accept the terms and click **Launch Instance**.
![image of oracle cloud developer image](/Lab5/images/oracle-image.png)
&nbsp;

4. After the instance is launched, you may proceed to pull your own Docker containers into the instance.


## **STEP 2** Configure Java Usage Tracker Location
To use JMS in a container, you must ensure that Java Usage Tracker records are written to `/var/log/java/usagetracker.log` on the container host. For a Docker container, run the following command with your DockerHub username, the name the image and the associated tag name:
```
docker run <Your DockerHub username>/<Your Image Name>:<Tag Name> -v /var/log/java/:/var/log/java/ -v /etc/oracle/java/:/etc/oracle/java/:ro
```

## **STEP 3** Verify Configuration
You may also verify that the log files were successfully written to the host by running this command:
```
sudo locate usagetracker.log
```
If correctly configured, the response should be as follows:
```
/var/log/java/usagetracker.log
/var/log/java/usagetracker.log.progress
```

**Note:** You should only use this configuration with trusted containers or where you do not require isolation between the host and the container, or between containers. If you require isolation, you should use a separate `usagetracker.log` file for each container and aggregate those logs into `/var/log/java/usagetracker.log` on the container host. 

## Want to Learn More?
For more information on how to run a Docker container, see [docker run](https://docs.docker.com/engine/reference/commandline/run/).

For more information on regarding changing the location of records, please see [Use bind mounts](https://docs.docker.com/storage/bind-mounts/).


## Acknowledgements
* **Author** - Alvin Lam, Java Management Service
* **Last Updated By/Date** - Alvin Lam, November 2021