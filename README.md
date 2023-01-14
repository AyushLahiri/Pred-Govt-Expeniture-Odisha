
# Tracking development outcomes in Indian villages, 2011-2020

Targeting and assessing development policy measures requires fine-grained data. While India has a relatively robust data infrastructure among developing nations; granularity and frequency are major issues. The decennial census of India, last conducted in 2011, is the most complete enumeration of public goods and infrastructure at the village level. 

### Why is Odisha of interest?

Within India, the state of Odisha has some of the poorest economic and human development indicators. A large proportion of the state's residents are historically marginalized indigenous groups, assured special Constitutional protections. Settlement patterns track the high **forest cover** in the state. The state also has large mineral deposits of coal, steel, bauxite and chromite, and thus a large presence of **mining operations**.

### Rural local government funding

To promote decentralization and development, elected village councils (Gram Panchayats, GP) are supposed to submit plans for infrastructure and development expenditure before each fiscal year. 


### Endline data - missing?

However, since the Census of 2021 was delayed, there is no reliable, large-scale, granular endline data that allows an assessment of how funding has changed outcomes. In similar cases, **satellite data** of nightlights or built-up area has been used in other, comparable, data-scarce contexts.


## Data

 Make sure you have two files with these names in the `./data` folder:

[census_infra_od.csv](https://www.dropbox.com/s/b9w156q75ngyr5k/census_infra_od.csv?dl=0)
 - The census data contains 51313 data points across 396 variables which capture multiple demographic, geographical, infrastructure and public good outcomes over 5531 gram panchayats.

[exp_t4.csv](https://www.dropbox.com/s/81q8tp2gvdkhdjn/exp_t4.csv?dl=0)
- Data from India’s Ministry of Panchayati Raj (MoPR) contains village level expenditure data over 5 years from 2017-2022, across the nature of public projects undertaken and the estimated expenditure for projects . The dataset contains 1489471 data points in the state of Odisha across 19 variables over 6049 Gram Panchayats.

## Execution

1. Open and run the [`01_cleaning.ipynb`](https://github.com/bhollan/DS_F22_IFP/blob/master/code/01_cleaning.ipynb) file and run all cells.

2. This will result in the `analysis_df.csv` file creation. 

3. Run [`02_cleaning.ipynb`](https://github.com/bhollan/DS_F22_IFP/blob/master/code/02_analysis.ipynb). This uses the `analysis_df.csv` file.



### Organization

The village level expenditure data is captured at the district, block and the GP level. The census data is organized at the State (redundant in our case since our data is from a single state), District, Sub-district, Block, Gram Panchayat and Village level. We focus on the district, block and gram panchayat levels.

The primary distinction between the village panchayat and village level is as follows: The village level government i.e. the panchayat, is formed at a single village. This village can be analogously seen as the village level government “headquarter”. Multiple villages then fall under the jurisdiction of a single village level panchayat.
![](./Assets/Schema.png)

## Merging of Datasets 

### Mismatch in GP names

The census and expenditure level data will be effectively matched at the GP government level. In order to match at the GP government level, which can be common for villages, we create keys based on the GP government, the block and district. In an ideal scenario, these keys should match for both datasets, that is not the case, primarily due to two reasons:

 1. Panchayat/Block names have been spelled differently across the two data sets and also within datasets.
 2. New panchayats/Blocks/districts have been created between 2011 and 2022. This affects matching on the expenditure level data as it is longitudinal and captures the new political demarcations, which do not exist in the census data which only exists for 2011

The proportion of matches, at each of the three levels of demarcation are shown below and will be reconciled using fuzzy string matching of these names:

![](./Assets/Propotion.png)

### Infrastructure levels and funding demand

We look to probe into broader trends and questions of how per capita expenditures evolve across time and amongst other trends, investigate if higher/lower expenditures in the future are correlated with past lower/higher expenditures. 
These questions will also span across expenditure trends in specific sectors and how/if prioritization of sector wise expenditure is changing over time. 

### Segregation
We also intend to broadly study the question of how segregation of villages based on the population's caste status, affects a village’s ability to demand better public good provision for their villages. We aim to do this by computing the segregation and fractionalization measures used by [Tajima Et al.](https://doi.org/10.1017/S0003055418000138)[[1]](#1), adopted from [Goodman and Krushal](https://doi-org.proxy.library.georgetown.edu/10.1080/01621459.1954.10501231)[[2]](#2)


### References 
<a id="1">[1]</a> 
TAJIMA, Y., SAMPHANTHARAK, K., & OSTWALD, K. (2018)
Ethnic Segregation and Public Goods: Evidence from Indonesia
American Political Science Review, 112(3), 637-653.

<a id="2">[2]</a> 
Goodman, Leo A., and Kruskal, William H. (1954)
Measures of Association for Cross Classifications.
Journal of the American Statistical Association 49 (268): 732–64.

