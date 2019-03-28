# Data-analysis--Python-for-data-cleaning-regex-etc.
Python- regex and other methods for data cleaning


# Using regex for cleaning and parsing string data:

## Code demo from data extracted via an ETL/web crawler of IMDB data (note: see following repo for more detailed analysis: 

### Python for data cleaning via regex library:

After extracting 80+ years of films data from the IMDB database, which inputted the data into lists for each variable, some of
these lists contained data that needed to be cleaned.

The most severe case was the list of years data. The elements of the list sometimes contained ranges of years or extra characters
such as "-" or "TV Movie". 

Python's regex library allows this list of data to be parsed and cleaned.

### For a visual of how the original/raw data of the 'years' list looked (i.e., immediately after implementing the web crawler):

<img width="802" alt="Screen Shot 2019-03-27 at 5 58 55 PM" src="https://user-images.githubusercontent.com/35751364/55122603-c0c94380-50bc-11e9-916f-b9fe0b8cd285.png">

## Python code--via regex library--for cleaning and parsing the list of string data:
```
#import regex library
import re

#define a function for specifying the regex function
def splitting(year):
    s = re.findall(r'\d{4}', year)
    if s:
        #return only the first set of results: i.e., the first year that's listed in each row of the year column
        return(s[0])

#apply the "splitting" regex function to the year column, and assign/save this in the column
imdb_data['year']  = imdb_data['year'].apply(splitting)

```

After applying the regex function to the year list/data, the elements of the list were parsed and cleaned such that the 
list of data could be converted to integer, and then placed directly in a Pandas Dataframe.

The end result can be seen as follows:
<img width="953" alt="Screen Shot 2019-03-27 at 6 43 37 PM" src="https://user-images.githubusercontent.com/35751364/55123801-2d464180-50c1-11e9-80b0-53af245574cf.png">
### Convert elements from the year list to integer:
```
#convert the year column to integer
imdb_data['year'] = imdb_data['year'].astype(int)
```


