# UrbanEvac
## Original Authors
* Shaun Cross
* Grant Doohen
* Giovanni Gaito
* Bradley Griffee
* Nasi Robinson
* Rebekah Warnock

## Project Description
Our team hopes to ultize the power of machine learning and artificial intelligence to tackle the problem of large scale evacuation of major cities in the case of an environmental disaster. Through leveraging accumulated traffic data and pre-existing route mapping technology we aim to create an application which will provide real time evacuation plans for individuals in a disaster zone.

### Motivation
In recent years, natural disasters have destroyed many communities in the United States and throughout the world. Thankfully, loss of life was significantly reduced, or completely prevented in many of these disasters by utilizing advanced warning systems and emergency broadcasts. However, we believe that with the gowing popularity of smart devices, we can reduce the impact of these disasters even further. Through efficient route planning, with specialzed considerations for natural disaster circumstances, our system will aim to supplement the emergency broadcast systems with real-time evacuation planning.

# Needed Applications
* Eclipse with Maven support
* PostgreSQL Server (Can't find anywhere to host this for free, needs to run locally)
* Wildfly (or other Java EE Application Server(could possibly use the built-in eclipse tools to do this))
* Java JDK

# Setup

These steps are out of date now. After I did my (hacky) optimization, the server expects the database to have been converted (the code should still exist in the webapp to do this). Also, the data dump is outdated and a more concise version (which I don't have a backup of) was used.

## Install PostgreSQL
1. Download PostgreSQL from EnterpriseDB
2. Install PostgreSQL and Launch StackBuilder
3. Select ODBC driver and PostGIS to install
4. Once installed, launch pgAdmin 4
5. Create a database called OSM
6. Create a user called OSM with password osm123
7. Use psql command-line tool to import data

.\psql.exe -U postgres -f "D:\schema.sql" OSM

.\psql.exe -U postgres -f "D:\data.sql" OSM

## Import Project in Eclipse
Choose File->Import->Existing Maven Projects and select the RoutingApp directory

## Setup New JRE
Window->Preferences->Java->Installed JREs and add a new Standard VM that points to the JDK home directory.
This allows Maven to actually work.

## Install extra Maven Dependency
Microsoft doesn't have their JDBC driver in maven, so it needs to be installed manually.

In Eclipse, make a new Run Configuration for a Maven Build... and config it as shown below.

https://gyazo.com/bd41966253f140e74ad3664e52cb59eb

## Setup Build Configuration
Create a new Run Configuration for a Maven Build... and config it as shown below.

https://gyazo.com/c2f0b10ef60bdcfc8982fac18b2932ef

# Build
Select the created "Maven Build" run configuration and run it.

# Running/Testing
Copy the UrbanEvac-0.0.1-SNAPSHOT.war file from the target directory to the wildfly/standalone/deployments folder.

Run wildfly by running wildfly/bin/standalone.bat

The server will be running on http://localhost:8080/UrbanEvac-0.0.1-SNAPSHOT/

BE SURE TO INCLUDE A '/' AT THE END OF ALL REQUESTS!

Changes can be deployed by rebuilding and copying the new war file to the deployments folder - no server restart necessary.

# Known Problems

### Wildfly will occasionally crash with "Out of metaspace" after re-deploying too many times. 
* Restarting the server will fix it.

### Some hibernate error complaing about not able to create a connection because of a Azure Firewall.
* Exactly as it sounds. You must not be sitting on campus working on this. Let me know if this happens.