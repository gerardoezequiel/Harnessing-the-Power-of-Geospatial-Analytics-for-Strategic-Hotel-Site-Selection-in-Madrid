<style> /* CSS styles for animation */ .code-block { overflow: auto; /* Hide overflow to clip the height */ max-height: 300px; /* Initial max-height value */ max-width: 1200px; /* Initial max-height value */ transition: max-height 0.5s ease-out; /* Apply transition effect */ } .code-block:hover { max-height: 800px; /* Increase max-height on hover */ } </style>
# Harnessing the Power of Geospatial Analytics in CARTO for Strategic Hotel Site Selection in Madrid
Prepared By: Gerardo Ezequiel Martín Carreño
Date: 10/07/2023



## Table of Contents

[Summary](#summary)  
1. [Introduction and Problem Context](#1-introduction-and-problem-context)  
2. [Methodology](#2-methodology)  
   2.1. [Data Acquisition & Preprocessing](#21-data-acquisition--preprocessing)  
   2.2. [Accessibility Analysis](#22-accessibility-analysis)  
   2.3. [Spatial Correlation, Hotspot Detection Analysis](#23-spatial-correlation-hotspot-detection-analysis)  
   2.4. [Spatial Index Enrichment](#24-spatial-index-enrichment)  
   2.5. [Competitive Proximity and Dispersion Analysis using Local Outlier Factor and KNN](#25-competitive-proximity-and-dispersion-analysis-using-local-outlier-factor-and-knn)  
3. [Value of the Analysis for NH Hotels Group](#3-value-of-the-analysis-for-nh-hotels-group)  
4. [Leveraging CARTO for Enhanced Geospatial Analysis](#4-leveraging-carto-for-enhanced-geospatial-analysis)  
5. [Limitations](#5-limitations)  
6. [Conclusions and Recommendations](#6-conclusion-and-recommendations)  

## [1. Introduction and Problem Context](#introduction-and-context)
NH Hotel Group, a renowned hotel chain based in Madrid, is actively seeking to open a new hotel that caters to the growing demand for cultural tourism. While NH Hotel Group has traditionally focused on serving business and corporate travelers, they recognize the shifting preferences of their target demographic and the opportunities presented by Madrid's rich cultural heritage. However, expansion in a city as dynamic and competitive as Madrid requires careful planning and strategic decision-making.

The target demographic for their new hotel is the mid-high income population aged 40-69, which represents a significant portion of visitors to Madrid. This demographic is attracted to the city's cultural heritage, vibrant performing arts scene, and diverse gastronomical offerings, as highlighted by the Madrid Tourism Report (Tourist Perception Survey 2019). The report indicates that 97.64% of visitors associate the city's service offerings with a mid-high purchasing power, emphasizing the potential of targeting this group for cultural tourism experiences. 

![](https://i.ibb.co/dmc2g0g/Carto-tourism-graphic.png)


To cater to this discerning demographic, NH Hotels Group aims to provide accommodations that offer a blend of luxury, convenience, and unique experiences reflecting the local culture. The location of the hotel plays a crucial role, requiring accessibility and proximity to the city's main attractions. NH Hotels Group recognizes that a central location not only enhances the guest experience but also aligns with the growing trend of "bleisure" travel.

The location of the new hotel will play a crucial role, requiring accessibility and proximity to the city's main cultural attractions. NH Hotels Group understands that a central location not only enhances the guest experience but also aligns with the growing trend of "bleisure" travel, where business and leisure activities are combined. By strategically positioning the new hotel in a vibrant area with cultural attractions, NH Hotels Group can create a seamless integration of cultural experiences and business opportunities for their guests.

The Madrid Tourism Report (Tourist Perception Survey 2019) also reveals that cultural tourism and business tourism are the most in-demand tourism products and services in Madrid

![](https://i.ibb.co/yVZ0c9K/Screenshot-2023-07-01-at-22-09-11-2x.png)



The success of the hotel is significantly influenced by its strategic location, ideally situated in a vibrant area bustling with diverse dining and entertainment options, all conveniently within walking distance. This advantageous positioning allows guests to effortlessly explore the city's main attractions while fully immersing themselves in the vibrant ambiance of the neighbourhood. Furthermore, NH Hotels Group showcases a steadfast commitment to environmental responsability, ensuring that sustainable practices are integrated throughout their operations. By carefully selecting locations within a 15-minute walking distance from tourists points of intetest, the hotel minimizes its environmental footprint while simultaneously delivering an exceptional experience to guests. 


Our goal in this project is to leverage the power of geospatial data and sophisticated analysis techniques using the CARTO platform to identify the optimal location for a new NH Hotel that caters specifically to cultural tourism. By finding a location that aligns with the preferences and needs of the target demographic, NH Hotels Group can enhance their offering, provide exceptional guest experiences, and contribute to the growth of cultural tourism in Madrid.



## [2. Methodology](#methodology)

Our methodology utilises sophisticated spatial analysis techniques to support NH Hotels Group in their hotel site selection process in Madrid. By combining data acquisition, preprocessing, and advanced analytical approaches, we uncover crucial factors that influence hotel suitability, accessibility, competitive proximity, and dispersion patterns within the city.

To enhance our methodology and unlock spatial intelligence for smarter decision-making, we leveraged the powerful capabilities offered by CARTO's platform and Analytics Toolbox. Here's how CARTO's features integrated seamlessly into our methodology:

**Seamless Cloud Connectivity & Integrations**
In our case, we integrated CARTO with Google BigQuery, one of the leading cloud data platforms. CARTO's seamless integration with BigQuery eliminates the complexities of Extract, Transform, Load (ETL) processes and enhances scalability. This integration enabled us to connect and leverage spatial data effectively, ensuring smooth data workflows and unparalleled support for location-based decision-making.
![](https://assets-global.website-files.com/6345207a1b18e581fcf67604/63bd89e9cd3c07f3671b3611_cloud-native-asset_white-bg.gif)

**Data Preparation**
CARTO's Data Observatory provided us with access to relevant datasets, allowing us to collect information on pedestrian traffic, existing accommodations, and points of interest in Madrid. This enriched our data acquisition process, ensuring comprehensive and up-to-date datasets for analysis.
![](https://i.ibb.co/DgQxFd0/Screenshot-2023-07-09-at-17-51-21-2x.png)

**Spatial Data Visualization** 
CARTO's advanced visualization capabilities were instrumental in creating interactive maps and visualizations of the datasets. These visual representations aided in understanding spatial patterns and relationships, providing valuable insights into the city's dynamics.
![](https://assets.website-files.com/6345207a1b18e581fcf67604/638dc4b9adbcad7169dce687_poster-video.a6526171%20(1).png)

**Spatial Analysis Techniques**
CARTO's Analytics Toolbox played a crucial role in our spatial analysis techniques. We leveraged functionalities such as isochrone intersection analysis, proximity analysis, geographically weighted regression (GWR) analysis, hotspot detection using Getis Ord statistics, and competitive proximity analysis using Local Outlier Factor (LOF) and K-nearest neighbours (KNN) techniques. CARTO's powerful tools allowed us to conduct these analyses effectively and efficiently, providing comprehensive insights into optimal hotel site selection, factors influencing suitability, identification of commercial hotspots, and assessment of the competitive landscape.
![](https://i.ibb.co/820XdHP/image4.png)

By integrating our methodology with CARTO's capabilities, we unlocked the full potential of spatial intelligence for smarter decision-making. CARTO's seamless cloud connectivity and integrations, including the integration with Google BigQuery, eliminated data silos, ensuring smooth data workflows and enabling effective leveraging of spatial data. Access to CARTO's Data Observatory enriched our analysis by providing a vast array of geospatial datasets, allowing us to gain deeper insights and make more informed decisions.

Additionally, CARTO's rapid spatial analysis capabilities accelerated our analysis process, empowering us to make data-driven decisions more efficiently. The platform's advanced visualization capabilities facilitated effective communication of findings and aided in building impactful solutions tailored to NH Hotels Group's specific needs.

### 2.1 Data Acquisition & Preprocessing
#### 2.1.1 Datasets
The foundation of our analysis is a robust collection of datasets that provide a comprehensive view of Madrid's tourism landscape. We focused on acquiring data that could offer insights into pedestrian traffic patterns, existing tourist accommodations, and points of interest - three key factors that significantly influence the success of a hotel location.

**Pedestrian Traffic Data**: We utilized two pedestrian datasets to understand the flow of foot traffic across the city. The first dataset, accessible through the [Madrid Open Data Portal - Pedestrian and bicycle capacity](https://datos.madrid.es/portal/site/egob/menuitem.c05c1f754a33a9fbe4b2e4b284f1a5a0/?vgnextoid=695cd64d6f9b9610VgnVCM1000001d4a900aRCRD&vgnextchannel=374512b9ace9f310VgnVCM100000171f5a0aRCRD&vgnextfmt=default), provides granular data on pedestrian traffic on selected streets in Madrid from 2019 to June 2021. This dataset offers a historical perspective, allowing us to identify long-term trends and patterns in pedestrian movement. The second dataset, sourced from the [CARTO demo tables](https://clausa.app.carto.com/data/explorer/carto_dw/carto-demo-data/demo_tables/madrid_est_pedestrian_traffic), offers more recent data but is limited to the center of Madrid. Despite its spatial and temporal limitations, this dataset is invaluable for its insights into the most recent pedestrian traffic trends in one of Madrid's most tourist-heavy areas.

The pedestrian data was processed using a [Python notebook](https://colab.research.google.com/drive/1YSLiIRLenV-iwKi4YFTwBYeW-v8SAJUx?usp=sharing), where we cleaned and standardized the data, converted date and time information into a timestamp format, handled missing values, and converted latitude and longitude data into geometric points for geospatial analysis.

**Existing Tourist Accommodations**: To understand the current landscape of tourist accommodations in Madrid, we incorporated data from the [Madrid Open Data Portal - Accommodation in the city of Madrid](https://datos.madrid.es/portal/site/egob/menuitem.c05c1f754a33a9fbe4b2e4b284f1a5a0/?vgnextoid=df42a73970504510VgnVCM2000001f4a900aRCRD&vgnextchannel=374512b9ace9f310VgnVCM100000171f5a0aRCRD&vgnextfmt=default). This dataset provides comprehensive information about existing accommodations, including hotels, hostels, pensions, and campsites. It offers insights into the distribution of accommodations across the city, their types, and their proximity to key points of interest.

**Points of Interest**: Points of interest data, sourced from the [OpenStreetMap Nodes via the CARTO Data Observatory](https://clausa.app.carto.com/data/observatory/openstreetmap/subscriptions/osm_nodes_205a5f56), provides information about key attractions in Madrid. This includes cultural heritage sites, performing arts venues, gastronomical hotspots, and other attractions that draw tourists to the city. The proximity of a hotel to these points of interest can significantly influence its attractiveness to potential guests.

**Pedestrian and Building Data**: To further enrich our analysis, we incorporated pedestrian data and building data from the CARTO Data Observatory. The demographic data, including age and income information, helped us understand the socio-economic landscape of different areas in Madrid. The building data, sourced from the [CARTO demo tables](https://clausa.app.carto.com/data/explorer/carto_dw/carto-demo-data/demo_tables/inspire_buildings_madrid), provided insights into the physical landscape of the city, which could influence the feasibility of establishing a new hotel in certain locations.

#### 2.1.2 Preprocessing
To ensure the data was in an optimal state for analysis, both the pedestrian and accommodation data underwent thorough preprocessing steps in a [Colab Python notebook](https://colab.research.google.com/drive/1YSLiIRLenV-iwKi4YFTwBYeW-v8SAJUx?usp=sharing). 

The pedestrian data was cleaned, standardized, timestamps were created, missing values were handled, and geospatial points were generated. For the accommodations data, relevant information was extracted, incomplete entries were removed, star ratings were converted to numerical format, and hotel brands were classified using internet research for competitor analysis. The remaining datasets, including pedestrian data, building data, and OpenStreetMap Nodes for points of interest, were processed using Google's BigQuery. This powerful tool allowed us to handle large volumes of data efficiently, performing operations such as filtering, aggregation, and spatial joins. The processed data was then integrated into our analysis, providing a more comprehensive view of Madrid's tourism landscape.

In addition to utilising BigQuery, we incorporated workflows, a newly introduced tool within the Carto Platform, to preprocess our base data specifically for the study area. These workflows proved instrumental in managing the intricacies of data processing tasks associated with the study area. By effectively utilising workflows, we streamlined the data preparation process, ensuring that the data was in an optimal state for further analysis.

  <img src="https://i.ibb.co/GQ5JTKZ/Screenshot-2023-07-05-at-05-49-09-2x.png" alt="Workflow study">
<figcaption><small><strong>Workflow 1.</strong> Creation of study area and spatial indexes and area and centroid calculation operations.</small></figcaption>

Furthermore, we introduced workflows, a newly introduced tool within the Carto Platform, to streamline the data preparation process specifically for the study area. The workflows played a crucial role in managing the various data processing tasks related to our study area. By leveraging the capabilities of these workflows, we were able to streamline the preprocessing of our base data, particularly for the map creation. This included handling data extraction, transformation, and loading operations in a systematic and organised manner.

By incorporating workflows into our data processing pipeline, we achieved enhanced efficiency and reproducibility. The workflows provided a structured framework for executing tasks, enabling us to maintain consistency and accuracy throughout the process. This systematic approach not only saved time but also ensured that our data was processed consistently and reliably.

Given the constraints of data availability, our study area was carefully selected to maximise the insights derived from the available pedestrian traffic data. This data, despite its high level of granularity, was restricted to the central area of Madrid, specifically within the boundaries of the M-30 motorway network. Consequently, we focused our analysis within this defined study area, which spans an approximate area of 37.72 km2 and 2439 h3 cells resolution 10. This deliberate choice allowed us to concentrate our efforts on a specific and meaningful subset of Madrid's tourism landscape, enabling us to gain a deeper understanding of the dynamics within this region.

To extract relevant points of interest (POIs) from OpenStreetMap (OSM) for visualization and analysis, we used a SQL query. The query selected POIs based on specific tags, such as museums, attractions, theatres, restaurants, cafes, parks, and gardens. The retrieved data included the name and geographical coordinates (latitude and longitude) of each POI. 

The points of interest data has been categorized into four main categories: "patrimony, museum and monuments", "theatre and arts", "gastronomy", and "leisure." This categorization allows for a clearer understanding of the different types of attractions and amenities available in Madrid. 

<div class="code-block">
  <pre>
    <code>
      CREATE TABLE `carto-dw-ac-vs5d76ww.shared.madrid_osm_poi_study_area` AS
WITH poi_data AS (
  SELECT 
    ROW_NUMBER() OVER() AS osm_tourism_poi_id,
    names.value AS poi_name,
    CASE 
      WHEN tags.value IN ('museum', 'attraction', 'gallery', 'viewpoint', 'monument', 'memorial') THEN 'patrimony_monuments_museums'
      WHEN tags.value IN ('theatre', 'cinema', 'arts_centre') THEN 'theatre_arts'
      WHEN tags.value IN ('cafe', 'restaurant', 'bar', 'pub') THEN 'gastronomy'
      WHEN tags.value IN ('park', 'garden', 'zoo', 'aquarium', 'theme_park', 'stadium', 'sports_centre', 'swimming_pool', 'golf_course') THEN 'leisure'
    END AS poi_category,
    do_geom.geom AS geom,
    do_data.geoid AS geoid
  FROM 
    `carto-data.ac_vs5d76ww.sub_openstreetmap_pointsofinterest_nodes_esp_latlon_v1_quarterly_v1` do_data
  INNER JOIN 
    `carto-data.ac_vs5d76ww.sub_openstreetmap_geography_esp_latlon_v1` do_geom 
  ON 
    do_data.geoid = do_geom.geoid
  INNER JOIN 
    `carto-dw-ac-vs5d76ww.shared.madrid_study_area` AS study_area
  ON 
    ST_Contains(study_area.geom, do_geom.geom),
    UNNEST(
      ARRAY(
        SELECT AS STRUCT key, value
        FROM UNNEST(do_data.all_tags)
        WHERE key IN ('tourism', 'amenity', 'shop', 'leisure')
      )
    ) AS tags,
    UNNEST(
      ARRAY(
        SELECT AS STRUCT value
        FROM UNNEST(do_data.all_tags)
        WHERE key = 'name'
      )
    ) AS names
)
SELECT 
  ANY_VALUE(CASE WHEN poi_category = 'patrimony_monuments_museums' THEN poi_name END) AS patrimony_monuments_museums,
  ANY_VALUE(CASE WHEN poi_category = 'theatre_arts' THEN poi_name END) AS theatre_arts,
  ANY_VALUE(CASE WHEN poi_category = 'gastronomy' THEN poi_name END) AS gastronomy,
  ANY_VALUE(CASE WHEN poi_category = 'leisure' THEN poi_name END) AS leisure,
  ANY_VALUE(geom) AS geom,
  geoid
FROM poi_data
GROUP BY geoid
HAVING
  MAX(CASE WHEN poi_category = 'patrimony_monuments_museums' THEN poi_name END) IS NOT NULL
  OR MAX(CASE WHEN poi_category = 'theatre_arts' THEN poi_name END) IS NOT NULL
  OR MAX(CASE WHEN poi_category = 'gastronomy' THEN poi_name END) IS NOT NULL
  OR MAX(CASE WHEN poi_category = 'leisure' THEN poi_name END) IS NOT NULL;
    </code>
  </pre>
</div>



The processed data was then utilized to create visualizations and maps that provide a better understanding of the variables and exploratory analysis. For example, the pedestrian heatmap shows the highest concentration of pedestrians from our target audience (people between 40 and 69 years old with mid-high income) in the districts of Salamanca and Chamberí. By zooming in on the map, we can observe time series analysis of pedestrian traffic in selected streets, particularly in the low emission zone of Madrid. This analysis covers the period from January 2019 to June 2021.

To enhance the interactivity and flexibility of the visualizations, we have incorporated SQL parameters, a recently released feature. SQL Parameters are placeholders that can be used on any SQL Query data source in Builder. With this feature, users can define parameters and set their actual values through a control UI in the right side panel's 'Parameters' tab. This allows both Editor and Viewer users to manipulate the actual SQL Query through a user-friendly interface.

By leveraging SQL parameters, the data on the map can be dynamically filtered based on specific criteria or user preferences. For example, users can filter the pedestrian count  by date. Additionally, widgets were added to the map interface, enabling viewers to interactively adjust the visualization based on their preferences.


In addition to the previous mentioned features, we have further enhanced the map with interactive elements to provide a richer user experience. One notable addition is the integration of interactivity when hovering over hotels on the map. As users hover over a hotel icon, a side panel is dynamically displayed, offering detailed information about the selected hotel. This interactive feature allows users to access relevant qualitative information, enabling a deeper understanding of each hotel's unique characteristics and attributes.

Furthermore, we have incorporated interactivity into the pedestrian count feature. As users explore the map, they can now observe the number of pedestrians per street directly on the map interface. This real-time display of pedestrian counts provides valuable insights into the foot traffic patterns and allows users to identify streets with higher pedestrian activity. By incorporating this interactivity, NH Hotels Group gains a more comprehensive understanding of the pedestrian flow across different areas of Madrid, aiding in their decision-making process for optimal hotel site selection.

These interactive elements significantly enhance the usability of the map, empowering NH Hotels Group to explore and analyze the data with greater depth and efficiency. The combination of interactive hotel information panels and pedestrian counts adds a new level of interactivity and engagement, facilitating NH Hotels Group' decision-making process and enabling them to make informed choices based on a holistic understanding of both qualitative and quantitative data.

<iframe width="1280px" height="720px" src="https://clausa.app.carto.com/map/51125179-58c9-47fa-9f23-022d86f0c120"></iframe>


By visualizing this information on the map, NH Hotels Group gains a solid foundation for conducting exploratory analysis and gaining valuable insights into the variables and their relationships. This initial map serves as a valuable resource for NH Hotels Group in their decision-making process and strategy for hotel site selection in Madrid.

By examining the distribution of points of interest and their proximity to existing tourist accommodations, NH Hotels Group can identify areas with high potential for attracting guests. They can also assess the competitive landscape in terms of nearby attractions and amenities. This knowledge empowers NH Hotels Group to make informed decisions about where to establish new hotels or expand their existing presence in Madrid.

This initial map serves as a foundation for understanding the data, conducting exploratory analysis, and gaining insights into the variables and their relationships. It provides NH Hotels Group with valuable information to inform their decision-making process and strategy for hotel site selection in Madrid.

### 2.2. Accessibility and Proximity Analysis

To gain insights into the accessibility of key attractions in Madrid, we conducted an in-depth accessibility analysis using isochrone intersection analysis. This analysis allowed us to understand the spatial relationships and convenience of various points of interest (POI) categories within a 15-minute walking distance.

Within Workflow 2, we initiated the creation of isochrones representing 15-minute walking distances from each POI within the categories of "Patrimony, Monuments and Museums," "Theaters and Arts," "Gastronomy," and "Leisure." These isochrones served as spatial boundaries, illustrating what a tourist could conveniently access within a quarter of an hour's walk from each respective POI. 

<img src="https://i.ibb.co/yXKSX1C/Screenshot-2023-07-05-at-06-20-35-2x.png" alt="Workflow study">
<figcaption><small><strong>Workflow 2.</strong> Creation of 15-minute walking isochrones for the different POI categories and their intersection and aggregation.</small></figcaption>

The isochrones were then spatially aggregated and intersected to identify zones of overlap. These overlapping zones indicated areas where tourists could conveniently access a diverse range of attractions within a 15-minute walking distance. These areas emerged as highly desirable locations for hotels, offering optimal convenience to tourists.

The accessibility analysis carried out through Workflow 2 played a critical role in identifying areas that provided the utmost convenience for tourists interested in Madrid's cultural heritage, performing arts scene, gastronomy, and leisure activities. By understanding the intersecting zones, we could pinpoint the regions that offered the most accessible and vibrant experience for tourists, aiding in strategic decision-making for the placement of accommodations and highlighting key areas of interest within the city.

In addition to the isochrone intersection analysis, we took into account the proximity between NH Hotels Group location. This consideration aimed to avoid cannibalization, which occurs when a new hotel draws customers away from nearby NH Hotels Group.

To assess this proximity, we performed an analysis using a SQL query. We defined a buffer area to encompass the study area in Madrid, and then selected NH Hotels Group within that buffer zone. Specifically, we focused on NH Hotels Group and located within the study area.

Next, we created a grid of hexagons to represent different potential hotel locations. For each hexagon in the grid, we calculated the minimum distance to the closest NH Hotel. This distance metric helped us understand the proximity of each potential hotel location to existing NH Hotels Group.
```sql
DECLARE madrid_buffer GEOGRAPHY;
SET madrid_buffer = ST_BUFFER(ST_GEOGPOINT(-3.70000775514063, 40.4150453503748), 3500);

WITH NH_hotels AS (
 SELECT `carto-un`.carto.H3_FROMGEOGPOINT(geom, 10) AS h3
 FROM nh_hotels_table
 WHERE ST_CONTAINS(madrid_buffer, geom) 
 AND brand = 'NH_%'
),

h3_grid AS (
 SELECT h3
 FROM h3_grid_table
)

SELECT h3_grid.h3, MIN(`carto-un`.carto.H3_DISTANCE(h3_grid.h3, NH_hotels.h3)) AS dist
FROM NH_hotels
CROSS JOIN h3_grid
GROUP BY h3_grid.h3;
```


This proximity data, along with the coverage of 15-minute walk isochrones from tourist points of interest, were used to enrich our analysis. These factors helped us identify locations that not only offer high accessibility to key attractions but also maintain a healthy distance from existing NH Hotels Group, ensuring a balanced distribution of accommodations across the city.
<iframe width="1280px" height="720px" src="https://clausa.app.carto.com/map/d973dc67-828d-414c-bc74-3cc839221e98"></iframe>

The results of the accessibility analysis were visualized on a map. The map displayed the aggregated isochrones representing accessible areas within a 15-minute walk from various POI categories including "patrimony, museum and monuments", "theatre and arts", "gastronomy", and "leisure". The overlapping areas of the isochrones highlighted regions that offered diverse attractions within a short walking distance, making them desirable for hotel development.

The first isochrone, shown in blue, represents the intersection of these aggregated isochrones. It highlights the areas where multiple categories of POIs overlap, indicating locations that offer easy access to diverse attractions within a short walking distance. These areas are particularly desirable for hotel development as guests can conveniently explore a variety of cultural, artistic, culinary, and leisure experiences.

Additionally, in the map  we can the location of hotels that fall within this aggregated isochrone. These hotels are strategically positioned to ensure that guests can reach the POIs belonging to the different categories within a 15-minute walk. By staying at these hotels, visitors have the advantage of convenient access to a range of attractions without the need for extensive travel.

This visualization provides NH Hotels Group with valuable insights into the distribution of isochrones, the areas of overlap, and the location of hotels within the desired accessibility range. It allows NH Hotels Group to identify specific areas where the concentration of diverse POIs and hotel accommodations create a favorable environment for attracting and satisfying guests.

By leveraging this information, NH Hotels Group can make informed decisions regarding the selection of hotel sites that offer the best proximity to popular attractions and enhance the overall guest experience. This strategic approach ensures that NH Hotels Group can position their establishments in areas with high tourist appeal and optimize their market presence in Madrid.

### 2.3 Spatial Index Enrichment

To enhance the granularity and precision of our analysis, we incorporated the H3 spatial indexing system using the CARTO Analytics Toolbox. Spatial indexes, like H3, are global discrete grids that cover the entire globe. They are designed to efficiently process and query spatial data, making spatial analysis faster and more accurate.
    
For our analysis, we used an H3 resolution of 10. This resolution level was chosen because it provides a good balance between spatial precision and computational efficiency, particularly for a city center like Madrid. At this resolution, each hexagon covers an area of approximately 0.015 square kilometers, which is suitable for capturing the spatial variations in pedestrian traffic by age and income and number of visitors, points of interest density, and the minimun distance between NH Hotels Group.

By using the H3 spatial indexing system, we were able to create an enriched grid that integrated various variables, including demographic data, hotel locations, and points of interest density. This enriched grid map provides a more detailed and accurate view of potential hotel locations, allowing us to identify optimal locations with greater precision. This approach ensures that our analysis is grounded in a robust understanding of the spatial dynamics of Madrid's city center.

<iframe width="1280px" height="720px" src="https://clausa.app.carto.com/map/d5e61e72-4097-4d5e-ab25-b25c48e271e8"></iframe>

This map provides valuable insights obtained by enriching the spatial index with our data using an H3 resolution of 10. On the left side of the map, we can observe the concentration of pedestrians belonging to our target audience. This information allows NH Hotels Group to identify areas with high pedestrian activity, indicating popular tourist spots and potential hotspots for hotel development. By strategically positioning their hotels in these areas, NH Hotels Group can attract more guests and cater to their preferences, enhancing customer satisfaction and driving business growth.

On the right side of the map, we have the visualization of the minimum distances between existing NH Hotels Group. This information is crucial to avoid cannibalization and ensure a balanced distribution of accommodations across the city. By maintaining an appropriate distance between NH Hotels Group, NH Hotels Group can optimize their market presence and prevent customers from being drawn away from existing locations. The map assists NH Hotels Group in identifying gaps in coverage and strategically selecting new hotel sites that maximize accessibility to key attractions while minimizing competition with their own properties. 



### 2.4 Spatial Correlation, Hotspot Detection Analysis

In our analysis to identify ideal hotel sites in Madrid, we employed spatial correlation and hotspot detection techniques. To determine the importance of each variable, we assigned weights based on their relevance to identifying ideal hotel sites. Factors such as visitor demographics, covered percentage, distance from existing NH Hotels Group, count of patrimony monuments and museums, count of gastronomy establishments, count of leisure facilities, and count of theater and arts venues were considered.


To achieve this, we utilized the following procedures 

Sections:
- Spatial Correlation and Geographically Weighted Regression (GWR)
- Composite Score Calculation
- Hotspot Detection using Getis Ord Statistics

#### 2.4.1 Geographically Weighted Regression (GWR)

Geographically Weighted Regression (GWR) is a powerful analytical technique that helps us understand the spatial correlations between the target variable (our target audience) and the correlation variables (such as the count of points of interest per category and the percentage of area covered by them). GWR allows us to account for spatial heterogeneity, recognizing that the relationships between variables may vary across different locations within Madrid.

To perform GWR, we divided the study area into a grid of cells. For each cell, a local regression model was created, taking into account the data from neighboring cells within a specified neighborhood. The weights assigned to the neighboring cells were determined using the Gaussian kernel function, which means that closer cells had higher weights, while cells further away had lower weights.

The GWR analysis provided us with coefficients for each cell, indicating the relationship between the coefficient and the target variable. Positive coefficients indicate a positive relationship, while negative coefficients indicate a negative relationship. A coefficient of 0 suggests no relationship.

By conducting GWR, we were able to capture the localized impacts of different variables and uncover spatial patterns. This analysis helped us understand how factors such as the count of points of interest per category and the percentage of area covered by them influence the suitability of hotel locations in Madrid. It allowed us to identify areas where specific factors have a stronger influence, enabling NH Hotels Group to prioritize locations that align with their target audience and preferences.

Geographically Weighted Regression (GWR) was performed to understand the spatial correlations between the target variable, our target audience, and the correlation variables including the count of POI per category, the percentage of area covered by them. GWR allows us to account for spatial heterogeneity and better understand how different variables influence the suitability of hotel locations in Madrid. By applying weights to neighboring cells using the Gaussian kernel function, GWR captures the localized impacts of these variables and helps us uncover spatial patterns.

```sql
CALL `carto-un`.carto.GWR_GRID(
  -- Source Spatial Index grid
  'carto-dw-ac-vs5d76ww.shared.madrid_h3_study_area_enriched_final_NH',
  -- Correlation variables
  ['patrimony_monuments_museums_count', 'theatre_arts_count', 'gastronomy_count', 'leisure_count', 'covered_percentage', 'NH_distance'],
  -- Target variable
  'visitors_midhigh_40_69_sum',
  -- Index column, index type, k-ring distance, kernel function
  'h3', 'h3', 3, 'gaussian', TRUE,
  -- Output table
  'carto-dw-ac-vs5d76ww.shared.madrid_h3_GWR'
);
```

 We used the H3 spatial index grid and set the k-ring distance to 3, indicating the neighborhood size around each cell. The Gaussian kernel function was applied to assign weights to neighboring cells, with closer cells having higher weights. 
 <iframe width="1280px" height="720px" src="https://clausa.app.carto.com/map/d3d79b28-bd83-4ce2-a679-ce66ce744d29"></iframe>

#### 2.4.2 Composite Score

After performing the geographically weighted regression (GWR) analysis and gaining a better understanding of the spatial relationships between variables, we proceeded to calculate composite scores.  The composite scores provide a comprehensive assessment of each potential hotel site by combining and weighting the relevant factors.

There are various methods to compute composite scores, each with its own advantages and considerations. In this analysis, we have chosen the "CUSTOM_WEIGHTS" method because we have access to data from the 2019 Tourist Perception Survey conducted by the Tourist Intelligence Centre of Madrid Destino. This survey provides valuable insights into visitor preferences and allows us to assign weights to different variables based on their importance.

The selection of an appropriate scoring method depends on various factors, as illustrated in the diagram below:

![](https://3078048011-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FybPdpmLltPkzGFvz7m8A%2Fuploads%2FwrLEgV6REq3bQcde71QI%2Fimage.png?alt=media&token=1b6a4a97-53de-4e0b-bc16-89df06c3389f)

As shown in the diagram above, the choice of the scoring method depends on the availability of expert knowledge: when this is available, the recommended choice for the scoring_method parameter is CUSTOM_WEIGHTS, which allows the user to customize both the scaling and the aggregation functions as well as the set of weights.

Using the "CUSTOM_WEIGHTS" method, we assign weights to each variable based on its relevance and impact on the overall assessment. These weights reflect the relative importance of each factor in influencing the desirability of potential hotel locations. By incorporating these weights, we create a composite score that takes into account the specific factors that are most significant for hotel development in Madrid.

By assigning weights to each variable based on their importance, we create a composite score that takes into account the relative significance of each factor. This process allows us to evaluate the suitability of each location for hotel development in a more comprehensive manner. The composite scores enable us to rank the sites and identify those with the highest potential for success.

To establish the weights, we referred to the 2019 Tourist Perception Survey, which revealed the preferences of visitors to Madrid. We focused on the categories of Patrimony, Arts, Gastronomy, and Leisure as they directly influence location desirability for potential guests. The percentages for these categories were normalized to reflect their relative importance within the total weight, ensuring a comprehensive analysis that considers diverse reasons for visiting Madrid.

To assign weights to the variables in our analysis, we referred to the 2019 Tourist Perception Survey conducted by the Tourist Intelligence Centre of Madrid Destino. The survey collected data from over 1,600 visitors and provided valuable insights into the reasons visitors choose to come to Madrid. From the survey, we observed the following percentages for different categories:

- Patrimony: 33.16%
- Arts: 20.42%
- Gastronomy: 17.73%
- Leisure: 13.49%
- Visit family or friends: 4.01%
- Other: 11.19%

Based on the relevance of these categories to the hotel industry and their influence on location desirability, we focused our analysis on the categories of Patrimony, Arts, Gastronomy, and Leisure. We excluded the categories "Visit family or friends" and "Other" from the normalization process, as they were not considered in the assignment of weights.

To represent the relative importance of these chosen categories within the total weight, we performed normalization. Each percentage was divided by the sum of the percentages of the considered categories (Patrimony, Arts, Gastronomy, and Leisure), and then multiplied by the remaining weight after assigning a 20% to each of the following factors: visitors_midhigh_40_69_sum, covered_percentage, and NH_distance.

This normalization process resulted in the following weights for the chosen categories:

- `patrimony_monuments_museums_count`: 15.644%
- `gastronomy_count`: 8.364%
- `leisure_count`: 6.364%
- `theatre_arts_count`: 9.64%

and adding the other three variables: 
- `visitors_midhigh_40_69_sum`: 20%
- `covered_percentage`: 20%
- `NH_distance`: 20%



These weights sum up to 100%, ensuring that they accurately represent the relative proportions of each category within the total weight. By incorporating these weights into our analysis, we can better understand the significance of each category and its influence on the suitability of potential hotel locations in Madrid.

To calculate the composite scores, we use the CREATE_SPATIAL_COMPOSITE_UNSUPERVISED procedure from CARTO Analytics Toolbox for BigQuery. This procedure allows us to combine the variables, apply customized weights, and perform scaling to ensure comparability across different variables. We chose the "STANDARD_SCALER" method for scaling, which standardizes the variables by subtracting the mean and dividing by the standard deviation.


```sql
CALL `carto-un`.carto.CREATE_SPATIAL_COMPOSITE_UNSUPERVISED(
  -- Input table
  'carto-dw-ac-vs5d76ww.shared.madrid_h3_study_area_enriched_final_NH',
  -- Unique index
  'h3',
  -- Output table name
  'carto-dw-ac-vs5d76ww.shared.madrid_hotel_composite_index_NH',
  -- Options
  '''
  {
    "scoring_method": "CUSTOM_WEIGHTS",
    "weights": {
      "visitors_midhigh_40_69_sum": 0.20,
      "covered_percentage": 0.20,
      "NH_distance": 0.20,
      "patrimony_monuments_museums_count": 0.1564,
      "gastronomy_count": 0.0836,
      "leisure_count": 0.0636,
      "theatre_arts_count": 0.0964
    },
    "scaling": "STANDARD_SCALER",
    "return_range": [0.0,1.0]
  }
  '''
);
```



The variables were scaled using the STANDARD_SCALER method, which subtracts the mean and divides by the standard deviation. The resulting composite scores were normalized to the range [0.0, 1.0].

The computed composite scores provide a comprehensive assessment of each potential hotel site in Madrid, taking into account the weighted factors derived from the tourism report. By analyzing and visualizing these scores, we can identify areas with the highest potential for hotel development success and make informed decisions based on the composite scores and spatial analysis.

#### 2.4.3 Hotspot Detection

To conduct hotspot detection and gain valuable insights into the spatial distribution of desirable hotel sites in Madrid, we utilized the COMMERCIAL_HOTSPOTS procedure. This powerful analysis technique leverages the Getis Ord Gi* statistic to identify clusters of high-ranking locations where multiple factors align, indicating areas with a higher potential for success and profitability.

In our analysis, we carefully selected a dataset containing relevant information about potential hotel sites and their associated variables. These variables were chosen based on their influence in determining the desirability of hotel sites, encompassing visitor demographics, accessibility, cultural attractions, and leisure amenities.

To account for the varying importance of each variable, we assigned weights to them during the hotspot analysis. These weights reflected their relative significance in influencing the desirability of potential hotel locations. By incorporating these weights, we ensured that the analysis captured the true importance of each factor in identifying hotspots.

The kring parameter played a vital role in the hotspot analysis, determining the size of the neighborhood considered within the analysis. With a value of 3, we included cells within a radius of 3 units from the origin cell, allowing us to detect spatial clusters within a specified distance.

Moreover, we set a p-value threshold of 0.05 to determine the significance level for hotspot identification. Cells with p-values below this threshold were identified as hotspots, indicating a statistically significant clustering of high-ranking locations. This approach helped us identify areas where desirable hotel sites tend to cluster together, providing valuable insights for NH Hotels Group' decision-making process.

By conducting the Getis Ord hotspot analysis through the COMMERCIAL_HOTSPOTS procedure, we pinpointed specific regions in Madrid where multiple factors aligned to create hotspots of desirable hotel sites. These hotspots represented areas with a higher concentration of favorable attributes that contribute to their desirability.

Finally, we conducted hotspot detection using the COMMERCIAL_HOTSPOTS procedure. 


```sql
CALL `carto-un`.carto.COMMERCIAL_HOTSPOTS(
  'carto-dw-ac-vs5d76ww.shared.madrid_h3_study_area_enriched_final_NH',
  'carto-dw-ac-vs5d76ww.shared.madrid_h3_study_area_commercial_hotspots_NH',
  'h3',
  'h3',
  ['visitors_midhigh_40_69_sum', 'covered_percentage', 'NH_distance', 'patrimony_monuments_museums_count', 'gastronomy_count', 'leisure_count', 'theatre_arts_count'],
  [0.20, 0.20, 0.20, 0.1564, 0.0836, 0.0636, 0.0964],
  3,
  0.05
);
```

The identification of these hotspots empowers NH Hotels Group to strategically focus their attention and allocate resources to areas with the highest potential for success and profitability. By capitalizing on these insights, NH Hotels Group can make informed decisions regarding site selection and prioritize their investments in locations that offer the most promising opportunities.

In summary, our hotspot detection analysis using the COMMERCIAL_HOTSPOTS procedure allowed us to identify clusters of high-ranking locations in Madrid. These clusters represent areas where multiple factors align to create hotspots of desirable hotel sites. By leveraging this spatial analysis technique, NH Hotels Group can strategically plan their expansion and optimize their decision-making process for site selection, ultimately enhancing their chances of success in the competitive hotel industry.
<iframe width="1280px" height="720px" src="https://clausa.app.carto.com/map/a6b9411a-7273-4ab4-ae63-037c91c95b94"></iframe>

Through the synergistic integration of geographically weighted regression (GWR), the creation of a composite score based on weighted factors, and hotspot detection using Getis Ord statistics, our analysis has provided us with a holistic and comprehensive understanding of the ideal hotel sites in Madrid. By incorporating these sophisticated techniques, we were able to examine multiple factors simultaneously, revealing crucial insights that are invaluable for NH Hotels Group' strategic decision-making process in hotel site selection.

Geographically weighted regression (GWR) allowed us to unravel the spatial correlations and localized impacts of various variables, enabling a deeper understanding of how different factors influence the suitability of hotel locations. By assigning weights to each variable based on their significance, we created a composite score that accurately reflects the relative importance of each factor. This composite score served as a powerful tool to rank and prioritize potential hotel sites in Madrid.

Additionally, our hotspot detection analysis using Getis Ord statistics enabled us to identify clusters of high-ranking locations, representing areas with a higher concentration of favorable attributes. These hotspots highlighted regions where multiple factors aligned, indicating their desirability and potential for success.

By combining these advanced techniques, we have gained valuable insights that go beyond individual variables and isolated analyses. Our comprehensive approach has provided NH Hotels Group with a robust foundation for strategic decision-making, offering a clearer understanding of the ideal hotel sites in Madrid and maximizing the chances of success in the competitive hotel industry.
  
### 2.5 Competitive Proximity and Dispersion Analysis using Local Outlier Factor and KNN 

The Competitive Proximity and Dispersion Analysis, utilizing the Local Outlier Factor (LOF) and K-nearest neighbors (KNN) methodologies, provides NH Hotels Group with valuable insights into the spatial distribution and proximity of hotels in Madrid. This analysis reveals areas of high competition and potential cannibalization, helping NH Hotels Group select the best location from their identified commercial hotspots.

#### 2.5.1 Local Outlier Factor (LOF)
The Local Outlier Factor (LOF) algorithm is a powerful tool for detecting outliers and anomalies within a dataset. It measures the density deviation of a data point compared to its neighbors. If a point has a much lower density than its neighbors, it is considered an outlier and receives a high LOF score (>1).

In the context of analyzing hotel distribution, LOF helps identify outliers that deviate from the expected clustering pattern. For example, a hotel located on the edge of the study area where most hotels are clustered in the core would have a high LOF score. Conversely, if hotels are sparsely distributed across a town, the LOF score would be lower (<1) as there is no significant clustering behavior among its neighbors.

To calculate the LOF, users must specify the value of k, which represents the distance to the kth nearest neighbor. A smaller k-value, such as 5, produces more localized results but is more sensitive to noise in the data.

In our analysis, we used the carto-un.carto.LOF function to compute the LOF scores for hotel locations in Madrid. We chose a threshold of 1.2 to identify areas of high competition, where hotels are in very close proximity to each other. By filtering for LOF scores below 1.2, we can focus on these areas and gain insights into intense competition and potential market saturation.

```sql
CREATE OR REPLACE TABLE `carto-dw-ac-vs5d76ww.shared.madrid_hotels_competitors_NH_LOF_analysis` AS
WITH lof_output AS (
    -- We calculate the Local Outlier Factor in order to identify hotels without competition.
    SELECT `carto-un`.carto.LOF(ARRAY_AGG(STRUCT(CAST(id AS STRING), geom)), 5) as lof 
    FROM `carto-dw-ac-vs5d76ww.shared.madrid_hotels_brand_id`
    WHERE brand != 'NH_%'
)
SELECT lof.* 
FROM lof_output, UNNEST(lof_output.lof) AS lof
WHERE lof.lof < 1.2;
```

The insights provided by LOF empower NH Hotels Group to strategically allocate resources, identify untapped market opportunities, and optimize their hotel portfolio. By avoiding locations with excessive hotel density and focusing on areas with higher demand, NH Hotels Group positions itself for long-term success and profitability.

Moreover, ensuring a balanced distribution of accommodations across the city enhances NH Hotels Group' competitiveness and contributes to the overall development and sustainability of the hotel industry in Madrid.

By leveraging the valuable insights from LOF, NH Hotels Group makes informed decisions, avoids concentration in specific areas, and optimizes its market presence. This strategic approach enables NH Hotels Group to focus on areas with higher demand and better potential for success.

#### 2.5.2 K-nearest neighbors (KNN)
KNN is a machine learning algorithm utilized in the Competitive Proximity and Dispersion Analysis to assess the spatial relationship between hotels in Madrid. It measures the proximity between data points and helps NH Hotels Group understand the distances between existing hotels and potential new locations. By analyzing the distances, NH Hotels Group can identify clusters and patterns of hotel distribution, enabling them to strategically position their new hotel to avoid cannibalization with existing establishments and ensure a healthy competitive landscape.

To implement the KNN analysis, we utilized the carto-un.carto.KNN function in SQL. We first prepared a dataset of hotels within the study area, including their unique identifiers, geometry, stars rating, and brand. Then, by applying the KNN function with a k-value of 10, we determined the nearest neighbors for each NH Hotel location. The resulting output provides information about the NH Hotel, its neighboring hotels, their distances, and stars ratings, allowing NH Hotels Group to make strategic decisions based on the spatial relationships and competition in the market.healthy distance from existing hotels, avoiding excessive competition and optimizing their market presence.


```sql
WITH hotels AS (
    SELECT 
        CONCAT(brand, '_', CAST(ROW_NUMBER() OVER(PARTITION BY brand ORDER BY name) AS STRING)) AS id,
        geom, stars_rating, brand
    FROM `carto-dw-ac-vs5d76ww.shared.madrid_hotels_brand`
    WHERE ST_WITHIN(geom, (SELECT geom FROM `carto-dw-ac-vs5d76ww.shared.madrid_study_area`))
),
knn AS (
    SELECT 
        knn.*
    FROM UNNEST((SELECT `carto-un`.carto.KNN(ARRAY_AGG(STRUCT(id, geom)), 10) FROM hotels)) AS knn
    WHERE geoid LIKE 'NH_%' AND geoid_knn NOT LIKE 'NH_%'
)
SELECT 
    h.id AS NH_id,
    h.geom AS geom,
    h.stars_rating AS NH_stars,
    o.id AS other_id,
    o.geom AS other_geom,
    o.stars_rating AS other_stars,
    k.distance,
    k.knn,
    ST_MAKELINE(h.geom, o.geom) AS line_geom
FROM knn k
JOIN hotels h ON k.geoid = h.id
JOIN hotels o ON k.geoid_knn = o.id
ORDER BY NH_id, knn;
```
<iframe width="1280px" height="720px" src="https://clausa.app.carto.com/map/dad1bcc9-c728-48ff-8661-ee3ae27049f2"></iframe>

In our comprehensive analysis of Madrid's hotel industry, we employed advanced methodologies such as LOF (Local Outlier Factor) and KNN (K-nearest neighbors) to gain invaluable insights into the competitive landscape. Through this analysis, we were able to identify areas characterized by a high concentration of hotels, indicating intense competition and potential cannibalization among establishments.

By leveraging the insights derived from LOF and KNN, NH Hotels Group can make informed decisions regarding the optimal location for their new hotel within their identified commercial hotspots. The selection process takes into account various factors, including accessibility to key attractions and amenities, as well as the importance of maintaining a healthy distance from existing hotels. This strategic approach ensures NH Hotels Group can avoid excessive competition and optimize their market presence in Madrid.

The Competitive Proximity and Dispersion Analysis, supported by the robust LOF and KNN techniques, assumes a vital role in NH Hotels Group' expansion strategy. It provides them with the ability to identify areas of opportunity, gain a deep understanding of the competitive dynamics at play, and ultimately select the most optimal location for their new hotel. By effectively leveraging these insights, NH Hotels Group can position themselves strategically in the market, minimize cannibalization with existing establishments, and maximize their potential for long-term success and profitability within Madrid's fiercely competitive hotel industry.

#### 2.6 Methodological Key insights

**Data Acquisition & Preprocessing**

- Robust dataset collection provides a comprehensive view of Madrid's tourism landscape, including pedestrian traffic patterns, existing accommodations, and points of interest.
- Thorough preprocessing ensures data suitability through cleaning, standardization, and transformation, improving data quality and compatibility for analysis.

**Accessibility Analysis**

- Isochrone intersection analysis identifies areas with convenient access to diverse attractions within a short walking distance, aiding hotel site selection based on accessibility.
- Proximity analysis helps avoid cannibalization by maintaining appropriate distances between NH Hotels Group, optimizing market presence and guest satisfaction.

**Spatial Index Enrichment**

- H3 spatial indexing system enhances analysis granularity and precision by creating an enriched grid integrating demographic data, hotel locations, and points of interest density.
- Enriched spatial index map provides a deeper understanding of urban dynamics, aiding identification of areas with high tourist appeal and hotel development opportunities.

**Identification of Commercial Hotspots**
- Commercial hotspots represent areas with a high concentration of favorable attributes for hotel development.
- These hotspots indicate regions where visitor demographics, points of interest density, and accessibility align to create an environment conducive to hotel success.

**Factors Influencing Hotel Suitability**
- Geographically weighted regression (GWR) analysis reveals localized impacts and spatial correlations between variables.
- Factors such as patrimony, arts, gastronomy, leisure, visitor demographics, coverage percentage, and distance from existing NH Hotels Group significantly influence the suitability of potential hotel locations.

**Composite Scores for Site Evaluation**
- Composite scores are calculated by assigning weights to each relevant factor based on their importance.
- These scores provide a comprehensive assessment of each potential hotel site, allowing for ranking and prioritization based on the weighted factors.

**Hotspot Detection**
- Hotspot detection using Getis Ord statistics identifies clusters of high-ranking locations within the commercial hotspots.
- These clusters represent areas with a higher concentration of favorable attributes, indicating their desirability for hotel development.

**Competitive Proximity Analysis**
- Local Outlier Factor (LOF) and K-nearest neighbors (KNN) techniques assess the competitive landscape and proximity of existing hotels.
- This analysis helps understand areas of high competition and potential cannibalization among establishments.



## 3. Value of the Analysis for NH Hotels Group

NH Hotels Group stands to gain significant value from the comprehensive analysis conducted using geospatial data and advanced analytical techniques. The insights obtained from the analysis directly contribute to NH Hotels Group' growth, customer satisfaction, and profitability. By aligning the value proposition with NH Hotels Group' specific goals and challenges, the analysis becomes even more relevant and impactful.

### 3.1 Optimizing Location Selection for Growth

One of NH Hotels Group' key goals is to strategically expand its presence in Madrid. The analysis provides NH Hotels Group with a strategic advantage by identifying optimal locations for new hotel development. By considering factors such as pedestrian traffic patterns, proximity to popular points of interest, and minimizing cannibalization with existing NH Hotels Group, the analysis guides NH Hotels Group in selecting locations with the highest potential for success. This strategic approach ensures that NH Hotels Group can capture a significant share of the mid-high income population visiting Madrid while avoiding areas of high competition. By expanding in well-positioned locations, NH Hotels Group can drive growth and maximize their market presence.

### 3.2 Enhancing Customer Satisfaction

NH Hotels Group prioritizes customer satisfaction and aims to provide a superior guest experience. The analysis plays a pivotal role in this aspect by enabling NH Hotels Group to understand the preferences and needs of their target demographic. By selecting locations that offer a blend of luxury, convenience, and unique experiences, NH Hotels Group can ensure that their guests have access to popular attractions, cultural landmarks, and amenities that align with their interests. This tailored approach enhances customer satisfaction, fosters positive reviews and recommendations, and cultivates long-term loyalty. The analysis empowers NH Hotels Group to deliver exceptional guest experiences that keep customers coming back.

### 3.3 Gaining a Competitive Advantage

In a competitive hotel market like Madrid, NH Hotels Group strives to differentiate itself from competitors. The analysis provides NH Hotels Group with a competitive advantage by revealing areas of high hotel density and potential cannibalization. By avoiding locations with excessive competition and strategically positioning their new hotels in commercial hotspots, NH Hotels Group can ensure a balanced distribution of accommodations across the city. This approach not only maximizes NH Hotels Group' market share but also avoids dilution of their brand and resources. By leveraging the insights from the analysis, NH Hotels Group gains a competitive edge, allowing them to stand out and thrive in the highly competitive hospitality industry.

### 3.4 Ensuring Long-term Success

NH Hotels Group aims for sustainable growth and long-term success in Madrid. The analysis contributes to this goal by enabling NH Hotels Group to establish a strong presence and reputation in the market. By selecting optimal locations that cater to the target demographic, offer convenience, and reflect the local culture, NH Hotels Group can build a loyal customer base and foster brand loyalty. The strategic placement of hotels based on the analysis insights enhances NH Hotels Group' reputation as a trusted and preferred choice for visitors to Madrid. This long-term success translates into increased market share, revenue, and profitability.

In summary, the analysis provides NH Hotels Group with significant value in optimizing location selection, enhancing customer satisfaction, gaining a competitive advantage, and ensuring long-term success. By leveraging the insights and recommendations from the analysis, NH Hotels Group can drive growth, deliver exceptional guest experiences, differentiate from competitors, and establish a strong market presence in Madrid.





## 4. Leveraging CARTO for Enhanced Geospatial Analysis

NH Hotels Group recognizes the significant value derived from CARTO, a cloud-native GIS platform that enhances their geospatial analysis capabilities. This integration empowers NH Hotels Group to unleash the power of geospatial analytics, accelerate spatial analysis, and unlock deeper insights for effective decision-making.

### 4.1 Unleashing the Power of Cloud-Native GIS
CARTO's cloud-native architecture revolutionizes NH Hotels Group' geospatial analytics by providing scalability and flexibility. With self-hosted and hybrid deployment options, CARTO caters to the needs of modern data and GIS professionals. NH Hotels Group can now handle large volumes of geospatial data, perform complex analyses, and seamlessly scale their operations as they expand. CARTO's cloud-native approach ensures that NH Hotels Group can leverage the full potential of geospatial analytics at scale, driving innovation and growth.

### 4.2 Streamlined Spatial Analysis Workflow
CARTO streamlines NH Hotels Group' spatial analysis workflow, enabling data scientists, developers, and analysts to achieve speed and efficiency. By simplifying the spatial problem-solving process into four straightforward steps—Cloud Connectivity & Integrations, Data Enrichment, Spatial Analysis, and Solutions & Visualization—CARTO empowers NH Hotels Group to extract insights quickly. This streamlined workflow allows NH Hotels Group to optimize business processes, predict future outcomes, and make data-driven decisions in a timely manner. With CARTO, NH Hotels Group' teams can focus on extracting valuable insights rather than being overwhelmed by complex analysis procedures.

### 4.3 Uncovering Deeper Insights with Enriched Data
CARTO's Data Observatory offers NH Hotels Group a wealth of geospatial datasets, providing access to over 12,000 data sources. This includes "always-on" public and premium datasets such as points of interest (POIs), human mobility data, credit card transactions, and more. By incorporating these enriched datasets into their spatial analysis, NH Hotels Group gains the ability to uncover deeper insights into customer behavior, market trends, and other spatial factors influencing decision-making. CARTO's Data Observatory enhances NH Hotels Group' analytical capabilities and enables them to make informed, data-driven choices based on a comprehensive understanding of their target market.

### 4.4 Communicating Geospatial Insights Effectively
CARTO equips NH Hotels Group with powerful solutions and visualization tools to effectively communicate their geospatial insights. Through CARTO's solutions and visualization capabilities, NH Hotels Group can create interactive maps, charts, and dashboards that showcase their analysis results in a visually engaging manner. This enhances NH Hotels Group' ability to communicate findings, engage stakeholders, and facilitate data-driven decision-making across the organization. CARTO's visualization features empower NH Hotels Group to convey complex geospatial insights with clarity and impact, enabling effective communication of key findings and driving actionable outcomes.

### 4.5 Conclusions
The integration of CARTO into NH Hotels Group' geospatial analysis processes yields significant value by optimizing location selection, enhancing customer satisfaction, gaining a competitive advantage, and ensuring long-term success. By leveraging the insights and recommendations generated through geospatial analysis, NH Hotels Group can drive growth, deliver exceptional guest experiences, differentiate themselves from competitors, and establish a strong market presence in Madrid. The integration of CARTO as a cloud-native GIS platform further enhances NH Hotels Group' capabilities, unlocking the full potential of geospatial analytics and enabling NH Hotels Group to make data-driven decisions with confidence.

## 5. Limitations

While the geospatial analysis conducted in this report provides valuable insights for NH Hotels Group' strategic decision-making process, it is important to acknowledge and address certain limitations that may affect the interpretation and applicability of the findings. The following limitations should be considered:

### 5.1 Data Limitations
The analysis heavily relies on the availability and quality of the data used. Despite efforts to ensure data accuracy and reliability, there may be inherent limitations in the data sources utilized. Data gaps, inaccuracies, or biases could introduce uncertainties into the analysis and potentially impact the representativeness of the findings. For example, if certain data sources were not available or if there were limitations in the spatial resolution or coverage of the data, these limitations should be acknowledged. It is important to exercise caution when interpreting the results and consider the potential impact of data limitations on the conclusions drawn.

### 5.2 Assumptions and Simplifications
To facilitate the analysis, certain assumptions and simplifications were made. These include generalizations of variables or factors, which may not fully capture the complexity or heterogeneity of the real-world context. While these assumptions were necessary for the analysis, they introduce limitations in terms of the accuracy and granularity of the results. It is important to consider these simplifications when interpreting the findings and making decisions based on the analysis. Additionally, it is crucial to be aware of any potential biases that may arise from these assumptions and simplifications.

### 5.3 Spatial and Temporal Scale
The analysis is conducted at a specific spatial and temporal scale, primarily focusing on the city of Madrid. While this approach allows for a systematic and consistent analysis within the defined scope, it may not capture fine-grained variations or local nuances within the study area. The findings should be interpreted with caution, recognizing that the analysis results are based on the selected spatial and temporal scale and may not fully represent the intricacies of individual neighborhoods or specific street-level conditions. It is important to consider the potential limitations introduced by the chosen scale when applying the findings to specific locations or situations.

### 5.4 External Factors and Future Uncertainties
The analysis is conducted based on the available data and the prevailing conditions at the time of the study. However, it is essential to acknowledge that external factors beyond the scope of this analysis may influence the suitability and success of hotel sites in the future. Factors such as changes in market conditions, economic fluctuations, shifts in tourist preferences, or regulatory changes could impact the demand for hotels and the viability of specific locations. NH Hotels Group should be mindful of these external factors and regularly reassess the analysis results in light of changing circumstances. Future uncertainties should be considered when making long-term decisions based on the analysis.

### 5.5 Model Limitations and Generalization
 Models are simplifications of reality and are based on assumptions that may not perfectly capture the complexity of the real-world context. There may be potential sources of error or uncertainties associated with model outputs. It is crucial to understand that the models provide estimates and predictions based on available data and should be further validated and refined as more data becomes available.

### 5.6 Human Judgment and Expertise

While the analysis incorporates advanced analytical techniques, it is important to acknowledge that human judgment and expertise play a significant role in decision-making. The analysis should be considered as a complementary tool to inform decision-making, alongside expert insights and qualitative considerations. The final selection of hotel sites should take into account additional factors that may not be captured in the analysis, such as specific market conditions, strategic goals, and stakeholder preferences.

### 5.7 Conclusions
These limitations highlight the need for a cautious and comprehensive approach to decision-making. NH Hotels Group should consider the findings of this analysis as a starting point, complemented by additional research, expert knowledge, and stakeholder input. By acknowledging these limitations and actively seeking to address them, NH Hotels Group can make more informed and robust decisions in their strategic expansion and site selection processes.

While the limitations identified may introduce uncertainties or constraints, they should not undermine the value of the geospatial analysis conducted in this report. By understanding and addressing these limitations, NH Hotels Group demonstrates a commitment to transparency, rigor, and ongoing improvement in their decision-making processes. The analysis provides a solid foundation for NH Hotels Group to make informed choices, maximize their market presence, and drive long-term success in the highly competitive hotel industry in Madrid and beyond.


## 6. Conclusion and Recommendations

The comprehensive geospatial analysis conducted in this report has provided NH Hotels Group with valuable insights into the optimal site selection, market positioning and  sustainability practices for their growth and long-term success in Madrid's competitive hotel industry. Based on the key findings of the analysis, the following actionable recommendations are provided to guide NH Hotels Group' strategic decision-making:

### 6.1 Strategic Site Selection

1. **Leverage Commercial Hotspots**: Focus on developing new hotels in the identified commercial hotspots, where a high concentration of favorable attributes, including visitor demographics, points of interest density, and accessibility, create an environment conducive to hotel success. By strategically positioning new hotels within these hotspots, NH Hotels Group can maximize their market share and profitability.

2. **Consider Accessibility**: Emphasize accessibility to key attractions when selecting new hotel sites. Prioritize locations that offer convenient access to diverse attractions within a short walking distance, as identified through the isochrone intersection analysis. This approach will enhance guest satisfaction and improve the overall guest experience.

3. **Avoid Cannibalization**: Mitigate the risk of cannibalization by maintaining an appropriate distance between NH Hotels Group. Consider the insights from the LOF (Local Outlier Factor) and KNN (K-nearest neighbors) analyses to identify areas of high hotel density and potential competition. By strategically selecting new hotel sites that minimize competition with existing establishments, NH Hotels Group can ensure a balanced distribution of accommodations across the city and optimize their market presence.

### 6.2 Market Positioning and Differentiation

1. **Tailor Offerings to Customer Preferences**: Leverage the insights from the Tourist Perception Survey and the weighted factors derived from the composite score analysis to align hotel offerings with customer preferences. Focus on the categories of Patrimony, Arts, Gastronomy, and Leisure, as these directly influence location desirability for potential guests. By curating experiences and amenities that reflect these preferences, NH Hotels Group can enhance customer satisfaction and differentiate themselves in the market.

2. **Embrace Sustainability Practices**: Incorporate sustainable practices and environmental considerations into hotel operations and design. By demonstrating a commitment to sustainability, NH Hotels Group can attract conscious travelers, improve their brand reputation, and contribute to the long-term environmental sustainability of Madrid.

### 6.3 Technology Integration and Digital Transformation

1. **Leverage CARTO's Geospatial Analytics Platform**: Continue leveraging CARTO's cloud-native GIS platform to enhance geospatial analysis capabilities. Maximize the potential of geospatial analytics by scaling operations, handling large volumes of geospatial data, and performing complex analyses. CARTO's solutions, visualization tools, and access to enriched datasets through the Data Observatory can further support NH Hotels Group in uncovering deeper insights and making data-driven decisions.

2. **Adapt to Changing Market Dynamics**: Regularly reassess the analysis results and adapt strategies based on changing market dynamics and external factors. Monitor market trends, shifts in tourist preferences, and regulatory changes that may impact the demand for hotels and the viability of specific locations. By staying agile and responsive to market changes, NH Hotels Group can maintain their competitive advantage and ensure long-term success.


### 6.4 Rationale and Benefits
NH Hotels Group can expect the following benefits from implementing the recommendations:
- Strategic site selection ensures NH Hotels Group can capitalize on commercial hotspots, leading to increased market share and profitability.
- Emphasizing accessibility and guest satisfaction enhances the overall guest experience and improves NH Hotels Group' reputation.
- Minimizing cannibalization through careful distance management ensures a balanced distribution of accommodations, optimizing market presence.
- Tailoring offerings to customer preferences and embracing sustainability practices differentiates NH Hotels Group and attracts conscious travelers.
- Leveraging CARTO's platform enhances geospatial analysis capabilities, allowing NH Hotels Group to make data-driven decisions effectively.
- Adapting to changing market dynamics ensures NH Hotels Group remain competitive and responsive to evolving customer demands and trends.

In conclusion, the geospatial analysis conducted in this report has provided NH Hotels Group with a solid foundation for strategic decision-making in site selection, market positioning and sustainability practices. By following the actionable recommendations outlined above, NH Hotels Group can optimize their growth, deliver exceptional guest experiences, differentiate themselves from competitors, and establish a strong market presence in Madrid's highly competitive hotel industry. By continuously refining and improving their strategies based on insights gained through geospatial analysis, NH Hotels Group can secure long-term success and profitability.



## Summary

### Harnessing the Power of Geospatial Analytics for Strategic Hotel Site Selection in Madrid

### 1. Introduction and context
NH Hotel Group, a renowned hotel chain based in Madrid, seeks to open a new hotel catering to the growing demand for cultural tourism. The target demographic is the mid-high income population aged 40-69, attracted to the city's cultural heritage, performing arts scene, and gastronomical offerings. NH Hotels Group aims to provide luxury accommodations reflecting local culture, strategically located within walking distance of attractions. By embracing sustainability and selecting eco-friendly locations near tourist points of interest, NH Hotels Group ensures an exceptional guest experience while minimizing environmental impact.

### 2. Tangible Insights: Results and Visualizations
#### 2.1 Accessibility Analysis:
- Isochrone intersection analysis identified areas with convenient access to diverse attractions within a short walking distance. These areas represent potential hotspots for hotel development.
- Proximity analysis determined appropriate distances between NH Hotels Group locations, ensuring guest convenience while avoiding cannibalization.


#### 2.2 Factors Influencing Hotel Suitability:
- Geographically weighted regression (GWR) analysis unveiled the localized impacts and spatial correlations of factors influencing hotel suitability. These factors include patrimony, arts, gastronomy, leisure, visitor demographics, coverage percentage, and distance from existing NH Hotels Group locations.
- Composite scores were calculated, providing a comprehensive assessment of potential hotel sites based on the weighted factors.
- Commercial Hotspot were identified using Getis Ord statistics revealing clusters of high-ranking locations within the commercial hotspots, highlighting their desirability and potential for success.

#### 2.3 Competitive Proximity Analysis:
- Local Outlier Factor (LOF) and K-nearest neighbors (KNN) techniques helped identify areas of high competition and potential cannibalization among existing hotels. NH Hotels Group can strategically position their new hotel by avoiding locations with excessive hotel density.

### 3. Measuring Value for the Customer's Business:
- Optimizing Location Selection for Growth: NH Hotels Group can strategically expand their presence by selecting hotel sites that align with customer preferences, offer convenient access to attractions, and minimize competition.
- Enhancing Customer Satisfaction: By curating experiences and amenities based on customer preferences and ensuring accessibility to attractions, NH Hotels Group can deliver exceptional guest experiences and improve overall customer satisfaction.
- Gaining a Competitive Advantage: The analysis enables NH Hotels Group to differentiate themselves by avoiding areas of high competition and maintaining a balanced distribution of accommodations across the city.
- Ensuring Long-term Success: NH Hotels Group can establish a strong market presence by selecting locations with long-term market potential and integrating sustainability practices.

#### Conclusions
The comprehensive geospatial analysis conducted using CARTO's platform empowers NH Hotels Group to optimize hotel site selection, enhance customer satisfaction, gain a competitive advantage, and ensure long-term success. By leveraging geospatial analytics and CARTO's platform, NH Hotels Group can make data-driven decisions that align with customer preferences, differentiate from competitors, and strategically expand their presence in Madrid's highly competitive hospitality industry.

