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
![image](https://user-images.githubusercontent.com/58075995/213633667-675a624a-94f4-41dc-8c6d-9ece8f5bec54.png)



Create a framework to incorporate multiple dashboard grids that displays nation and regional level details of Verizon. 

Summary

The ideation behind this analytical tool is mainly on building a reusable framework that allows to incorporate new dashboards with minimal development intervention. To achieve this, an intuitive interface called super set is introduced between the user interface and database.
Superset comprises wide array of data sets and create interactive dashboards. The communication happens between the UI and already defined superset dashboard which in turn talks with database to return results in the form Iframe template.
The details page produces regional level analytics in the form of highcharts using super set ![image](https://user-images.githubusercontent.com/58075995/213633723-e9e162a4-7b2d-44b8-b69c-d76b7663f755.png)


Planning module serves the purpose of planning the construction of future Cband 5g sites
and also in updating the existing Verizon presence sites to be 5g Cband compatible.
The different types of planning revolves around
 1)Sector management
 2)Solution management
 3)Capacity management
 4)Rational management
The utilization and planning of SMDB sites and new raw land sites are considered if the planning of
coverage doesn't not meet the target percentage.


Sites Nomenclature:
* Existing Sites---->Existing On Air
* Future Sites - CA----->Embedded Base - Active Project (Mod)
* Vz Presence Sites---->Embedded Base - No Project (Mod)
* Future Sites - NB ---------->New Build - Active Project
* SMDB Sites----->New Build - No Project (SMDB Existing Structure)
* New Sites----->New Build - No Project (Raw Land)


Step A & B: Existing and Embedded Base and New Build Active

1. Identify any embedded base and new build active sites that are within a 10km buffer of the analysis area.

2.From the user uploaded list of locations falling within the analysis area, identify all existing transmitters and embedded base transmitters with an active project that cover at least one location.

3. Generate coverage for all transmitters in Step 2 using NPP PoD, if coverage is not available.

4. For each location store RSRP value for corresponding transmitters.

5. Perform best server analysis at all HH locations and assign locations to best serving sites.

6. Check total covered and served locations (based on per site capacity). If targets met, stop, else go to next step

ATOLL Coverage Spec :  https://docs.google.com/document/d/1SrYwoujmhl3IHAs59d0yCzg1aByuXSMDdSb1tMtHJpE/edit?usp=sharing

 POD Spec: Identify nearest C-band sites and use ATOLL coverages Spec.



Step C: New Build - No Project (SMDB Existing Structure)


1. Identify locations not covered by sites in Steps A+B

2. Identify SMDB sites falling within the analysis area, including within a 10km buffer.

3. Eliminate SMDB sites which violate ISD (Intersite Distance) criteria with Step A+B sites

4. Generate coverage for each Step 3 candidate site using NPP POD.

5. From the candidate SMDB sites, choose a site covering most uncovered locations (Step#1) and perform best server analysis with StepA+B and Step C sites and assign locations to this site. If no. of locations served is < Min. Locations required to consider (50) then ignore the site. Consider a site not violating ISD constraint with other SMDB sites.

6. Check total covered and served locations (based on per site capacity). If targets met, stop, else go Step#5 and choose from the remaining candidate sites.


7. Repeat Step#5 and Step#6 till either targets are met or all candidate sites have been considered. If targets are not met, go to Step D


Step D: New Build - No Project (Raw Land):

1. Identify locations not covered by sites in Steps A, B, and C.

2. Using user defined ISD and min location count (as specified as part of project creation), run clustering on the uncovered locations. This will create clusters with at least Min. Locations required to consider (50) with max. radius of 3km.

3. Consider cluster centroids as site locations, check if they satisfy ISD constraint with step A+B and step C sites, if so, assume them as new build site locations. If not choose a different location in the cluster as a new build site location. To choose different location create a uniform fixed grid (300m) with cluster boundary and select a location using a 3km buffer which covers max. HH locations.

4. Generate coverage for each Step 3 candidate site using NPP POD.

5. From the candidate New build sites, choose a site covering most uncovered locations (Step#1) and perform best server analysis with StepA+B, Step C, Step D sites and assign locations to this site. If no. of locations served is < Min. Locations required to consider (50) then ignore the site.
6. Check total covered and served locations (based on per site capacity). If targets met, stop, else go Step#5 and choose from the remaining candidate sites.

7. Repeat Step#5 and Step#6 till either targets are met or all candidate sites have been considered. If capacity % target is not met, go to Step E.



Step E: Offloading most overloaded sites

1. Get the list of sites overloaded and rank in descending order.

2. To offload the top site, try to offload with the SMDB sites first. If any unselected candidate SMDB site which covers locations from the overloaded site and meets the ISD and min locations criteria, select that site.

3. Perform BSP with selected SMDB site coverage and assign locations. If the site serves <  Min. Locations required to consider (50) then ignore the site.

4. Check total covered and served locations (based on per site capacity). If targets met, stop, else repeat Step#1 to Step#3

5. If capacity % target is not met, try to offload with New build sites. To select a new build site, create a uniform fixed grid (300m) using a convex hull with unserved locations of the overloaded site.

6. Consider each centroid of these grid cells as new build site location and eliminate site locations based on ISD and min locations criteria with 3km buffer around site location

7. With remaining site locations create clusters using agglomerative clustering using intersite distance as parameter. Choose one site per cluster based on max covered with the 3km buffer and generate PoD coverages for them.

8. Perform BSP with selected new build site coverage and assign locations. If the site serves <  Min. Locations required to consider (50) then ignore the site.

9. Repeat Step#1, and Step#5 to Step#8 till capacity % target is met.


