<style>
/* CSS styles for animation */
.code-block {
  overflow: auto; /* Hide overflow to clip the height */
  max-height: 300px; /* Initial max-height value */
  max-width: 1200px; /* Initial max-height value */
  transition: max-height 0.5s ease-out; /* Apply transition effect */
}

.code-block:hover {
  max-height: 800px; /* Increase max-height on hover */
}
</style>
# Harnessing the Power of Geospatial Analytics for Strategic Hotel Site Selection in Madrid
Prepared By: Gerardo Ezequiel Martín Carreño
Date: 03/07/2023

## 1. Introduction and Problem Context


NH Hotels, a well-established hotel chain with a significant footprint in Madrid, is seeking for expansion. With 15 existing locations spread across the city, they have a strong understanding of the local market and a proven track record of delivering high-quality hospitality experiences. However, expansion in a city as dynamic and competitive as Madrid requires careful planning and strategic decision-making.

The target demographic for their new hotel is the mid-high income population aged 40-69. This group represents a significant portion of Madrid's visitors, drawn to the city for its rich cultural heritage, vibrant performing arts scene, and diverse gastronomical offerings. These insights are supported by the Madrid Tourism Report (Tourist Perception Survey 2019), which indicates that 97.64% of visitors associate the city's service offerings with a mid-high purchasing power. The report also highlights the main reasons for visiting Madrid, including its cultural heritage, performing arts, and gastronomy.
![](https://i.ibb.co/dmc2g0g/Carto-tourism-graphic.png)

However, catering to this demographic is not without its challenges. The mid-high income population often has discerning tastes and high expectations for their travel experiences. They seek accommodations that offer a blend of luxury, convenience, and unique experiences that reflect the local culture.

Moreover, the location of the hotel plays a crucial role in its success. It needs to be situated in an area that is accessible but also close to the city's main attractions. The ideal location would be in a vibrant area with a variety of dining and entertainment options.

Our goal in this project is to leverage the power of geospatial data and sophisticated analysis techniques using the CARTO platform  to identify optimal locations for a new NH Hotel. We aim to find locations that not only have high potential for profitability but also align with the preferences and needs of the target demographic. By doing so, we hope to provide NH Hotels with actionable insights that can guide their expansion strategy and contribute to the success of their new hotel.

## 2. Methodology

### 2.1 Data Acquisition & Preprocessing
#### 2.1.1 Datasets
The foundation of our analysis is a robust collection of datasets that provide a comprehensive view of Madrid's tourism landscape. We focused on acquiring data that could offer insights into pedestrian traffic patterns, existing tourist accommodations, and points of interest - three key factors that significantly influence the success of a hotel location.

**Pedestrian Traffic Data**: We utilized two pedestrian datasets to understand the flow of foot traffic across the city. The first dataset, accessible through the [Madrid Open Data Portal - Pedestrian and bicycle capacity](https://datos.madrid.es/portal/site/egob/menuitem.c05c1f754a33a9fbe4b2e4b284f1a5a0/?vgnextoid=695cd64d6f9b9610VgnVCM1000001d4a900aRCRD&vgnextchannel=374512b9ace9f310VgnVCM100000171f5a0aRCRD&vgnextfmt=default), provides granular data on pedestrian traffic on selected streets in Madrid from 2019 to June 2021. This dataset offers a historical perspective, allowing us to identify long-term trends and patterns in pedestrian movement. The second dataset, sourced from the [CARTO demo tables](https://clausa.app.carto.com/data/explorer/carto_dw/carto-demo-data/demo_tables/madrid_est_pedestrian_traffic), offers more recent data but is limited to the center of Madrid. Despite its spatial and temporal limitations, this dataset is invaluable for its insights into the most recent pedestrian traffic trends in one of Madrid's most tourist-heavy areas.

The pedestrian data was processed using a [Python notebook](https://colab.research.google.com/drive/1YSLiIRLenV-iwKi4YFTwBYeW-v8SAJUx?usp=sharing), where we cleaned and standardized the data, converted date and time information into a timestamp format, handled missing values, and converted latitude and longitude data into geometric points for geospatial analysis.

**Existing Tourist Accommodations**: To understand the current landscape of tourist accommodations in Madrid, we incorporated data from the [Madrid Open Data Portal - Accommodation in the city of Madrid](https://datos.madrid.es/portal/site/egob/menuitem.c05c1f754a33a9fbe4b2e4b284f1a5a0/?vgnextoid=df42a73970504510VgnVCM2000001f4a900aRCRD&vgnextchannel=374512b9ace9f310VgnVCM100000171f5a0aRCRD&vgnextfmt=default). This dataset provides comprehensive information about existing accommodations, including hotels, hostels, pensions, and campsites. It offers insights into the distribution of accommodations across the city, their types, and their proximity to key points of interest.

**Points of Interest**: Points of interest data, sourced from the [OpenStreetMap Nodes via the CARTO Data Observatory](https://clausa.app.carto.com/data/observatory/openstreetmap/subscriptions/osm_nodes_205a5f56), provides information about key attractions in Madrid. This includes cultural heritage sites, performing arts venues, gastronomical hotspots, and other attractions that draw tourists to the city. The proximity of a hotel to these points of interest can significantly influence its attractiveness to potential guests.

**Demographic and Building Data**: To further enrich our analysis, we incorporated demographic data and building data from the CARTO Data Observatory. The demographic data, including age and income information, helped us understand the socio-economic landscape of different areas in Madrid. The building data, sourced from the [CARTO demo tables](https://clausa.app.carto.com/data/explorer/carto_dw/carto-demo-data/demo_tables/inspire_buildings_madrid), provided insights into the physical landscape of the city, which could influence the feasibility of establishing a new hotel in certain locations.

#### 2.1.2 Preprocessing
Both the pedestrian and accommodations data were processed in a [Colab Python notebook](https://colab.research.google.com/drive/1YSLiIRLenV-iwKi4YFTwBYeW-v8SAJUx?usp=sharing). The pedestrian data was cleaned, standardized, timestamps were created, missing values were handled, and geospatial points were generated. For the accommodations data, relevant information was extracted, incomplete entries were removed, star ratings were converted to numerical format, and hotel brands were classified using internet research for competitor analysis. The remaining datasets, including pedestrian data, building data, and OpenStreetMap Nodes for points of interest, were processed using Google's BigQuery. This powerful tool allowed us to handle large volumes of data efficiently, performing operations such as filtering, aggregation, and spatial joins. The processed data was then integrated into our analysis, providing a more comprehensive view of Madrid's tourism landscape.

In addition to utilising BigQuery, we incorporated workflows, a newly introduced tool within the Carto Platform, to preprocess our base data specifically for the study area. These workflows proved instrumental in managing the intricacies of data processing tasks associated with the study area. By effectively utilising workflows, we streamlined the data preparation process, ensuring that the data was in an optimal state for further analysis.

  <img src="https://i.ibb.co/GQ5JTKZ/Screenshot-2023-07-05-at-05-49-09-2x.png" alt="Workflow study">
<figcaption><small><strong>Workflow 1.</strong> Creation of study area and spatial indexes and area and centroid calculation operations.</small></figcaption>

The workflows played a crucial role in managing the various data processing tasks related to our study area. By leveraging the capabilities of these workflows, we were able to streamline the preprocessing of our base data, particularly for the map creation. This included handling data extraction, transformation, and loading operations in a systematic and organised manner.

By incorporating workflows into our data processing pipeline, we achieved enhanced efficiency and reproducibility. The workflows provided a structured framework for executing tasks, enabling us to maintain consistency and accuracy throughout the process. This systematic approach not only saved time but also ensured that our data was processed consistently and reliably.

Given the constraints of data availability, our study area was carefully selected to maximise the insights derived from the available pedestrian traffic data. This data, despite its high level of granularity, was restricted to the central area of Madrid, specifically within the boundaries of the m-30 motorway network. Consequently, we focused our analysis within this defined study area, which spans an approximate area of 37.72 km2 and 2439 h3 cells resolution 10. This deliberate choice allowed us to concentrate our efforts on a specific and meaningful subset of Madrid's tourism landscape, enabling us to gain a deeper understanding of the dynamics within this region.

To extract relevant points of interest (POIs) from OpenStreetMap (OSM) for visualization and analysis, we used a SQL query. The query selected POIs based on specific tags, such as museums, attractions, theatres, restaurants, cafes, parks, and gardens. The retrieved data included the name and geographical coordinates (latitude and longitude) of each POI. This information was categorized into different groups, such as patrimony/monuments/museums, theatre/arts, gastronomy, and leisure.

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



The processed data was then utilized to create visualizations and maps that provide a better understanding of the variables and exploratory analysis. For example, the pedestrian heatmap shows the highest concentration of pedestrians from our target audience (people between 40 and 69 years old with mid-high income) in the districts of Salamanca and Chamberí. By zooming in on the map, we can observe time series analysis of pedestrian traffic in selected streets, particularly in the low emission zone of Madrid. This analysis covers the period from January 2019 to June 2021, and the data can be filtered through SQL parameters or widgets. The dynamic visualization showcases how pedestrian counts evolve weekly. Additionally, the map displays the distribution of hotels in the study area, allowing users to filter and access additional information for each hotel through a side panel.
<iframe width="1280px" height="720px" src="https://clausa.app.carto.com/map/51125179-58c9-47fa-9f23-022d86f0c120"></iframe>

The points of interest are categorized into "patrimony, museum and monuments," "theatre and arts," "gastronomy," and "leisure." The map highlights the high number of restaurants and cafés with green and yellow dots.

This initial map serves as a foundation for understanding the data, conducting exploratory analysis, and gaining insights into the variables and their relationships. It provides NH Hotels with valuable information to inform their decision-making process and strategy for hotel site selection in Madrid.

### 2.2. Accessibility Analysis

To gain insights into the accessibility of key attractions in Madrid, we leveraged our workflows to conduct an isochrone intersection analysis. This involved a series of steps executed within Workflow 2, enabling us to understand the spatial relationships and convenience of various points of interest (POI) categories.

Within Workflow 2, we initiated the creation of isochrones representing 15-minute walking distances from each POI within the categories of "Patrimony, Monuments and Museums," "Theaters and Arts," "Gastronomy," and "Leisure." These isochrones served as spatial boundaries, illustrating what a tourist could conveniently access within a quarter of an hour's walk from each respective POI. 

<img src="https://i.ibb.co/yXKSX1C/Screenshot-2023-07-05-at-06-20-35-2x.png" alt="Workflow study">
<figcaption><small><strong>Workflow 2.</strong> Creation of 15-minute walking isochrones for the different POI categories and their intersection and aggregation.</small></figcaption>

After generating the isochrones, we performed spatial aggregations and intersections to identify zones of overlap. These overlapping zones indicated areas where a tourist could conveniently access a diverse range of attractions within a 15-minute walking distance. These areas emerged as highly desirable locations for hotels, offering optimal convenience to tourists.

The accessibility analysis carried out through Workflow 2 played a critical role in identifying areas that provided the utmost convenience for tourists interested in Madrid's cultural heritage, performing arts scene, gastronomy, and leisure activities. By understanding the intersecting zones, we could pinpoint the regions that offered the most accessible and vibrant experience for tourists, aiding in strategic decision-making for the placement of accommodations and highlighting key areas of interest within the city.

In addition to the isochrone intersection analysis, we took into account the proximity of potential hotel locations to existing NH Hotels. This consideration aimed to avoid cannibalization, which occurs when a new hotel draws customers away from nearby NH Hotels.

To assess this proximity, we performed an analysis using a SQL query. We defined a buffer area to encompass the study area in Madrid, and then selected NH Hotels within that buffer zone. Specifically, we focused on NH Hotels and located within the buffer area.

Next, we created a grid of hexagons to represent different potential hotel locations. For each hexagon in the grid, we calculated the minimum distance to the closest NH Hotel. This distance metric helped us understand the proximity of each potential hotel location to existing NH Hotels.
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


This proximity data, along with the coverage of 15-minute walk isochrones from tourist points of interest, were used to enrich our analysis. These factors helped us identify locations that not only offer high accessibility to key attractions but also maintain a healthy distance from existing NH Hotels, ensuring a balanced distribution of accommodations across the city.
<iframe width="1280px" height="720px" src="https://clausa.app.carto.com/map/d973dc67-828d-414c-bc74-3cc839221e98"></iframe>

In this map, we have visualized the results of the 15-minute isochrones based on different categories of points of interest (POI), including "patrimony, museum and monuments," "theatre and arts," "gastronomy," and "leisure." The aggregated isochrones are represented in the background, providing an overview of the areas that can be reached within a 15-minute walk from the respective POIs.

The first isochrone, shown in blue, represents the intersection of these aggregated isochrones. It highlights the areas where multiple categories of POIs overlap, indicating locations that offer easy access to diverse attractions within a short walking distance. These areas are particularly desirable for hotel development as guests can conveniently explore a variety of cultural, artistic, culinary, and leisure experiences.

Additionally, the map displays the location of hotels that fall within this aggregated isochrone. These hotels are strategically positioned to ensure that guests can reach the POIs belonging to the different categories within a 15-minute walk. By staying at these hotels, visitors have the advantage of convenient access to a range of attractions without the need for extensive travel.

This visualization provides NH Hotels with valuable insights into the distribution of isochrones, the areas of overlap, and the location of hotels within the desired accessibility range. It allows NH Hotels to identify specific areas where the concentration of diverse POIs and hotel accommodations create a favorable environment for attracting and satisfying guests.

By leveraging this information, NH Hotels can make informed decisions regarding the selection of hotel sites that offer the best proximity to popular attractions and enhance the overall guest experience. This strategic approach ensures that NH Hotels can position their establishments in areas with high tourist appeal and optimize their market presence in Madrid.

### 2.3 Spatial Index Enrichment

To enhance the granularity and precision of our analysis, we incorporated the H3 spatial indexing system using the CARTO Analytics Toolbox. Spatial indexes, like H3, are global discrete grids that cover the entire globe. They are designed to efficiently process and query spatial data, making spatial analysis faster and more accurate.
    
For our analysis, we used an H3 resolution of 10. This resolution level was chosen because it provides a good balance between spatial precision and computational efficiency, particularly for a city center like Madrid. At this resolution, each hexagon covers an area of approximately 0.015 square kilometers, which is suitable for capturing the spatial variations in pedestrian traffic by age and income and number of visitors, points of interest density, and the minimun distance between NH hotels.

By using the H3 spatial indexing system, we were able to create an enriched grid that integrated various variables, including demographic data, hotel locations, and points of interest density. This enriched grid map provides a more detailed and accurate view of potential hotel locations, allowing us to identify optimal locations with greater precision. This approach ensures that our analysis is grounded in a robust understanding of the spatial dynamics of Madrid's city center.

<iframe width="1280px" height="720px" src="https://clausa.app.carto.com/map/d5e61e72-4097-4d5e-ab25-b25c48e271e8"></iframe>

This map provides valuable insights obtained by enriching the spatial index with our data using an H3 resolution of 10. On the left side of the map, we can observe the concentration of pedestrians belonging to our target audience. This information allows NH Hotels to identify areas with high pedestrian activity, indicating popular tourist spots and potential hotspots for hotel development. By strategically positioning their hotels in these areas, NH Hotels can attract more guests and cater to their preferences, enhancing customer satisfaction and driving business growth.

On the right side of the map, we have the visualization of the minimum distances between existing NH hotels. This information is crucial to avoid cannibalization and ensure a balanced distribution of accommodations across the city. By maintaining an appropriate distance between NH hotels, NH Hotels can optimize their market presence and prevent customers from being drawn away from existing locations. The map assists NH Hotels in identifying gaps in coverage and strategically selecting new hotel sites that maximize accessibility to key attractions while minimizing competition with their own properties. 



### 2.4 Spatial Correlation, Hotspot Detection Analysis

In our analysis to identify ideal hotel sites in Madrid, we employed spatial correlation and hotspot detection techniques. To determine the importance of each variable, we assigned weights based on their relevance to identifying ideal hotel sites. Factors such as visitor demographics, covered percentage, distance from existing NH Hotels, count of patrimony monuments and museums, count of gastronomy establishments, count of leisure facilities, and count of theater and arts venues were considered.


To achieve this, we utilized the following procedures 

#### Geographically Weighted Regression (GWR):
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

#### Composite Score Calculation :

After performing the geographically weighted regression (GWR) analysis and gaining a better understanding of the spatial relationships between variables, we proceeded to calculate composite scores. The composite scores provide a comprehensive assessment of each potential hotel site by combining and weighting the relevant factors.

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

#### Hotspot Detection:
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

The kring parameter was set to 3, indicating that cells within a radius of 3 units from the origin cell were considered in the analysis. The p-value threshold for hotspot significance was set to 0.05, meaning that only cells with a p-value below this threshold were identified as hotspots.

The Getis Ord hotspot analysis, conducted through the Commercial Hotspots tool in the analytical toolbox, helped us identify areas with clusters of high-ranking locations. This analysis allows us to pinpoint specific regions in Madrid where multiple factors align to create hotspots of desirable hotel sites. By identifying these hotspots, NH Hotels can focus their attention on areas with the highest potential for success and profitability.

By combining geographically weighted regression (GWR) for spatial correlation analysis, the creation of a composite score based on weighted factors, and hotspot detection using Getis Ord statistics, we obtained a comprehensive understanding of the ideal hotel sites in Madrid. These techniques allowed us to consider multiple factors simultaneously and identify areas with clusters of high-ranking locations, providing valuable insights for NH Hotels' decision-making process in hotel site selection.
<iframe width="1280px" height="720px" src="https://clausa.app.carto.com/map/a6b9411a-7273-4ab4-ae63-037c91c95b94"></iframe>
  
### 2.5 Competitive Proximity and Dispersion Analysis using Local Outlier Factor and KNN 

The Competitive Proximity and Dispersion Analysis, utilizing the Local Outlier Factor (LOF) and K-nearest neighbors (KNN) methodologies, provides NH Hotels with valuable insights into the spatial distribution and proximity of hotels in Madrid. This analysis reveals areas of high competition and potential cannibalization, helping NH Hotels select the best location from their identified commercial hotspots.

#### Local Outlier Factor (LOF)
 LOF is a powerful algorithm that detects outliers and anomalies within a dataset. In the context of this analysis, LOF is applied to the distribution of hotels in Madrid. It helps identify areas where the density of hotels significantly deviates from the expected pattern. By highlighting these outliers, NH Hotels gains insights into areas of high competition and potential market saturation. This information enables NH Hotels to make strategic decisions and avoid locations with excessive hotel density, ensuring a balanced distribution of accommodations across the city.

#### K-nearest neighbors (KNN)
 KNN is a machine learning algorithm that measures the proximity between data points. In the Competitive Proximity and Dispersion Analysis, KNN is employed to assess the spatial relationship between hotels in Madrid. By analyzing the distances between hotels, NH Hotels can identify clusters and patterns of hotel distribution. This information helps in understanding the proximity of existing hotels to potential new locations. NH Hotels can strategically position their new hotel to avoid cannibalization with existing hotels and ensure a healthy competitive landscape.

By applying LOF and KNN methodologies, NH Hotels gains valuable insights into the competitive landscape of Madrid's hotel industry. The analysis reveals areas with a high concentration of hotels, indicating intense competition and potential cannibalization. This information allows NH Hotels to make informed decisions about the best location from their commercial hotspots. NH Hotels can select a location that not only offers accessibility to key attractions and amenities but also ensures a healthy distance from existing hotels, avoiding excessive competition and optimizing their market presence.

The Competitive Proximity and Dispersion Analysis, supported by LOF and KNN techniques, plays a vital role in NH Hotels' expansion strategy. It helps them identify areas of opportunity, understand the competitive dynamics, and select the optimal location for their new hotel. By leveraging these insights, NH Hotels can position themselves strategically in the market, minimize cannibalization, and maximize their potential for success and profitability in the competitive hotel industry of Madrid.
<iframe width="1280px" height="720px" src="https://clausa.app.carto.com/map/dad1bcc9-c728-48ff-8661-ee3ae27049f2"></iframe>



## 3. Value of the Analysis for NH Hotels

NH Hotels stands to gain significant value from the comprehensive analysis conducted using geospatial data and advanced analytical techniques. The insights obtained from the analysis directly contribute to NH Hotels' growth, customer satisfaction, and profitability. By aligning the value proposition with NH Hotels' specific goals and challenges, the analysis becomes even more relevant and impactful.

### Optimizing Location Selection for Growth

One of NH Hotels' key goals is to strategically expand its presence in Madrid. The analysis provides NH Hotels with a strategic advantage by identifying optimal locations for new hotel development. By considering factors such as pedestrian traffic patterns, proximity to popular points of interest, and minimizing cannibalization with existing NH Hotels, the analysis guides NH Hotels in selecting locations with the highest potential for success. This strategic approach ensures that NH Hotels can capture a significant share of the mid-high income population visiting Madrid while avoiding areas of high competition. By expanding in well-positioned locations, NH Hotels can drive growth and maximize their market presence.

### Enhancing Customer Satisfaction

NH Hotels prioritizes customer satisfaction and aims to provide a superior guest experience. The analysis plays a pivotal role in this aspect by enabling NH Hotels to understand the preferences and needs of their target demographic. By selecting locations that offer a blend of luxury, convenience, and unique experiences, NH Hotels can ensure that their guests have access to popular attractions, cultural landmarks, and amenities that align with their interests. This tailored approach enhances customer satisfaction, fosters positive reviews and recommendations, and cultivates long-term loyalty. The analysis empowers NH Hotels to deliver exceptional guest experiences that keep customers coming back.

### Gaining a Competitive Advantage

In a competitive hotel market like Madrid, NH Hotels strives to differentiate itself from competitors. The analysis provides NH Hotels with a competitive advantage by revealing areas of high hotel density and potential cannibalization. By avoiding locations with excessive competition and strategically positioning their new hotels in commercial hotspots, NH Hotels can ensure a balanced distribution of accommodations across the city. This approach not only maximizes NH Hotels' market share but also avoids dilution of their brand and resources. By leveraging the insights from the analysis, NH Hotels gains a competitive edge, allowing them to stand out and thrive in the highly competitive hospitality industry.

### Ensuring Long-term Success

NH Hotels aims for sustainable growth and long-term success in Madrid. The analysis contributes to this goal by enabling NH Hotels to establish a strong presence and reputation in the market. By selecting optimal locations that cater to the target demographic, offer convenience, and reflect the local culture, NH Hotels can build a loyal customer base and foster brand loyalty. The strategic placement of hotels based on the analysis insights enhances NH Hotels' reputation as a trusted and preferred choice for visitors to Madrid. This long-term success translates into increased market share, revenue, and profitability.

In summary, the analysis provides NH Hotels with significant value in optimizing location selection, enhancing customer satisfaction, gaining a competitive advantage, and ensuring long-term success. By leveraging the insights and recommendations from the analysis, NH Hotels can drive growth, deliver exceptional guest experiences, differentiate from competitors, and establish a strong market presence in Madrid.

