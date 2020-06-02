# Coronavirus (covid-19) in Sierra Leone

This repository contains datasets relating to coronavirus in Sierra Leone, as well as on demographic and other information from the 2015 Population and Household Census (PHC).

Last updated: 2 June 2020.

<br/>

## Context

The novel 2019 coronavirus (covid-19) arrived late to West Africa and Sierra Leone in particular. This dataset provides the number of reported cases on a district-by-district basis for Sierra Leone, as well as various additional statistics at the country level. In addition, I provide district-by-district demographic data and information about households' main sources of information, both from the 2015 census, as well as shapefiles for the 14 districts of Sierra Leone.

## Content

The dataset consists of four main files, which are in the `output` folder. See the column descriptions below for further details.

1. **Coronavirus confirmed cases by district** (`sl_districts_coronavirus.csv`). I found the original data by looking in the `static/js/data` folder in the source code for [covid19.mic.gov.sl](https://covid19.mic.gov.sl), last accessed 2 June 2020. The file contains the cumulative number of confirmed coronavirus cases in the 14 districts of Sierra Leone as a time series. I have used the R tidyverse to reshape the data and ensure naming is consistent with the other data files.

2. **Demographic statistics by district** (`sl_districts_demographics.csv`). Data from the 2015 Population and Housing Census (PHC), sourced from [Open Data Sierra Leone](https://opendatasl.gov.sl/dataset/population-distribution-district). The dataset covers the 14 districts of Sierra Leone, which increased to 16 in 2017. Last accessed 2 June 2020.

3. **Main Sources of Information by district** (`sl_districts_info_sources.csv`). Data from the 2015 Population and Housing Census (PHC), sourced from [Open Data Sierra Leone](https://opendatasl.gov.sl/dataset/households-main-source-information-district). The dataset presents the main sources of information, such as television or radio, for households in the 14 districts of Sierra Leone. Last accessed 2 June 2020. I note that I have made one correction to the source data (see R code with correction [here](https://todowa.github.io/coronavirus-sierra-leone/index.html)).

4. **Country-wide coronavirus statistics for Sierra Leone** (`sl_national_coronavirus.csv`). The original data also comes from [covid19.mic.gov.sl](https://covid19.mic.gov.sl), last accessed 2 June 2020. The file contains numerous statistics as time series, listed in the Column Description section below. I note that there are various potential issues in the file which I leave the user to decide how to deal with (duplicate datetimes, inconsistent statistics).

Additionally I include a set of five files with district-by-district mapping (shapefiles) and other data, unchanged from the original source, each labelled `sl_districts_mapping.*`. These files come from [Direct Relief Open Data](https://hub.arcgis.com/datasets/DirectRelief::sierre-leone-districts) on ArcGIS Hub. The data includes maternal child health attributes by district, which was the original purpose of the data.

## Column Descriptions

Coronavirus confirmed cases by district `sl_districts_coronavirus.csv`:

1. `date`: Data of reporting.
2. `district`: District of Sierra Leone (based on pre-2017 administrative boundaries)
3. `confirmed_cases`: Cumulative number of confirmed coronavirus cases; NA if no data reported
4. `decrease`: Dummy variable indicating whether the number of reported cases has been revised down. NA if no reported cases on that date; 1 if there is a decrease from the last reported cases; 0 otherwise

Demographic statistics by district `sl_districts_demographics.csv`:

1. `district`: District of Sierra Leone (based on pre-2017 administrative boundaries)
2. `d_code`: District code
3. `d_id`: District id
4. `total_pop`: Total population in district
5. `pop_share`: District's share of total country population
6. `t_male`: Total male population
7. `t_female`: Total female population
8. `s_ratio`: (*) Sex ratio at birth (number of males for every 100 females, under the age of 1)
9. `t_urban`: Total urban population
10. `t_rural`: Total rural population
11. `prop_urban`: Proportion urban
12. `t_h_pop`: Sum of `h_male` and `h_female`
13. `h_male`: (?)
14. `h_female`: (?)
15. `t_i_pop`: Sum of `i_male` and `i_female`
16. `i_male`: (?)
17. `i_female`: (?)
18. `working_pop`: Working population
19. `depend_pop`: Dependent population

I rely on the [Sierra Leone 2015 Population and Housing Census Thematic Report on Population Structure and Population Distribution Report](https://www.statistics.sl/images/StatisticsSL/Documents/Census/2015/sl_2015_phc_thematic_report_on_pop_structure_and_pop_distribution.pdf) to infer definitions for certain columns (marked with (*)) and am unable to locate a definition for others (marked (?)).

Main Sources of Information by district `sl_districts_info_sources.csv`:

1. `district`: District of Sierra Leone (pre-2017)
2. `d_code`: District code
3. `d_id`: District id
4. `total_household`: Total number of households (corrected)
5. `radio`: Number of households with radio as main source of information
6. `television`: Number of households with television as main source of information
7. `print_media`: Number of households with print media as main source of information
8. `post_mail`: Number of households with post mail as main source of information
9. `hand_mail`: Number of households with hand mail as main source of information
10. `social_media`: Number of households with social media as main source of information
11. `word_mouth`: Number of households with word of mouth as main source of information
12. `church_or_mosque`: Number of households with church or mosque as main source of information

Country-wide coronavirus statistics for Sierra Leone `sl_national_coronavirus.csv`:

1. `date`
2. `new_cases`
3. `confirmed_cases`
4. `at_isolation_centres`
5. `recovered`
6. `death`
7. `in_quarantine`
8. `out_of_quarantine`
9. `female`
10. `male`

## Note Regarding Districts

In 2017 Sierra Leone redrew its administrative boundaries, splitting two districts into two and raising the total number of districts from 14 to 16 (illustrated [here](https://opendatasl.gov.sl/gis-mapping-application-0)). The district-level coronavirus data includes information on 16 districts, whilst the demographics data and map data is only available for the 14 districts.

Although Open Data Sierra Leone explains that it has [re-analysed demographics data](https://opendatasl.gov.sl/dataset/re-analysis-2015-population-census-data-16-districts-5-regions) to accommodate the 16 districts, no data files accompany the discussion. I note that there is a PDF [report](https://www.statistics.sl/images/StatisticsSL/Documents/Census/2015/sierraleone_-2015_population_census_data_for_16_districts_5_regions.pdf) on the Statistics Sierra Leone website from which some though not all reanalysed demographics data can be scraped. I leave this for future work.

To create the data files, I merged the data on the two new districts, Karene and Falaba, back into their old districts of Bombali and Koinadugu respectively.

## Licence

Data from Open Data Sierra Leone has an open licence.

## Acknowledgements

All the data have been extracted from public sources:

* The Ministry of Information and Communication of Sierra Leone, [covid19.mic.gov.sl](https://covid19.mic.gov.sl) dashboard for all statistics relating to coronavirus.
* [Open Data Sierra Leone](https://opendatasl.gov.sl/dataset/population-distribution-district) and indirectly [Statistics Sierra Leone](https://www.statistics.sl/index.php/census/census-2015.html) for the 2015 Population and Household Census (PHC) data.
* [Direct Relief Open Data](https://hub.arcgis.com/datasets/DirectRelief::sierre-leone-districts) on ArcGIS Hub for the shapefiles.

## Further Information

See [here](https://todowa.github.io/coronavirus-sierra-leone/index.html) for a full description of how the data files have been created from the source data, including the R code used to do so.