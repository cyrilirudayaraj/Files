# Files

Objective: 
E2E process for RFP/Rural Broadband analysis. It provides an estimate to qualify all households in certain area for RFP .
Summary:
Quantify number of unserved/underserved households, addresses, covered by the existing Verizon network, covered  by new builds, new builds for capacity
Provide Cost estimate to qualify households in certain area for RFP
The different steps that are involved in planning a 5g coverage for any location, county or state includes the following steps.
		1) Existing & Embedded Base (Step A && Step B)
		2) NB - Active Project
		3) NB - No Project (SMDB) (Step C)
		4) NB - No Project (Raw Land) (Step D)
Brillion's contribution:
We have involved right from the design phase in shaping the wireframes of the application. We have come up with multiple UI templates before arrived at the final model. Extensively worked on constructing dynamic UI to display the results of RFP tool and also in mounting restful services.	
![image](https://user-images.githubusercontent.com/58075995/192478291-817dba62-a87d-466e-833f-864a6ddbe6d1.png)


Objective
Create a framework to incorporate multiple dashboard grids that displays nation and regional level details of Verizon. 

Summary

The ideation behind this analytical tool is mainly on building a reusable framework that allows to incorporate new dashboards with minimal development intervention. To achieve this, an intuitive interface called super set is introduced between the user interface and database.
Superset comprises wide array of data sets and create interactive dashboards. The communication happens between the UI and already defined superset dashboard which in turn talks with database to return results in the form Iframe template.
The details page produces regional level analytics in the form of highcharts using super set and its associated coverage representation using map in the form of geojson, tile ,WMS, heatmap layers

Brillion's contribution

We have developed an angular app which gives a niche of a framework. The framework is developed by configuring the key details in the database. Each granular HTML components are configured and fetched using REST API. To create the configuration in DB, an admin interface is developed. It takes entries to be persisted in in the DB and a dashboard to be created in superset to configure a new dashboard.
![image](https://user-images.githubusercontent.com/58075995/192478396-36714357-811c-4462-8ca2-5647358eaae3.png)
