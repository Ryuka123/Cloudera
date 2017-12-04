<img src="https://github.com/ShivaniThadiyan/Cloudera/blob/master/Images/Cloudera-logo-image.png"/>


<img src="https://github.com/ShivaniThadiyan/Cloudera/blob/master/Images/cloudera-microsoftAzure.png"/>


<!-- TOC -->
## Contents
1. [About Cloudera](#about-cloudera)
  * [Cloudera Director](#cloudera-director)
  * [Cloudera Manager](#cloudera-manager)
2. [Objective](#objective)  
3. [Getting Started](#getting-started)
 * [Accessing Cloudera Backend cluster details](#accessing-cloudera-backend-cluster-details)
 * [Accessing Cloudera Manager from Cloudera Director Web UI](#accessing-cloudera-Manager-from-Cloudera-Director-Web-UI)
 * [Hue](#hue)
 * [Apache Spark (Run Spark App)](#apache-spark-(Run-Spark-App))
 * [Viewing Jobs in UI](#viewing-Jobs-in-UI)
 * [Hive](#hive)
 * [Impala](#Impala)
4. [Power BI integration with Data Lake Store and Impala (Optional)](#power-BI-integration-with-Data-Lake-Store-and-Impala-(Optional))
 * [Integrating with Data Lake Store](#integrating-with-Data-Lake-Store)
 * [Integrating with Impala](#integrating-with-Impala)
5. [Reference](#reference)
 * [Restart Cloudera Management Service](#restart-Cloudera-Management-Service)
 * [Error Messages While Running the Spark Job](#error-Messages-While-Running-the-Spark-Job)
<!-- /TOC -->

### About Cloudera
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

## Cloudera Director
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

## Cloudera Manager
Cloudera  Manager  is  a  sophisticated  application  used  to  deploy,  manage,  monitor,  and
diagnose issues with your CDH deployments. Cloudera Manager provides the Admin Console,
a  web-based  user  interface  that  makes  administration  of your  enterprise  data  simple  and
straightforward. It also includes the Cloudera Manager API, which you can use to obtain
cluster health information and metrics, as well as configure Cloudera Manager.

<img src="https://github.com/ShivaniThadiyan/Cloudera/blob/master/Images/cloudera-manager.png"/>

# 2. Objective
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


# 3. Getting Started
## Accessing Cloudera Backend cluster details

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















  





