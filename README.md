# HelloELK
HelloELK is a repository which provides hands on introduction to Elastic Stack(formerly ELK Stack) using sample configuration files.
Here, we will be creating a simple pipeline where inputs will be provided from STDIN by user and will be shown in Kibana.
![Pipeline](https://raw.githubusercontent.com/contactsharmamohit/HelloELK/master/GettingStartedIllustrations/Pipeline.png)

## Prerequisites
Elastic Stack required Java 8 or above. Make sure you have one in place by executing following command in CMD.
```CMD
java -version
```
you should get following output
```CMD
java version "1.8.0_121"
Java(TM) SE Runtime Environment (build 1.8.0_121-b13)
Java HotSpot(TM) 64-Bit Server VM (build 25.121-b13, mixed mode)
```
If Java is not installed and configured properly, please follow steps mentioned [here](https://www.java.com/en/download/help/download_options.xml).

## Downloading Elastic Stack
Head over to official [downloads](https://www.elastic.co/downloads) section and download ElasticSearch, Logstash and Kibana.
For reference, following versions are used here for windows environment:
-	ElasticSearch [v6.5.1](https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-6.5.1.zip)
-	Logstash [v6.5.1](https://artifacts.elastic.co/downloads/logstash/logstash-6.5.1.zip)
-	Kibana [v6.5.1](https://artifacts.elastic.co/downloads/kibana/kibana-6.5.1-windows-x86_64.zip)

Unzip the packages and we’re good to go.

## Setting Up the Elastic Stack
### ElasticSearch Setup
1.  Open command prompt in "<Extracted-Elastic-Search-Zip-Path>\elasticsearch-6.5.1\bin" and execute command:
```CMD
elasticsearch
```
2.  After getting "started" message, we can proceed to next step.
![ElasticSearch Started Screenshot](https://raw.githubusercontent.com/contactsharmamohit/HelloELK/master/GettingStartedIllustrations/ElasticSearch.jpg)

3. Head over to [localhost:9200](http://localhost:9200/). You should get reponse similar to following :
```JSON
{
  "name" : "udlVS2N",
  "cluster_name" : "elasticsearch",
  "cluster_uuid" : "64onb1QsRy-CZKLT5B9-rw",
  "version" : {
    "number" : "6.5.1",
    "build_flavor" : "default",
    "build_type" : "zip",
    "build_hash" : "8c58350",
    "build_date" : "2018-11-16T02:22:42.182257Z",
    "build_snapshot" : false,
    "lucene_version" : "7.5.0",
    "minimum_wire_compatibility_version" : "5.6.0",
    "minimum_index_compatibility_version" : "5.0.0"
  },
  "tagline" : "You Know, for Search"
}
```
### Logstash Setup
1.	Create a file named [logstash.conf](https://github.com/contactsharmamohit/HelloELK/blob/master/logstash.conf) inside directory "<Extracted-Logstash-Zip-Path>\logstash-6.5.1".
This is logstash configuration file which contains plugins like "input", "filter" and "output". Input plugin is used by logstash to read data from the source provided in input plugin, which in our case is, STDIN. Filter plugin is used to filter out irrelevant data and massage the incoming data into JSON documents. We have used GROK filter to achieve this. Output plugin is used to send data extracted from input using filter to provided deswtination, which in our case is ElasticSearch.

2.	Open command prompt in "<Extracted-Logstash-Zip-Path>\logstash-6.5.1\bin" directory and execute command:
```CMD
logstash -f ../logstash.conf
```
This will start the logstash pipeline (INPUT -> FILTER -> OUTPUT).

3.	After getting "pipelines running" or "Successfully started API Endpoint" message, we can proceed to next step. Hereafter, this window will be referred as "Logstash Console". Write any message here and hit Enter. Get ready to see your message in Kibana!

![Logstash](https://raw.githubusercontent.com/contactsharmamohit/HelloELK/master/GettingStartedIllustrations/Logstash.jpg)

### Kibana Setup
1.	Open command prompt in “<Extracted-kibana-Zip-Path>\kibana-6.5.1-windows-x86_64\bin” and execute command:
```CMD
kibana
```
2.	After getting "Ready" message, we can proceed to next step.

![Kibana](https://raw.githubusercontent.com/contactsharmamohit/HelloELK/master/GettingStartedIllustrations/Kibana.jpg)

3.	Open [localhost:5601](http://localhost:5601/) in browser.
4.	If Kibana Welcome Screen shows up, select "Explore on my own".

![Kibana_Welcome_Screen](https://raw.githubusercontent.com/contactsharmamohit/HelloELK/master/GettingStartedIllustrations/Kibana_Welcome_Screen.jpg)

5.	Head over to "Discover".

![Kibana_Discover](https://raw.githubusercontent.com/contactsharmamohit/HelloELK/master/GettingStartedIllustrations/Kibana_Discover.jpg)

6.	You will be asked to create a "Index Pattern". Enter "Index Name" (which we created in [logstash.conf](https://github.com/contactsharmamohit/HelloELK/blob/master/logstash.conf) file) and hit "Next Step".

![Kibana_CreateIndexPattern](https://raw.githubusercontent.com/contactsharmamohit/HelloELK/master/GettingStartedIllustrations/Kibana_CreateIndexPattern.jpg)

7.	Select Timestamp from dropdown and hit "Create index pattern".

![Kibana_ConfigureSettings](https://raw.githubusercontent.com/contactsharmamohit/HelloELK/master/GettingStartedIllustrations/Kibana_ConfigureSettings.jpg)

8.	You will be shown Index Pattern Screen. Head over back to "Discover" Section (Step 5) and Select "Today" in the Time Range:

![Kibana_Discover_Messages](https://raw.githubusercontent.com/contactsharmamohit/HelloELK/master/GettingStartedIllustrations/Kibana_Discover_Messages.jpg)

9.	You can see your messages (Sent from Logstash in Step 3 of Logstash setup) in Kibana now.
10.	To play along, enter new messages in Logstash Console, Head over back to Kibana and hit Refresh. Your messages will show up in Kibana.

![Kibana_HelloWorld](https://raw.githubusercontent.com/contactsharmamohit/HelloELK/master/GettingStartedIllustrations/Kibana_HelloWorld.jpg)

We are now done with ELK Stack Hello World! We have successfully setup up ELK and created Logstash pipeline.

## What Now?
### Visulatizations and Dashboards
For Kibana visualizations and Dashboards, read [here](https://www.elastic.co/guide/en/kibana/current/tutorial-build-dashboard.html).
### Reading from Log Files
For advanced pipelines, read [here](https://www.elastic.co/guide/en/logstash/current/advanced-pipeline.html).
### More about GROK Filters
Read more about Logstash filters [here](https://www.elastic.co/guide/en/logstash/current/filter-plugins.html).

Read more about GROK filter [here](https://www.elastic.co/guide/en/logstash/current/plugins-filters-grok.html).

For Java based GROK filters, refer [this](https://github.com/logstash-plugins/logstash-patterns-core/blob/master/patterns/java). It will come handy while parsing LOGs for APM (Application Performance Monitoring).

For more GROK filters, refer [this](https://github.com/logstash-plugins/logstash-patterns-core/blob/master/patterns/grok-patterns).

