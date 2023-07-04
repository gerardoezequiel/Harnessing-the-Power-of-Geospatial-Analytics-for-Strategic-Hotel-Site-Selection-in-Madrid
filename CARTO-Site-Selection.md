# Harnessing the Power of Geospatial Analytics for Strategic Hotel Site Selection in Madrid
Prepared By: [Gerardo Ezequiel Martín Carreño]
Date: [04/07/07]

## 1. Introduction and Problem Context


NH Hotels, a well-established hotel chain with a significant footprint in Madrid, is seeking for expansion. With 15 existing locations spread across the city, they have a strong understanding of the local market and a proven track record of delivering high-quality hospitality experiences. However, expansion in a city as dynamic and competitive as Madrid requires careful planning and strategic decision-making.

The target demographic for their new hotel is the mid-high income population aged 40-69. This group represents a significant portion of Madrid's visitors, drawn to the city for its rich cultural heritage, vibrant performing arts scene, and diverse gastronomical offerings. These insights are supported by the Madrid Tourism Report (Tourist Perception Survey 2019), which indicates that 97.64% of visitors associate the city's service offerings with a mid-high purchasing power. The report also highlights the main reasons for visiting Madrid, including its cultural heritage, performing arts, and gastronomy.

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

**Demographic and Building Data**:To further enrich our analysis, we incorporated demographic data and building data from the CARTO Data Observatory. The demographic data, including age and income information, helped us understand the socio-economic landscape of different areas in Madrid. The building data, sourced from the [CARTO demo tables](https://clausa.app.carto.com/data/explorer/carto_dw/carto-demo-data/demo_tables/inspire_buildings_madrid), provided insights into the physical landscape of the city, which could influence the feasibility of establishing a new hotel in certain locations.

#### 2.1.2 Preprocessing
Both the pedestrian and accommodations data were processed in a [Colab Python notebook](https://colab.research.google.com/drive/1YSLiIRLenV-iwKi4YFTwBYeW-v8SAJUx?usp=sharing). The pedestrian data was cleaned, standardized, timestamps were created, missing values were handled, and geospatial points were generated. For the accommodations data, relevant information was extracted, incomplete entries were removed, star ratings were converted to numerical format, and hotel brands were classified using internet research for competitor analysis. The remaining datasets, including pedestrian data, building data, and OpenStreetMap Nodes for points of interest, were processed using Google's BigQuery. This powerful tool allowed us to handle large volumes of data efficiently, performing operations such as filtering, aggregation, and spatial joins. The processed data was then integrated into our analysis, providing a more comprehensive view of Madrid's tourism landscape.

<iframe width="640px" height="360px" src="https://clausa.app.carto.com/map/51125179-58c9-47fa-9f23-022d86f0c120"></iframe>



### 2.2. Accessibility Analysis

To understand the accessibility of key attractions in Madrid, we conducted an isochrone intersection analysis. This involved generating isolines for every point of interest (POI) in the categories of "Patrimony, Monuments and Museums", "Theaters and Arts", "Gastronomy", and "Leisure". Each isoline represented a 15-minute walking distance from the respective POI, providing a spatial representation of what a tourist could access within a quarter of an hour's walk.

We then performed spatial aggregations and intersections of these isolines to identify zones of overlap. These overlapping zones represent areas where a tourist can conveniently access a variety of attractions within a 15-minute walk, making them highly desirable locations for a hotel. This accessibility analysis played a crucial role in highlighting the areas that offer the most convenience for tourists, particularly those interested in Madrid's cultural heritage, performing arts scene, gastronomy, and leisure activities.

In addition to the isochrone intersection analysis, we also considered the proximity of potential hotel locations to existing NH Hotels. This was an important factor to avoid cannibalization, where a new hotel might draw customers away from existing NH Hotels in the vicinity.

To incorporate this factor, we calculated the distance from each hexagon in our spatial grid to each existing NH Hotel. We then kept the minimum distance for each hexagon, representing the closest existing NH Hotel.

This proximity data, along with the coverage of 15-minute walk isochrones from tourist points of interest, were used to enrich our analysis. These factors helped us identify locations that not only offer high accessibility to key attractions but also maintain a healthy distance from existing NH Hotels, ensuring a balanced distribution of accommodations across the city.
<iframe width="640px" height="360px" src="https://clausa.app.carto.com/map/d973dc67-828d-414c-bc74-3cc839221e98"></iframe>

### 2.3 Spatial Index Enrichment

To enhance the granularity and precision of our analysis, we incorporated the H3 spatial indexing system using the CARTO Analytics Toolbox. Spatial indexes, like H3, are global discrete grids that cover the entire globe. They are designed to efficiently process and query spatial data, making spatial analysis faster and more accurate.
    
For our analysis, we used an H3 resolution of 10. This resolution level was chosen because it provides a good balance between spatial precision and computational efficiency, particularly for a city center like Madrid. At this resolution, each hexagon covers an area of approximately 0.015 square kilometers, which is suitable for capturing the spatial variations in pedestrian traffic by age and income and number of visitors, points of interest density, and the minimun distance between NH hotels.

By using the H3 spatial indexing system, we were able to create an enriched grid that integrated various variables, including demographic data, hotel locations, and points of interest density. This enriched grid map provides a more detailed and accurate view of potential hotel locations, allowing us to identify optimal locations with greater precision. This approach ensures that our analysis is grounded in a robust understanding of the spatial dynamics of Madrid's city center.

<iframe width="640px" height="360px" src="https://clausa.app.carto.com/map/d5e61e72-4097-4d5e-ab25-b25c48e271e8"></iframe>





### 2.4 Spatial Correlation, Hotspot Detection Analysis

In our analysis to identify ideal hotel sites in Madrid, we employed spatial correlation and hotspot detection techniques. To determine the importance of each variable, we assigned weights based on their relevance to identifying ideal hotel sites. Factors such as visitor demographics, covered percentage, distance from existing NH Hotels, count of patrimony monuments and museums, count of gastronomy establishments, count of leisure facilities, and count of theater and arts venues were considered.


To achieve this, we utilized the following procedures 

#### Geographically Weighted Regression (GWR):
Geographically Weighted Regression (GWR) was performed to understand the spatial correlations between the target variable, our target audience, and the correlation variables including the count of POI per category, the percentage of area covered by them. GWR allows us to account for spatial heterogeneity and better understand how different variables influence the suitability of hotel locations in Madrid. By applying weights to neighboring cells using the Gaussian kernel function, GWR captures the localized impacts of these variables and helps us uncover spatial patterns.

```
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

To represent the relative importance of these chosen categories within the total weight, we performed normalization. Each percentage was divided by the sum of the percentages of the considered categories (Patrimony, Arts, Gastronomy, and Leisure), and then multiplied by the remaining weight after assigning a 20% to each of the following factors: visitors_midhigh_40_69_sum, covered_percentage, and hilton_dist.

This normalization process resulted in the following weights for the chosen categories:

- `patrimony_monuments_museums_count`: 15.644%
- `gastronomy_count`: 8.364%
- `leisure_count`: 6.364%
- `theatre_arts_count`: 9.64%

These weights, along with the weights for other factors, sum up to 100%, ensuring that they accurately represent the relative proportions of each category within the total weight. By incorporating these weights into our analysis, we can better understand the significance of each category and its influence on the suitability of potential hotel locations in Madrid.
```
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
```
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
<iframe width="640px" height="360px" src="https://clausa.app.carto.com/map/a6b9411a-7273-4ab4-ae63-037c91c95b94"></iframe>
  
### 2.5 Competitive Proximity and Dispersion Analysis using Local Outlier Factor and KNN 

The Competitive Proximity and Dispersion Analysis, utilizing the Local Outlier Factor (LOF) and K-nearest neighbors (KNN) methodologies, provides NH Hotels with valuable insights into the spatial distribution and proximity of hotels in Madrid. This analysis reveals areas of high competition and potential cannibalization, helping NH Hotels select the best location from their identified commercial hotspots.

#### Local Outlier Factor (LOF)
 LOF is a powerful algorithm that detects outliers and anomalies within a dataset. In the context of this analysis, LOF is applied to the distribution of hotels in Madrid. It helps identify areas where the density of hotels significantly deviates from the expected pattern. By highlighting these outliers, NH Hotels gains insights into areas of high competition and potential market saturation. This information enables NH Hotels to make strategic decisions and avoid locations with excessive hotel density, ensuring a balanced distribution of accommodations across the city.

#### K-nearest neighbors (KNN)
 KNN is a machine learning algorithm that measures the proximity between data points. In the Competitive Proximity and Dispersion Analysis, KNN is employed to assess the spatial relationship between hotels in Madrid. By analyzing the distances between hotels, NH Hotels can identify clusters and patterns of hotel distribution. This information helps in understanding the proximity of existing hotels to potential new locations. NH Hotels can strategically position their new hotel to avoid cannibalization with existing hotels and ensure a healthy competitive landscape.

By applying LOF and KNN methodologies, NH Hotels gains valuable insights into the competitive landscape of Madrid's hotel industry. The analysis reveals areas with a high concentration of hotels, indicating intense competition and potential cannibalization. This information allows NH Hotels to make informed decisions about the best location from their commercial hotspots. NH Hotels can select a location that not only offers accessibility to key attractions and amenities but also ensures a healthy distance from existing hotels, avoiding excessive competition and optimizing their market presence.

The Competitive Proximity and Dispersion Analysis, supported by LOF and KNN techniques, plays a vital role in NH Hotels' expansion strategy. It helps them identify areas of opportunity, understand the competitive dynamics, and select the optimal location for their new hotel. By leveraging these insights, NH Hotels can position themselves strategically in the market, minimize cannibalization, and maximize their potential for success and profitability in the competitive hotel industry of Madrid.
<iframe width="640px" height="360px" src="https://clausa.app.carto.com/map/dad1bcc9-c728-48ff-8661-ee3ae27049f2"></iframe>



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

