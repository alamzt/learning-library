# CREATE MYSQL DATABASE SYSTEM AND HEATWAVE CLUSTER
![INTRO](./images/00_mds_heatwave_2.png " ") 


## Introduction

In this lab, you will create and configure a MySQL DB System. The creation process will use a provided object storage link to create the airportdb schema and load data into the DB system.  Finally you will add a HeatWave Cluster comprise of two or more HeatWave nodes.  

_Estimated Lab Time:_ 20 minutes

Watch the video below for a quick walk through of the lab.

[](youtube:Uz_PXHzO9ac) 

### Objectives

In this lab, you will be guided through the following tasks:


- Create Virtual Cloud Network 
- Create MySQL Database for HeatWave (DB System) instance with sample data (airportdb)
- Add a HeatWave Cluster to MySQL Database System

### Prerequisites

- An Oracle Trial or Paid Cloud Account
- Some Experience with MySQL Shell


## Task 1: Create Virtual Cloud Network 

1. Navigation Menu   
        Networking  
            Virtual Cloud Networks
    ![VCN](./images/03vcn01.png " ")

2. Click **Start VCN Wizard**
    ![VCN](./images/03vcn02.png " ")

3. Select 'Create VCN with Internet Connectivity'

    Click 'Start VCN Wizard' 
    ![VCN](./images/03vcn03.png " ")

4. Create a VCN with Internet Connectivity 

    On Basic Information, complete the following fields:

 VCN Name: 
     ```
    <copy>MDS-VCN</copy>
    ```
 Compartment: Select  **(root)**

 Your screen should look similar to the following
    ![VCN](./images/03vcn04.png " ")

5. Click 'Next' at the bottom of the screen 

6. Review Oracle Virtual Cloud Network (VCN), Subnets, and Gateways
         
    Click 'Create' to create the VCN
    ![VCN](./images/03vcn04-1.png " ")

7. The Virtual Cloud Network creation is completing 
    ![VCN](./images/03vcn05.png " ")
    
8. Click 'View Virtual Cloud Network' to display the created VCN
    ![VCN](./images/03vcn06.png " ")

9. On MDS-VCN page under 'Subnets in (root) Compartment', click  '**Private Subnet-MDS-VCN**' 
     ![VCN](./images/03vcn07.png " ")

10.	On Private Subnet-MDS-VCN page under 'Security Lists',  click  '**Security List for Private Subnet-MDS-VCN**'
    ![VCN](./images/03vcn08.png " ")

11.	On Security List for Private Subnet-MDS-VCN page under 'Ingress Rules', click '**Add Ingress Rules**' 
    ![VCN](./images/03vcn09.png " ")

12.	On Add Ingress Rules page under Ingress Rule 1
 
 Add an Ingress Rule with Source CIDR 
    ```
    <copy>0.0.0.0/0</copy>
    ```
 Destination Port Range 
     ```
    <copy>3306,33060</copy>
     ```
Description 
     ```
    <copy>MySQL Port Access</copy>
     ```
 Click 'Add Ingress Rule'
    ![VCN](./images/03vcn10.png " ")

13.	On Security List for Private Subnet-MDS-VCN page, the new Ingress Rules will be shown under the Ingress Rules List
    ![VCN](./images/03vcn11.png " ")

## Task 2: Create MySQL Database for HeatWave (DB System) instance with sample data (airportdb)

1. Go to Navigation Menu 
         Databases 
         MySQL
         DB Systems
    ![MDS](./images/04mysql01.png " ")

2. Click 'Create MySQL DB System'
    ![MDS](./images/04mysql02.png " ")

3. Create MySQL DB System dialog complete the fields in each section

    - Provide basic information for the DB System
    - Setup your required DB System
    - Create Administrator credentials
    - Configure Networking
    - Configure placement
    - Configure hardware
    - Exclude Backups
    - Advanced Options - Data Import
   
4. Provide basic information for the DB System:

 Select Compartment **(root)**

 Enter Name
     ```
    <copy>MDS-HW</copy>
    ```
 Enter Description 
    ```
    <copy>MySQL Database Service HeatWave instance</copy>
    ```
 
 Select **HeatWave** to specify a HeatWave DB System
    ![MDS](./images/04mysql03-3.png " ")

5. Create Administrator Credentials

 Enter Username
    ```
    <copy>admin</copy>
    ```
    
 Enter Password
    ```
    <copy>Welcome#12345</copy>
    ```   
 Confirm Password
    ```
    <copy>Welcome#12345</copy>
    ```
    ![MDS](./images/04mysql04.png " ")

6. On Configure networking, keep the default values

    Virtual Cloud Network: **MDS-VCN**
    
    Subnet: **Private Subnet-MDS-VCN (Regional)**

    ![MDS](./images/04mysql05.png " ")

7. On Configure placement under 'Availability Domain'
   
    Select AD-3

    Do not check 'Choose a Fault Domain' for this DB System. 

    ![MDS](./images/04mysql06-3.png " ")

8. On Configure hardware, keep default shape as **MySQL.HeatWave.VM.Standard.E3**

    Data Storage Size (GB) Set value to:  **100**
    
    ```
    <copy>100</copy>
    ``` 
    ![MDS](./images/04mysql07-3-100.png" ")

9. On Configure Backups, disable 'Enable Automatic Backup'

    ![MDS](./images/04mysql08.png " ")

10. Click on Show Advanced Options 


11. Select Data Import tab. 

12. Use the Image below identify your OCI Region. 

    ![MDS](./images/regionSelector.png " ")

13. Click on your localized geographic area

    ## North America (NA)  
    **Tenancy Regions** Please select the same region that you are creating MDS in  

    <details>
    <summary>US East (Ashburn) Region - Copy and paste to PAR Source URL</summary>
    <br>
    ```
    <copy> 
    https://objectstorage.us-ashburn-1.oraclecloud.com/p/IeENlkro2TdsgKZPh2KyLNUnKOh45sWFvIr5jz2djuFfC6ExviKq7cwITTLOUhDP/n/idazzjlcjqzj/b/airportdb-bucket/o/airportdb/@.manifest.json
    </copy>
    ```
    </details>

    <details>
    <summary>US West (Phoenix) Region - Copy and paste to PAR Source URL</summary>
    <br>
    ```
    <copy> 
    https://objectstorage.us-phoenix-1.oraclecloud.com/p/vQk5N0AGtnaDJuwBdvA4CpqnXpOo96_XEzOEcTapd5I2dK6ZPzFRp7fFYF5_bGGN/n/idazzjlcjqzj/b/airportdb-bucket/o/airportdb/@.manifest.json
    </copy>
    ```
    </details>

    <details>
    <summary>US West (San Jose) Region - Copy and paste to PAR Source URL</summary>
    <br>
    ```
    <copy> 
    https://objectstorage.us-sanjose-1.oraclecloud.com/p/8ggUw6KN3odKB2111P0jvDcp0G4c9UhqqOhICQdLPa1OGEuqFhNDaCJ52txv3rT9/n/idazzjlcjqzj/b/airportdb-bucket/o/airportdb/@.manifest.json
    </copy>
    ```
    </details>
 
    <details>
    <summary>Canada Southeast (Montreal) Region - Copy and paste to PAR Source URL</summary>
    <br>
    ```
    <copy> 
    https://objectstorage.ca-montreal-1.oraclecloud.com/p/M-VE3R_PRlUZCdO7nkZm-NEIKCJibSbHfP39PhIQU8hnkTmbwdiH98_LQS-R02Sc/n/idazzjlcjqzj/b/airportdb-bucket/o/airportdb/@.manifest.json
    </copy>
    ```
    </details>
   
    <details>
    <summary>Canada Southeast (Toronto) Region - Copy and paste to PAR Source URL</summary>
    <br>
    ```
    <copy> 
    https://objectstorage.ca-toronto-1.oraclecloud.com/p/5hzfshBP7rSU7W-L1gzLUqLTQrU7Jd7BkA8IUoPjVj_hTs5BdDvC-ncv0E-pNyzm/n/idazzjlcjqzj/b/airportdb-bucket/o/airportdb/@.manifest.json
    </copy>
    ```
    </details>

    ## Latin America (LAD)
    **Tenancy Regions** Please select the same region that you are creating MDS in 
    <details>
    <summary>Brazil East (Sao Paulo) Region - Copy and paste to PAR Source URL</summary>
    <br>
    ```
    <copy> 
    https://objectstorage.sa-saopaulo-1.oraclecloud.com/p/OhTbbGLOoiEt-mPIlWLvX1G1k-c8A7xSIb-ua6-Pc4KX9JHioWev8ipdO5LyoC55/n/idazzjlcjqzj/b/airportdb-bucket/o/airportdb/@.manifest.json
    </copy>
    ```
    </details>
    
    <details>
    <summary>Chile (Santiago) Region - Copy and paste to PAR Source URL</summary>
    <br>
    ```
    <copy> 
    https://objectstorage.sa-santiago-1.oraclecloud.com/p/V9-g6ijSAi4gUVayFYZsFbKLJRAxm3MaYR_S3YddXxhoBcm51vwjiAIB-yTL9I0x/n/idazzjlcjqzj/b/airportdb-bucket/o/airportdb/@.manifest.json
    </copy>
    ```
    </details>
        
    <details>
    <summary>Brazil Southeast (Vinhedo) Region - Copy and paste to PAR Source URL</summary>
    <br>
    ```
    <copy> 
    https://objectstorage.sa-vinhedo-1.oraclecloud.com/p/a9QeIhMQzAgC6Zga-bOeSfBk47CgzNsuUEnxTYSh4P33WrS4-jgzpPoAJN4JvEai/n/idazzjlcjqzj/b/airportdb-bucket/o/airportdb/@.manifest.json
    </copy>
    ```
    </details>
    ## Europe, Middle East and Africa (EMEA)
    **Tenancy Regions** Please select the same region that you are creating MDS in 

    <details>
    <summary>UK South(London) Region - Copy and paste to PAR Source URL</summary>
    <br>
    ```
    <copy> 
    https://objectstorage.uk-london-1.oraclecloud.com/p/VP6XbjonZbxrHCdr5sO2VyMTJ4LIcLLKhskHKXhUvFfG9lKUYYezdYv_ahkEZ8-p/n/idazzjlcjqzj/b/airportdb-bucket/o/airportdb/@.manifest.json
    </copy>
    ```
    </details>

    <details>
    <summary>UK West (Newport) Region - Copy and paste to PAR Source URL</summary>
    <br>
    ```
    <copy> 
    https://objectstorage.uk-cardiff-1.oraclecloud.com/p/W9hqprQAyNOwMQI_MVdXByEEjpj7ys91uJCF9mGgRobyq6_YW9cY-vE24ypujlTI/n/idazzjlcjqzj/b/airportdb-bucket/o/airportdb/@.manifest.json

    </copy>
    ```
    </details>
    
    <details>
    <summary>Germany Central (Frankfurt) Region - Copy and paste to PAR Source URL</summary>
    <br>
    ```
    <copy> 
    https://objectstorage.eu-frankfurt-1.oraclecloud.com/p/K_x7ZZLppROogwgHiMIuwCvliVjALS3BjnRSVyEn309zhWS1KSuTf7SpAgSOA1gX/n/idazzjlcjqzj/b/airportdb-bucket/o/airportdb/@.manifest.json
    </copy>
    ```
    </details>

    <details>
    <summary>Switzerland North(Zurich) Region - Copy and paste to PAR Source URL</summary>
    <br>
    ```
    <copy> 
    https://objectstorage.eu-zurich-1.oraclecloud.com/p/dXzR82NbfW_0KgA_BAb90RVC2z2848R89bMmrBvWdvxNCauAPeaFoibq1LhZPdpv/n/idazzjlcjqzj/b/airportdb-bucket/o/airportdb/@.manifest.json
    </copy>
    ```
    </details>

    <details>
    <summary>Netherlands Northwest(Amsterdam) Region - Copy and paste to PAR Source URL</summary>
    <br>
    ```
    <copy> 
    https://objectstorage.eu-amsterdam-1.oraclecloud.com/p/Lv9NBkqSvnACewUgvpBsyPvctiIPGctIXzyIaegBjoxzNHpI1KmaKj3uIS-EFExr/n/idazzjlcjqzj/b/airportdb-bucket/o/airportdb/@.manifest.json   
    </copy>
    ```
    </details>

    <details>
    <summary>Saudi Arabia West(Jeddah)  Region - Copy and paste to PAR Source URL</summary>
    <br>
    ```
    <copy> 
    https://objectstorage.me-jeddah-1.oraclecloud.com/p/y_J1QSrYDXElSyZodq_nObqR_sMai_eff1wGDbXO0Jf5ObzilBODjtCWa-70026V/n/idazzjlcjqzj/b/airportdb-bucket/o/airportdb/@.manifest.json  
    </copy>
    ```
    </details>

    <details>
    <summary>Israel 1 (Jerusalem) Region - Copy and paste to PAR Source URL</summary>
    <br>
    ```
    <copy> 
    https://objectstorage.il-jerusalem-1.oraclecloud.com/p/NNXovSVu6Q9HfSLNUKR5rMYzktt1RPrJW6z8emLM6M3ggasHMANykrpshp7nU-Ld/n/idazzjlcjqzj/b/airportdb-bucket/o/airportdb/@.manifest.json
    </copy>
    ```
    </details>

    ## Asia Pacific (APAC)
    **Tenancy Regions** Please select the same region that you are creating MDS in 

    <details>
    <summary>Japan East(Tokyo) Region - Copy and paste to PAR Source URL</summary>
    <br>
    ```
    <copy> 
    https://objectstorage.ap-tokyo-1.oraclecloud.com/p/N-Fj8lY5lJe4JKbf9-vbpBcBat4B5G9VBk-iC37d7Juz9lq_zR660gRrs3bmiblC/n/idazzjlcjqzj/b/airportdb-bucket/o/airportdb/@.manifest.json 
    </copy>
    ```
    </details>
 
    <details>
    <summary> Japan Central (Osaka) Region - Copy and paste to PAR Source URL</summary>
    <br>
    ```
    <copy>
    https://objectstorage.ap-osaka-1.oraclecloud.com/p/lsDWl1s5qPZuRdN7hxjqY3Pnqena71I4j2QKSdDIbM6BVbNXxki4zs1SaqnPnp0g/n/idazzjlcjqzj/b/airportdb-bucket/o/airportdb/@.manifest.json
    </copy>
    ```
    </details>
   
    <details>
    <summary>South Korea Central(Seoul) Region - Copy and paste to PAR Source URL</summary>
    <br>
    ```
    <copy>
    https://objectstorage.ap-seoul-1.oraclecloud.com/p/SCwM4wjV5i5dWBp0E7rtxNff6wS8NE2rpTm9IDrTOh6H2sQriR-WkqHU96KxdScV/n/idazzjlcjqzj/b/airportdb-bucket/o/airportdb/@.manifest.json
    </copy>
    ```
    </details>

  
    <details>
    <summary> South Korea North (Chuncheon) Region - Copy and paste to PAR Source URL</summary>
    <br>
    ```
    <copy>
    https://objectstorage.ap-chuncheon-1.oraclecloud.com/p/cmF0S75URKX_kZbLs3zoGpVrrNq7g-a6tWXrcfQXKRDjXuW_U9llrvKgE5bwh72l/n/idazzjlcjqzj/b/airportdb-bucket/o/airportdb/@.manifest.json
    </copy>
    ```
    </details>
  
    <details>
    <summary> Australia East (Sydney) Region - Copy and paste to PAR Source URL</summary>
    <br>
    ```
    <copy>
    https://objectstorage.ap-sydney-1.oraclecloud.com/p/GOSs0oAPv--FGz-NssbiGjCqGSlfXWcRToN4Nr_7ouGfAQpIafAbLA5akUxdWqfu/n/idazzjlcjqzj/b/airportdb-bucket/o/airportdb/@.manifest.json
    </copy>
    ```
    </details>

    <details>
    <summary> Australia Southeast (Melbourne) Region - Copy and paste to PAR Source URL</summary>
    <br>
    ```
    <copy>
    https://objectstorage.ap-melbourne-1.oraclecloud.com/p/_dxPlqS7R5T4O5HJdOfEsFg1toGjt1OvnxLwbyBbQLlydN-5mc3l4mmSOn8ZW5wc/n/idazzjlcjqzj/b/airportdb-bucket/o/airportdb/@.manifest.json
    </copy>
    ```
    </details>
 
    <details>
    <summary> India West (Mumbai) Region - Copy and paste to PAR Source URL</summary>
    <br>
    ```
    <copy>
    https://objectstorage.ap-mumbai-1.oraclecloud.com/p/brAVESzCt9Us9EEnopyY_geGagLMzKSqbcJNgN3FSgXFZk5Ue_mviRmU9MzLcvy0/n/idazzjlcjqzj/b/airportdb-bucket/o/airportdb/@.manifest.json
    </copy>
    ```
    </details>


    <details>
    <summary> India South (Hyderabad) Region - Copy and paste to PAR Source URL</summary>
    <br>
    ```
    <copy>
    https://objectstorage.ap-hyderabad-1.oraclecloud.com/p/VJ-OUzthr26NbTkfOKtCxk4nGeJ9pdsAmOjclZtp6rINVMKbJNdsx0Ma2G3Suhj7/n/idazzjlcjqzj/b/airportdb-bucket/o/airportdb/@.manifest.json 
    </copy>
    ```
    </details>
 
14. Your PAR Source URL entry should look like this:
    ![MDS](./images/04mysql08-2.png " ")

15. Review **Create MySQL DB System**  Screen 

    ![MDS](./images/04mysql09-3.png " ")

    
    Click the '**Create**' button

16. The New MySQL DB System will be ready to use after a few minutes 

    The state will be shown as 'Creating' during the creation
    ![MDS](./images/04mysql10-3.png" ")

17. The state 'Active' indicates that the DB System is ready for use 

    On MDS-HW Page, check the MySQL Endpoint (Private IP Address) 

    ![MDS](./images/04mysql11-3.png" ")

## Task 3: Add a HeatWave Cluster to MDS-HW MySQL Database System

1. Open the navigation menu  
    Databases 
    MySQL
    DB Systems
2. Choose the root Compartment. A list of DB Systems is displayed. 
    ![Connect](./images/10addheat01.png " ")
3. In the list of DB Systems, click the **MDS-HW** system. click **More Action ->  Add HeatWave Cluster**.
    ![Connect](./images/10addheat02.png " ")
4. On the “Add HeatWave Cluster” dialog, select “MySQL.HeatWave.VM.Standard.E3” shape

5. Click “Estimate Node Count” button
    ![Connect](./images/10addheat03.png " ")
6. On the “Estimate Node Count” page, click “Generate Estimate”. This will trigger the auto
provisioning advisor to sample the data stored in InnoDB and based on machine learning
algorithm, it will predict the number of nodes needed.
    ![Connect](./images/10addheat04.png " ")

7. Once the estimations are calculated, it shows list of database schemas in MySQL node. If you expand the schema and select different tables, you will see the estimated memory required in the Summary box, There is a Load Command (heatwave_load) generated in the text box window, which will change based on the selection of databases/tables

8. Select the airportdb schema and click “Apply Node Count Estimate” to apply the node count
    ![Connect](./images/10addheat05.png " ")

9. Click “Add HeatWave Cluster” to create the HeatWave cluster
    ![Connect](./images/10addheat06.png " ")
10. HeatWave creation will take about 10 minutes. From the DB display page scroll down to the Resources section. Click the **HeatWave** link. Your completed HeatWave Cluster Information section will look like this:
    ![Connect](./images/10addheat07.png " ")


You may now proceed to the next lab.

## Acknowledgements
* **Author** - Perside Foster, MySQL Solution Engineering 
* **Contributors** - Mandy Pang, MySQL Principal Product Manager,  Priscila Galvao, MySQL Solution Engineering, Nick Mader, MySQL Global Channel Enablement & Strategy Manager, Frédéric Descamps, MySQL Community Manager
* **Last Updated By/Date** - Perside Foster, MySQL Solution Engineering, September 2021
