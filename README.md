<img src="https://github.com/ShivaniThadiyan/Cloudera/blob/master/Images/Cloudera-logo-image.png"/>


<img src="https://github.com/ShivaniThadiyan/Cloudera/blob/master/Images/cloudera-microsoftAzure.png"/>


<!-- TOC -->
### Table of Contents
1. [Module 1: About Cloudera](#Module-1)
  - [1.1: Cloudera Director](#1.1)
  - [1.2: Cloudera Manager](#1.2)
2. [Module 2: Objective](#Module-2)  
3. [Module 3: Getting Started](#Module-3)
  - [3.1: Accessing Cloudera Backend cluster details](#3.1)
  - [3.2: Accessing Cloudera Manager from Cloudera Director Web UI](#3.2)
  - [3.3: Hue](#3.3)
  - [3.4: Apache Spark (Run Spark App)](#3.4)
  - [3.5: Viewing Jobs in UI](#3.5)
  - [3.6: Hive](#3.6)
  - [3.7: Impala](#3.3)
4. [Module 4: Power BI integration with Data Lake Store and Impala (Optional)](#Module-4)
  - [4.1: Integrating with Data Lake Store](#4.1)
  - [4.2: Integrating with Impala](#4.2)
5. [Module 5: Reference](#Module-5)
  - [5.1: Restart Cloudera Management Service](#5.1)
  - [5.2: Error Messages While Running the Spark Job](#5.2)
<!-- /TOC -->

### Module 1:About Cloudera
Cloudera is an open-source Apache Hadoop distribution, CDH (Cloudera Distribution Including
Apache Hadoop) targets enterprise-class deployments of that technology.
Cloudera provides a scalable, flexible, integrated platform that makes it easy to manage rapidly
increasing volumes and varieties  of data  in your enterprise. Cloudera products  and solutions
enable you to deploy and manage Apache Hadoop and related projects, manipulate and analyze
your data, and keep that data secure and protected.

Cloudera develops a Hadoop platform that integrates the most popular Apache Hadoop open
source software within one place. Hadoop is an ecosystem, and setting a cluster manually is a
pain. Going through each node, deploying the configuration though the cluster, deploying your
services, and restarting them on a wide cluster is a major drawback of distributed system and
require lot of automation for administration. Cloudera developed a big data Hadoop distribution
that handles installation and updates on a cluster in few clicks.

Cloudera  also  develop  their  own  projects  such  as  Impala  or  Kudu  that  improve  hadoop
integration and responsiveness in the industry.

### 1.1: Cloudera Director
Cloudera Director enables reliable self-service for using CDH and Cloudera Enterprise Data
Hub in the cloud.

Cloudera Director provides a single-pane-of-glass administration experience for central IT to
reduce  costs  and  deliver  agility,  and  for  end-users  to  easily  provision  and  scale  clusters.
Advanced users can interact with Cloudera Director programmatically through the REST API or
the CLI to maximize time-to-value for an enterprise data hub in cloud environments.
Cloudera Director is designed for both long running and transient clusters. With long running
clusters, you deploy one or more clusters that you can scale up or down to adjust to demand.
With transient clusters, you can launch a cluster, schedule any jobs, and shut the cluster down
after the jobs complete.

The Cloudera  Director  server is designed to  run  in a  centralized  setup,  managing multiple
Cloudera  Manager  instances  and  CDH clusters,  with  multiple  users and user accounts. The
server  works  well  for  launching  and  managing  large  numbers  of  clusters  in  a  production
environment.

### 1.2: Cloudera Manager
Cloudera  Manager  is  a  sophisticated  application  used  to  deploy,  manage,  monitor,  and
diagnose issues with your CDH deployments. Cloudera Manager provides the Admin Console,
a  web-based  user  interface  that  makes  administration  of your  enterprise  data  simple  and
straightforward. It also includes the Cloudera Manager API, which you can use to obtain
cluster health information and metrics, as well as configure Cloudera Manager.

<img src="https://github.com/ShivaniThadiyan/Cloudera/blob/master/Images/cloudera-manager.png"/>

### Module 2: Objective
NOTE: As this test drive provides access to the full Cloudera Director platform, deployment can
sometimes take up to 45 minutes. While you wait, please feel free to review to helpful content
in this manual and on [Cloudera’s Azure Marketplace product page](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/cloudera.clouderaedh), or on the Cloudera website.
Please also consider watching the demo video showcased on the test drive launch page on the
Azure Marketplace web site.

The test drive provisions Cloudera Director, the environment, Cloudera Manager, and a cluster
consisting of 1 master node and 3 worker nodes. The test drive also integrates with Azure Data
Lake Store.

The use case scenario for this test drive is to provide users with a test Azure Data Lake Store and:
1.  Run the WordCount app with Hadoop/Spark on ADLS.
2.  Create a Hive table on the output, and query Hive from Hue.
3.  Run query using Impala from Hue or Power BI.
The following diagram shows how the data in this test case flows from a .TXT file via Hue
to
ADLS, processed by Spark.

<img src="https://github.com/ShivaniThadiyan/Cloudera/blob/master/Images/cloudera-lab-dataflow.png"/>


### Module 3: Getting Started
### 3.1: Accessing Cloudera Backend cluster details

Please login to the Azure portal and go to the Cloudera Director HOL Azure resource group
allocated to you. Copy the DNS URLs for the Cloudera Director,Manager and Master nodes.

1. Go to the Resource Groups section and search by name for the Resource Group provided
to you.
<img src="https://github.com/ShivaniThadiyan/Cloudera/blob/master/Images/Click-on-RG.png"/>

2. Go to the virtual machine starting with "cldr" Cloudera Director DNS Name.
<img src="https://github.com/ShivaniThadiyan/Cloudera/blob/master/Images/Click-on-VM.png"/>

Click on the Cloudera Director virtual machine to get the DNS name. (See below)
<img src="https://github.com/ShivaniThadiyan/Cloudera/blob/master/Images/Cloudera-copy-DNSname.png"/>

3. Go to the virtual machine starting with “cdedge” for the Cloudera Manager DNS name.
<img src="https://github.com/ShivaniThadiyan/Cloudera/blob/master/Images/Cloudera-click-on-vm2.png"/>

Click on the Cloudera Manager virtual machine to get the DNS name. (See below)
<img src="https://github.com/ShivaniThadiyan/Cloudera/blob/master/Images/Cloudera-click-on-DNSname.png"/>

4. Go to the virtual machine starting with “cdmstr” for the Cloudera Master DNS name.
<img src="https://github.com/ShivaniThadiyan/Cloudera/blob/master/Images/cloudera-click-mastervm.png"/>

Click on the Cloudera Master virtual machine to get the DNS name. (See below).
<img src="https://github.com/ShivaniThadiyan/Cloudera/blob/master/Images/cloudera-cpopy-masterdns.png"/>

You must also access the Cloudera backend cluster details to get the  Node Details. This is
explained below.
1. Log in to the Cloudera Director VM using the Cloudera Director FQDN address gathered  from  the previous steps, and use an SSH tool like PuTTY (or Terminal on Mac), which we’ll refer to in this walkthrough.[(Download PuTTY here)](https://putty.en.softonic.com/).
E.g. cldrhyic.eastus.cloudapp.azure.com
<img src="https://github.com/ShivaniThadiyan/Cloudera/blob/master/Images/Clouder-putty.png"/>

2. Once connected, login to the Cloudera Director VM using the Director Username and then the Director Password from the provided test drive access credentials.
(Note:Passwords are hidden when typed or pasted in Linux terminals)
<img src="https://github.com/ShivaniThadiyan/Cloudera/blob/master/Images/cloudera-login-using-putty.png"/>

All the Cloudera Backend cluster details are present in the NodeDetails file. Copy the NodeDetails into a text file or Word document for  reference, these details will be used later. To open the NodeDetails file use the following command.
cat NodeDetails
The  NodeDetails  file  contains  Node  and  URI  details  used  by  the  Cloudera  test  drive environment.These are gathered using a script which pulls required data using the API calls.
<img src="https://github.com/ShivaniThadiyan/Cloudera/blob/master/Images/cloudera-node-details.png"/>

### 3.2: Accessing Cloudera Manager from Cloudera Director Web UI
After deploying a cluster, you can manage it using Cloudera Manager.

1. Access the Cloudera Director Web UI using the Cloudera Director Access URL provided in the Access Information. Enter it into a web browser.
Eg:cldrhyic.eastus.cloudapp.azure.com:7189
<img src="https://github.com/ShivaniThadiyan/Cloudera/blob/master/Images/cloudera-webUI.png"/>

2. Accept the End User License Terms and Conditions and click on Continue.
<img src="https://github.com/ShivaniThadiyan/Cloudera/blob/master/Images/cloudera-click-continue.png"/>

3. Login to the Cloudera Director web console using CD-WEB UI Username and Password from the Access Information.
<img src="https://github.com/ShivaniThadiyan/Cloudera/blob/master/Images/login-cloudera-director.png"/>

4. The  Cloudera  Director  console  should  open.  Click  on  the Cloudera  Manager link  from the Cloudera Director Dashboard, as shown below.
<img src="https://github.com/ShivaniThadiyan/Cloudera/blob/master/Images/click-clouderamanager-link.png"/>

5. Use the Cloudera Manager FQDN address, along with the port number, and paste it in new browser tab.
EX:cdedge-4f171cc5.eastus.cloudapp.azure.com:7180
<img src="https://github.com/ShivaniThadiyan/Cloudera/blob/master/Images/clodera-FQDN-login.png"/>

6. Login to the Cloudera Manager Console using CM-WEB UI Username and CM-WEB UI Password from the Access Information.
<img src="https://github.com/ShivaniThadiyan/Cloudera/blob/master/Images/login-clouderManager-console.png"/>

Note:The next step is to Restart Stale Services. We must do this to get the Azure Service Principle updated to the configuration file site-core.xml, which is required to integrate with Azure Data Lake Store.

7. In Cloudera Manager, click on the HDFS-1 service to Restart Stale Services.
<img src="https://github.com/ShivaniThadiyan/Cloudera/blob/master/Images/cloudera-click-HDFS.png"/>

8. Click on the Restart Stale Services icon as shown in the below screenshot.
<img src="https://github.com/ShivaniThadiyan/Cloudera/blob/master/Images/Cloudera-click-restart-Stale-services.png"/>

9. Click  on  the Restart  Stale  Services button  so  the  cluster  can  read  the  new  configuration information.
<img src="https://github.com/ShivaniThadiyan/Cloudera/blob/master/Images/cloudera-click-Restart-stale2.png"/>

10. Click on the Restart Now button
<img src="https://github.com/ShivaniThadiyan/Cloudera/blob/master/Images/Cloudera-click-restart-Now.png"/>

11. Wait until all requested services are restarted. Once all the services are restarted, click on the Finish button.
<img src="https://github.com/ShivaniThadiyan/Cloudera/blob/master/Images/Cloudera-click-finish.png"/>

12. Now we have the Cloudera Director ready, with Cloudera Manager and Cluster (1 master and 3 workers).

Note: Please visit section in the Reference section later in this guide for additional details and help for any error messages you may encounter.

### 3.3: Hue
Hue is a set of web applications that enable you to interact with a CDH cluster. Hue applications let you browse HDFS and manage a Hive metastore. They also let you run Hive and Cloudera Impala queries, HBase and Sqoop commands, Pig scripts, MapReduce jobs, and Oozie workflows.

1. Copy the Cloudera Hue Web URL using the cloudera master DNS server url with port 8888 as shown in below example and paste it in browser – which opens the Hue console.
Example: http://cdmstr-6ce17224.eastus.cloudapp.azure.com:8888
<img src="https://github.com/ShivaniThadiyan/Cloudera/blob/master/Images/cloudera-hue.png"/>

2. Create a Hue Account by giving Cloudera Hue Web UI Username/Password from the NodeDetailsfile. (Username/Password: admin/admin)
<img src="https://github.com/ShivaniThadiyan/Cloudera/blob/master/Images/cloudera-hue-create-account.png"/>

3. You will login into the Hue dashboard. On the right side of the page, click on the HDFS browser icon, as shown in the below screenshot.

Note: CDH 5.12 has a new Hue UI. We recommend switching to Hue 3 from the admintab (see screenshot below).

<img src="https://github.com/ShivaniThadiyan/Cloudera/blob/master/Images/cloudera-hue-page.png"/>

4. Copy the data of inputfile from the below link. Give any name to the file (Eg: 'data' or 'input'), then save it in input.txt format.
https://aztdrepo.blob.core.windows.net/clouderadirector/inputfile.txt Once ready, click on Upload on the Hue file browser page (see below).

Note: Please ensure the inputfile is uploaded to the path /user/admin (see below):

<img src="https://github.com/ShivaniThadiyan/Cloudera/blob/master/Images/cloudera-hue-click-upload.png"/>

5. Select the saved .txt file to upload it.
<img src="https://github.com/ShivaniThadiyan/Cloudera/blob/master/Images/cloudera-hue-textfiles.png"/>

<img src="https://github.com/ShivaniThadiyan/Cloudera/blob/master/Images/clousera-hue-uploadfiles2.png"/>

6. The .txt file is now uploaded to Hue. The Spark application will use this data as input and provide the output to ADLS.


















 

 
















  





