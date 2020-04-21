**Situation:** DataDog PreRequisites and Tagging assets.  Spin up a small test environment to become familiar with DataDog

**Task:**  I already had Virtual Box setup on my workstation, and decided to go with Vagrant since it had been a while since I had used it and I really needed a refresher. In a few relatively painless steps I had 3 test Ubuntu servers up running basic LAMP stacks.

**Actions:**

    1. VirtualBox 6.0.18, Vagrant 2.2.7, using 2 scotch/box provider (Ubuntu 18.0.4 LTS) and a Ruby on Rails image (boxesio/rails).
    2. Signed up for DataDog eval
    3. Got my agents installed and configured thd DataDog.yaml for basic support.
    4. Ran into my first issue trying to get the YAML formatting right.  This format worked for creating tags:
    ["environment:production", "datacenter:houston", "owner:prodappteam"]
  
  **Result:** 3 servers reporting correctly
  
  ![](images/1_agent_configured.png?raw=true)
  
  ![](images/3_reporting.png?raw=true)
  
  ![](images/2_vagrant.png?raw=true)
  
  ![](images/tags.png?raw=true)
  

  **Situation:** Configure the DataDog-agent MySQL Integrations and a MySQL server to collection metrics into my DataDog instance.
    
  **Task:**  Initially here I had all kinds of issues getting this work with any of the 3 LAMP stack servers to work in my environment. A combination of user creation and permissions haunted me.  I then decided to just go with the hashicorp/bionic64.  This was easier to work with and by installing MySQL myself I had more control over the security settings for MySQL. 
  
  **Actions:** 
   
    1. Configured MySQL.d yaml files initially for u: datadog, p: DataDog.123
    2. Added the user and password per the instructions, but received no data.
    3. Removed authentication helper and modifed the password to 'datadog123', updated the MySQL conf YAML.
    4. Restarted the DataDog-Agent service and voila'!

  **Result:** MySQL accurately reporting it's metrics!
  
  ![](images/mysql.png?raw=true)
   
  
  
  
  **Situation:** Configure the agent correctly to collect a randomly generated custom number called my_metric to demonstrate the extensibilty of DataDog.  This would allow near limitless levels of datacollection via custom integrations and methods.
  
  **Task:** This one was tricky at first.  The sample code for the metric didn't want to run. I wasted too much time playing with the Python script, before getting Victor on the phone for an assist.  Simplified the code to just generate a singl random number.  In doing so, also ran into an issue I had seen before when calling the random funcion inside of Python.  Altered it to use random.randrange and it worked like a charm.
  
  **Actions:** 
    1. Created the necessary folders inside of the etc/datadog-agent/conf.d directly.
    2. Edited the my_metric yaml to update the minimum collection time to 45 seconds, for the **Bonus**
    3. Edited and updated the my_metric python file to generate a randome number.
    
  **Result:**  Success!

![](images/my_metric_yaml.png?raw=true)

![](images/my_metric_py.png?raw=true)

![](images/my_metric_dash.png?raw=true)

  **Situation:** Utilize teh DataDog API to create a Timeboard with various custom metrics to demonstrate the ability to dynamically create associated dashboards to suit various needs.  The would demonstrate the flexibility of DataDog so that it could presumably be incorporated into a variety of Devops CI/CD processes.
  
  **Task:** I created the 3 separate dashboards manually at first, so I could I review their JSON files and figure out what properties were associated with each widget type.  Then using a sample script, cobbled them all together in a single dashboard.  Hardest part of this was getting the count dashboard to display properly and trying to figure what option to use on the Anomaly function.
  
  **Actions:**
  1. Created the samle dashboards.
  2. Review the JSON files.

>  {"title":"My_Metric Count Dashboard",
>    "description":"Count of My_Metric for Host Vagrant over 1 hour.",
>    "widgets":[{"id":5940309555818136,
>      "definition":{"type":"query_value",
>        "requests":[{"q":"sum:my_metric.count{host:vagrant}.as_count()","aggregator":"sum"}],
>        "title":"Count of My_Metric for Host Vagrant over 1 hour",
>        "time":{}}}],"template_variables":[{"name":"host1","default":"my-host","prefix":"host"}],"layout_type":"ordered","is_read_only":true,"notify_list":[],"template_variable_presets":[{"name":"Saved views for hostname 2","template_variables":[{"name":"host","value":"vagrant"}]}],"id":"kkx-jji-epc"}

  4. Edited the sample dashboard python script.  
  
  **Result:**

![](images/huff_dashboard.png?raw=true)


  **Situation:** Create a monitor a monitor for the My_Metric data to send various alerts, warning and no data states.
  
  **Task:** This was super straight forward to create the monitor and the thresholds.  Only issues here was to find the sweet spot of not being alerted too often, since we're using a random number generator.  The Anomaly function really helped here and I think I find the sweet spot.  The change schedule as also super easy to setup to prevent alerts during certain hours etc.  My biggest issue here, was getting blank data from the markup language inside the notification itself.  Both {{host.name}} and {{host.ip}} came in as blank every single alert.
  
  **Actions:**
  1. Create a monitor based on my_metric.count.
  2. Select the Alert, Warning and recovery thresholds.
  3. Create a message with for the notifications and select who to send them to.
  4. Create downtime schedule for my_metric
  5. Choose appropriate start time and days, add the number hours.
  6. Create a message and choose who to notify.

  **Result:**

 ![](images/monitor.png?raw=true)
 ![](images/downtime.png?raw=true)
 ![](images/downtime2.png?raw=true)
 
   **Situation:** Configure a sample application, configure ddtrace-run to collect events from the sample application
   **Task:** This was fun, I had previously never worked with the Flask framework.  Once I configured the sample application, it took me a few minutes to determine I had to generate some traffice for the events to be collected.  Using curl I was able to generate a few events, enough to see some data.  I then created an additional python script to run curl multiple times to enhance the view of the dashboard.
   **Actions:**
   **Result:**
   
   
   
   
   
   **Situation:** 
   **Task:**
   **Actions:**
   **Result:**
  
