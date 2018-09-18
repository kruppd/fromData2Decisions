# Data Entry Analysis Assignment
The purpose of this assignment is to identify data quality issues from three different data files. In addition to the typical concerns regarding data quality like accuracy and completeness, one of the underappreciated challenges with data organization is for one to decide when to use a wide data format versus a tall approach.

Choosing an approach to organize data is a key decision for any longitudinal study, especially when trying to balance best practices between statistical data analysis and relational database management. Normalization helps reduce unnecessary duplication for records but can add complexity with how the dataset is spread out in different files, which would have to be joined together again for certain analyses. I tried to include both of these perspectives for my solution.

## Data Quality Issues with the Plankton Data Files

#### Issues affecting all files
*	Station A, Station B, and 2010 observations should not be in separate files or tabs, and a station attribute should be added to the main file to organize this data in one table. 
*	A time of day attribute is needed to show why different colony sizes are occurring within the same day.
*	Depth and temp are being repeated three times with the same exact value, which creates unnecessary duplication. These columns are good candidates to be placed in a separate file.
*	Chla is being duplicated twice. I decided it would best to separate into a different file, while transforming the cuni and chippo data in a taller format. This should make it easier to analyze how location (station), depth, species, time of day, etc… affect the dependent variables.
*	At a minimum, data organization should be consistent, pond2010 is a tall file, which is more normalized, than the wide file approach for zoop – temp and zoop – temp main.
*	Some data values are formatted with red text without any indication why. This is a problem for two reasons: first, if these values are being highlighted for a reason, then the reason is not being documented or communicated to the dataset's consumers. Second, statistical and data visualization programs will not read these format differences, so the significance of this information will be quickly lost. A new attribute to flag this information should be used, and the metadata should describe its significance.
*	A more consistent data collection plan and naming is needed, because it’s unclear if the 2010 should be combined or separate from the 2011 files. Especially when a team is planning to trend observations from a longitudinal study, the dataset needs to be consistent.
* The units are not explicit in all files. Combining observations in one file should make it easier to manage metadata, units, and column naming conventions.
* If this dataset will be shared to the academic community for future analysis, then graphs shouldn't be embedded with the underlying data.

#### Issues affecting zoop – temp-main file
*	Row 29, Col H: The 37.8 value is most likely a data entry error, because it doesn’t follow the duplication pattern of other entries and is more than twice the value of the next highest observation.
*	Row 1, Col H: The scatter plot’s y-axis formula is ('Station A'!$H$1:$H$46,1), where H1 is the data header. This error is causing the scatter plot to show an observation of 0 on 6/4/2018 that doesn’t exist in the data.
*	Row 23, Col H: An asterisk is used instead of a null value, which is a problem for two reasons. First, Excel is plotting this observation as 0 on the scatter plot. Second, an asterisk character is nominal data, which is different from the ratio format used for the numerical observations. This may cause issues when using a statistical or data visualization program without cleaning or prepping this data beforehand.

#### Issues affecting zoop – temp file
*	Negative values don't make sense for the density measurements. This is likely a data entry error.
*	Metadata should be in a separate file or tab instead of the first five rows of the actual data observations. Data types should be consistent for each row within each column.

#### Issues affecting pond2010 file
*	2010 data lacks metadata
*	Consistent naming should be used. In pond2010, depth appears to be labeled as “z”, while the other two use “Depth”. Also, “Colony Diameter” and “Density”, which appears to represent “Colony Size” and “cunni/L” and “chippo/L”. I decided to drop “z” but use the "Density" and "Colony Size" in my file.
*	This file needs to have a station and time of day attribute, so the analyst knows where and when the observation data is occurring.
*	Lacks Chlorophyll measurements. I kept this attribute in a separate file, because I'm not sure of what units are being used.

## New Data Organization Example
* Note that these data are simulated, not real! S.E. Hampton; 27 June 2012
* Null represents no observation taken during that period

#### Plankton Observations Example
| Date | Station | Time |  Depth (m) | Density (#/L) | Colony Diameter (mm) | Species |
|--------|:---:|:-------:|:-----:|:----:|:------:|------|
| 6/4/11 | A | 02:00 | 0.5 | 72 | 2.12 | cuni |
| 6/4/11 | A | 12:00 | 0.5 | 54 | 1.98 | cuni |
| 6/4/11 | A | 18:00 | 0.5 | 35 | 2.34 | cuni |
| 6/4/11 | A | 02:00 | 5.0 | 45 | 1.60 | cuni |
| 6/4/11 | A | 12:00 | 5.0 | 54 | 1.98 | cuni |
| 6/4/11 | A | 18:00 | 5.0 | 35 | 2.34 | cuni |
| 6/4/11 | B | 02:00 | 0.5 | 70 | 3.46 | chippo |
| 6/4/11 | B | 12:00 | 0.5 | 68 | 3.28 | chippo |
| 6/4/11 | B | 18:00 | 0.5 | 57 | 3.01 | chippo |
| 6/4/11 | B | 02:00 | 5.0 |    |      | chippo |
| 6/4/11 | B | 12:00 | 5.0 | 70 | 3.71 | chippo |
| 6/4/11 | B | 18:00 | 5.0 | 37 | 3.9  | chippo |

#### Chlorophyll Observations Example
| Date | Station | Time | Depth (m) | Amount | Type |
|--------|:---:|:-------:|:-----:|:----:|------|
| 6/4/11 | A | 02:00 | 0.5 | 3.1 | Chlorophyll a | 
| 6/4/11 | A | 12:00 | 0.5 | 3.4 | Chlorophyll a |
| 6/4/11 | A | 18:00 | 0.5 | 3.2 | Chlorophyll a |
| 6/4/11 | A | 02:00 | 5.0 | 3.3 | Chlorophyll a |

#### Plankton Stations Example
| Date | Station | Depth (m) |  Temp (C) |
|------|:-------:|:---------:|:---------:|
| 6/4/11 | A | 0.5 | 14.1 | 
| 6/4/11 | A | 5.0 | 13.8 | 
| 6/4/11 | A | 10.0 | 12.3 | 
| 6/4/11 | A | 25.0 | 8.2 | 
| 6/4/11 | A | 50.0 | 7.5 |
| 6/5/11 | A | 0.5 | 15.7 | 
| 6/5/11 | A | 5.0 | 13.9 | 
| 6/5/11 | A | 10.0 |  |
| 6/4/11 | B | 0.5 | 18.2 |
| 6/4/11 | B | 5.0 | 15.8 |
| 6/4/11 | B | 10.0 | 14.2 |

#### Metadata Example
| Name | Data Type | Description |
|------|---------|-----|
| Station | String | Location of observations, Station B is in a shallower southern arm of the lake. |
| Time    | Date/Time | Samples are collected at three different times of day: 2AM, 12PM, and 6PM. | 
| Depth    | Float | Samples are taken at different depths to see differences. | 
| Density (#/L) | Float | Density is measured as number of organisms per liter. | 
| Colony Diameter (mm) | Float | Colony size is measured by the diameter in millimeters.  |
| Species | String | This study focues on cuni and chippo species of plankton. | 
| Amount | Float | The amount of chlorophyll present |
| Type | String | Type of chlorophyll measured |
| Temp | Float | YSI probe taken once at each depth and measured in Celsius |
