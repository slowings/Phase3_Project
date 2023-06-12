# Phase 3 Final Project: Ensuring Access to Water

Student name: Sarah Lowing

Student pace: Self paced

Project review date: 6/5/2023

Instructor: Abhineet Kulkarni

Blog post URL: https://wordpress.com/post/datamonsterdotblog.wordpress.com/47

## Introduction
For the Phase 3 final project we will develop a model to predict water well failure in Tanzania using information gathered by the Tanzanian government and hosted as a competition by DrivenData. We'll depart from the competition to address the needs of our client, a local NGO working with an international funding partner to locate the wells at greatest risk of failure in order to determine which geographic regions to direct their funding towards.

## Water Management
Tanzania faces an increased demand for water based on population growth projections.  To meet the needs of this growing population they have transferred water rights and management to national and regional authorities.  These municipalities face many challenges, such as increased contamination of groundwater storage from mining and agricultural runoff, frequent chollera outbreaks, and naturally occuring floride deposits in hazardous quantities.  Additionally, there are threats posed by changing climate conditions that have shifted rainfall patterns, causing storms producing more intense rainfall and increased flooding, leaving less water to filter into the underground aquafers and lakes from which the wells draw from- compounding this is more recent multi-year drought cycles.  As a result, paradoxically, this flood prone country faces increasing water shortages.   

It's important to clarify that the word well can mean many things in this dataset, from complex mechanicanical pump sites with extensive filtration to a hand pump that brings up untreated groundwater (water from lakes, rivers, and streams).

Some key factors we will take into account:

__Pollution__- Which water points have harmful concentrations of pollutants

__Population__- Which water points have the highest population density

__Salinization__- Which water points are at greatest risk from sea level rise

## EDA

Please note there is a seperate EDA file as well as the Phase3_Project in this notebook, where the bulk of our initial analysis takes place.  

By eliminating duplicate and unneccessary columns we were able to reduce our dataframe to the following columns:

__*amount_tsh*__- TSH measures the distance water travels vertically to the pump site.  70% have 0, indicating the well is actually groundwater/sourced from lakes, streams, rivers, etc.  We also see some values that might be erroneous, like 138,000, but might not be if the water is travelling through piping to a house in a town for instance. 

__*gps_height*__

__*latitude*__ and __*longitude*__- 

__*installer*__- Organization that installed the well

__*basin*__ - Geographic water basin: Lake Victoria, Pangani, Rufiji, Internal,
              Lake Tanganyika, Wami/Ruvu, Lake Nyasa, Ruvuma/Southern Coast, Lake Rukwa

__*district_code*__  - Geographic location (coded)

__*population*__  - Population around the well

__*gps_height*__  - Height of pump head above sea level

__*quality_group*__ - Quality of the water: good, salty, unknown, milky, colored, fluoride

__*source_class*__ - Source of the water: spring, shallow well, borehole, river/lake, 
                     rainwater harvesting, dam, other 

__*extraction_type*__- Kind of extraction at waterpoint: gravity, handpump, other, submersible, motorpump, rope pump, wind-powered, etc...


After cleaning and consalidating column values, we are ready for modelling.

## Modelling

We ran three successive models, a logistic regression, a decision tree, and a random forest.  We used the information generated by a LabelViz plot of decision tree to inform our understanding of some of the key variables influencing water security in Tanzania.  A feature importance plot of our random forest confirmed our findings from the DT.

## Findings and Conclusion

By far the most relevant factor in well failure is location. As we have been discussing, there is a noteable lack of working wells in the south eastern region of the country, and our analysis has confirmed this. The next most important factor in well failure is the 'installer' 'other', meaning small no-named well pumps, or simple machines designed to move water are most likely to fail. Our best model, the DTC was able to accurately predict well functionality 98% of the time in our test data.

## Next steps
Digging in deeper:

* Use mining site locations to anticipate water quality degradation
* Identify communities whose nearest water access is greater than 10 miles
* Use well depth and gps height to create a new column for wells at greatest risk of salinization 
* Use a blackbox model to improve F1 and recall scores to get the most accurate picture of where wells will fail

