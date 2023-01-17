# Functions for producing Timber Price Indices

:warning: **This is a prototype R package under constant development.**

:evergreen_tree: This packages provides functions to produce Forest Research's Timber Price Indices publication as a [Reproducible Analytical Pipeline](https://dataingovernment.blog.gov.uk/2017/03/27/reproducible-analytical-pipeline/) (RAP).

# Background

[Forest Research](https://www.forestresearch.gov.uk/) produces price inflation statistics from the sale of timber grown on public land in Great Britain.
Transaction (sale) data come from Forestry England, Natural Resources Wales, and Forestry and Land Scotland, with price indices published biannually (data to 31 March published in May and data to 30 September published in November).
For more information, see [FR's forthcoming releases page](https://www.forestresearch.gov.uk/tools-and-resources/statistics/forthcoming-publications/).

## The Coniferous Standing Sales Price Index (CSSPI)

The CSSPI monitors changes in the average price received per cubic metre overbark for timber sold standing, where the purchaser is responsible for harvesting.
The index is adjusted for timber size mix using the Fisher method with 5-yearly chain linking.

## The Softwood Sawlog Index (SSI)

The SSI monitors changes in the average price received per cubic metre of sawlogs sold at roadside, where sawlogs are defined as roundwood with a top diameter of 14 cm or more, likely to be sawn into planks or boards.

In addition, two sub-indices of the SSI are published:

-   The Spruce Sawlog Index,
-   The Other Conifers Sawlog Index.

## Small Roundwood Index (SRI)

The SRI monitors changes in the average price received per cubic metre for roundwood that is smaller in diameter than sawlogs, sold at roadside.
This includes chipwood, pulpwood and woodfuel.

Standing timber, sawlogs and small roundwood are distinct markets and may show different price movements.
The data are averages for historic periods, so may be slow to show any true turning points.
These indices are used to monitor trends in timber prices and to provide information on the state of the UK timber industry.
They are also used by the UK timber industry, alongside other economic indicators, in contract reviews.

The Timber Price Indices publication is designated [National Statistics](https://osr.statisticsauthority.gov.uk/national-statistics/) and are produced in full compliance with the [Code of Practice for Statistics](https://code.statisticsauthority.gov.uk/).

# Installation

The package can be installed using `devtools::install_github("ForestResearch/timbRinflation")`.
Some users may not be able to use the `devtools::install_github()` function as a result of their network security settings.
If this is the case, `timbRinflation` can be installed by downloading a [zip of the repository]() and installing the package locally via `devtools::install_local(<file path>)`.

# Getting started

The package includes functions which ingest the data into R, perform data wrangling and QA, and calculate the price indices.
The majority of the functions contained within are for the production of the more complex CSSPI.

### Extracting data from underlying spreadsheets

The data are provided to FR from Forestry England, Natural Resources Wales, and Forestry and Land Scotland and in spreadsheets.
Here, the first set of function in the package are designed to extract the data from the spreadsheets and combine the data into a single data set, ready to be QA'ed, before going into the statistics notice.

There are three `read_*` functions:

-   `read_css_worksheet`
-   `read_ss_worksheet`
-   `read_sr_worksheet`

There are three `combine_*` functions:

-   `combine_css`
-   `comebine_ss`
-   `combine_sr`

### Data preparation

#### CSSPI: 5-yearly chain linked Fisher index :link:

The package contains 6 functions to produce the CSSPI:

`aggregate2gb()`: takes a 5-by-n data frame (date, country, tree_size, value, volume) and returns a 4-by-n data frame with total value and total volume for each date and tree size.

`get_p1q1()`: takes a 4-by-n data frame (date, tree_size, value, volume) and returns a 4-by-n data frame primed for analysis (date, tree_size, p1, q1), where p1 is the price in the period t1 and q1 is the quantity (i.e., volume of standing timber sold) in the period t1.

`bind_p0q0()`: takes a 4-by-n data frame and a vector of reference (base) periods and binds p0 (the price in the reference period) and q0 (the quantity in the reference period).

`bind_link_id()`: takes date and a vector of reference (base) periods and adds a new variable which equals 0 for the current link period, 1 for the preceeding link period, 2, 3, ..., n, etc.
Where the maximum link ID variable n equals the total number of links - 1.

`bind_link_factor()`:

`link_chain()`: a for-loop which performs the chain-linking.

#### SSI & SRI

`bind_simple_index()`: inputs: price & reference period.

### Automated QA

WIP.

### Creating the publication :chart_with_upwards_trend:

WIP - .qmd report.

Loads the R package `ggGSS`.
This aligns all data visualisations with Government Statistical Service (GSS) guidance.
To install the package, run `devtools::install_github("ForestResearch/ggGSS")`.

## Licence

This information is licenced under the conditions of the [Open Government Licence](http://www.nationalarchives.gov.uk/doc/open-government-licence/version/3).

The following attribution statement MUST be cited in your products and applications when using this information.

> Contains public sector information licensed under the Open Government licence v3.

### About the license

The Open Government Licence (OGL) was developed by the Controller of His Majesty's Stationery Office (HMSO) to enable information providers in the public sector to licence the use and re-use of their information under a common open licence.

It is designed to encourage use and re-use of information freely and flexibly, with only a few conditions.

# Authors

This package was built by Simon Maxwell and is maintained by Daniel Braby.

For more information, contact [statistics\@forestresearch.gov.uk](mailto:statistics@forestresearch.gov.uk).
