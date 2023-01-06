The ideation behind this analytical tool is mainly on building a reusable framework that allows to incorporate new dashboards with minimal development intervention. To achieve this, an intuitive interface called super set is introduced between the user interface and database.
Superset comprises wide array of data sets and create interactive dashboards. The communication happens between the UI and already defined superset dashboard which in turn talks with database to return results in the form Iframe template.
The details page produces regional level analytics in the form of highcharts using super set and its associated coverage representation using map in the form of geojson, tile ,WMS, heatmap layers

Brillion's contribution

We have developed an angular app which gives a niche of a framework. The framework is developed by configuring the key details in the database. Each granular HTML components are configured and fetched using REST API. To create the configuration in DB, an admin interface is developed. It takes entries to be persisted in in the DB and a dashboard to be created in superset to configure a new dashboard.
![image](https://user-images.githubusercontent.com/58075995/210947207-9d5ac214-98a6-4ef6-ab2f-b33064a9fdd3.png)
