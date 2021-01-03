# Gentrification and demographic analysis of Halifax census data (2006-2016)
This repository contains data and analytic code that examines changes in demographics of the Halifax metro area, based on census tract data from 2006-2016. 

## Background
Since the 1980s, areas of Dartmouth, Spryfield, and Clayton Park have been [transitioning from middle income to low income areas](https://nsadvocate.org/2019/09/23/gentrification-and-income-inequality-the-halifax-way-an-interview-with-professor-howard-ramos/), while neighbourhoods on the peninsula, such as the North and South Ends, have been experiencing increases in the average income of residents. Low-income residents are being forced from their neighbourhoods to make way for high-end luxury properties being built for more wealthy occupants. Businesses in these areas have also been transformed from those who primarily serve the local community, to [places where residents don't feel welcome](https://www.cbc.ca/radio/thecurrent/the-current-for-february-21-2018-1.4543540/call-it-what-it-is-white-ignorance-gentrification-frays-the-social-fabric-in-halifax-s-north-end-1.4543545).

Although this project identifies gentrified areas and demographic changes based on census data from 2006-2016, further analyses of previous and upcoming (2021) census data can provide additional evidence of displacement and dispossession in Halifax. Equity-seeking groups, specifically Black and Indigenous community members, have been disproportionately affected by gentrification and urban renewal in the city. [Rates of homelessness are currently at record highs](https://www.cbc.ca/news/canada/nova-scotia/homeless-report-2020-covid-19-affordable-housing-association-of-nova-scotia-1.5805458), as affordable housing continues to disappear.

I recommend reviewing the following resources to learn more about gentrification in Halifax:
1. [Gentrifying Blackness in Halifax's inner city](https://www.thecoast.ca/halifax/gentrifying-blackness-in-halifaxs-inner-city/Content?oid=13953475)
2. [Halifax residents say gentrification is forcing them from their homes](https://atlantic.ctvnews.ca/halifax-residents-say-gentrification-is-forcing-them-from-their-homes-1.2532111)
3. ['Call it what it is — white ignorance': Gentrification frays the social fabric in Halifax's North End](https://www.cbc.ca/radio/thecurrent/the-current-for-february-21-2018-1.4543540/call-it-what-it-is-white-ignorance-gentrification-frays-the-social-fabric-in-halifax-s-north-end-1.4543545)
4. [Racism and gentrification in Halifax's North End](http://halifax.mediacoop.ca/blog/evancoole/33436)
5. [Africville 2.0: In Halifax’s North End, Black residents fear development will take another home away](https://www.theglobeandmail.com/canada/article-africville-20-in-halifaxs-north-end-black-residents-fear-development/)

## Data
The data used in this project was pulled from the [2006, 2011, and 2016 National Household Survey (NHS) census profiles](https://www12.statcan.gc.ca/census-recensement/index-eng.cfm?MM=1). The data from selected census tracts were collected and stored in `data/2006-census-data.csv`, `data/2011-census-data.csv`, and `data/2016-census-data.csv` with the following variables:

1. `tid`: Census Tract ID
2. `population`: tract population
3. `white`: population that did not identify as a visible minority
4. `indigenous`: population that identified with an Aboriginal group
5. `black`: population that identified as Black
6. `asian`: population that identified with an Asian group
7. `minority`: population that identified with another visible minority group
8. `adult`: population over 15
9. `income`: median total income among recipients
10. `home`: average value of dwellings ($)
11. `rent`: median monthly shelter costs for rented dwellings ($)
12. `education`: population holding a university certificate, diploma, or degree at bachelor level or above
13. `p_white`: percentage of white people in tract
14. `p_indig`: percentage of Indigenous people in tract
15. `p_black`: percentage of Black people in tract
16. `p_asian`: percentage of Asian people in tract
17. `p_mnrty`: percentage of those identifying with another visible minority group in tract
18. `p_poc`: overall percentage of people of colour in tract
19. `p_educ`: percentage of educational attainment

## Gentrification status methodology and analysis

Tracts are determined to have gentrified over a time period if they meet the following criteria:

1. An increase in a tract's educational attainment, as measured by the percentage of residents age 25 and over holding bachelor’s degrees, is in the top third percentile of all tracts within a metro area.
2. A tract’s home value increases when adjusted for inflation.
3. The percentage increase in a tract’s inflation-adjusted home value is in the top third percentile of all tracts within a metro area.

This measure of gentrification is based on the methodology found at [this link](https://www.governing.com/gov-data/gentrification-report-methodology.html). Halifax metro area calculations necessary for this test are:

1. `educ_eligible`: true if the tract is in the top third percentile of increases in educational attainment from 2006 to 2016.
2. `home_value_increase`: true if a tract's home value increases from 2006 to 2016 when adjusted for inflation.
3. `home_eligible`: true if a tract's percentage of home value increase is in the top third percentile of increases in home value from 2006 to 2016.

If all variables are true for a given tract, it is considered `gentrified`.

Data analysis was performed in the Jupyter notebook `notebooks/analysis.ipynb`. A list of tracts considered gentrified, maps of demographic changes, and calculations of demographic percentage changes were produced within the notebook.

## Licensing 

All code in this repository is available under the [MIT License](https://opensource.org/licenses/MIT). Datasets and shapefiles are available under the [respective terms outlined by Statistics Canada](https://www.statcan.gc.ca/eng/reference/licence).
