**Situation:** DataDog PreRequisites and Tagging assets

**Task:** Spin up a small test environment to become familiar with DataDog

**Action:** I already had Virtual Box setup on my workstation, and decided to go with Vagrant since it had been a while since I had used it and I really needed a refresher. In a few relatively painless steps I had 3 test Ubuntu servers up running basic LAMP stacks.

    a. VirtualBox 6.0.18, Vagrant 2.2.7, using 2 scotch/box provider (Ubuntu 18.0.4 LTS) and a Ruby on Rails image (boxesio/rails).
    b. Signed up for DataDog eval
    c. Got my agents installed and configured thd DataDog.yaml for basic support.
    d. Ran into my first issue trying to get the YAML formatting right.  This format worked for creating tags:
    ["environment:production", "datacenter:houston", "owner:prodappteam"]
  
  **Result:** 3 servers reporting correctly
  
  ![](images/1_agent_configured.png?raw=true)
  
  ![](images/3_reporting.png?raw=true)
  
  ![](images/2_vagrant.png?raw=true)
  

  **Situation:** MySQL Integrations
  
  **Task:** Configure the DataDog-agent MySQL Integrations and a MySQL server to collection metrics into my DataDog instance.
  
  **Action:** Initially here I had all kinds of issues getting this work with any of the 3 LAMP stack servers to work in my environment.  
  A combination of user creation and permissions haunted me.  I then decided to just go with the hashicorp/bionic64.  
  Easier to work with and by installing MySQL myself I had more control over the security settings for MySQL
   
    a. Configured MySQL.d yaml files initially for u: datadog, p: DataDog.123
    b. Added the user and password per the instructions, but received no data.
    c. Removed authentication helper and modifed the password to 'datadog123', updated the MySQL YAML.
    d. Restarted the DataDog-Agent service and voila'!

  **Result:** MySQL accurately reporting it's metrics!
  
  **Situation:**
  
  **Task:**
  
  **Action:**
  
  **Result:**



  **Situation:**
  
  **Task:**
  
  **Action:**
  
  **Result:**
