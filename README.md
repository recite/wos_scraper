## Web of Science Scraper

To collect retracted articles and the articles that cite them, we wrote a scraper for Web of Science. The script feeds the data used [here](https://github.com/recite/propagation_of_error).

### Scripts

* [scripts](scripts/)

### Requirements

1. Python(2.7) and selenium  
2. Chrome (>= 51.0.2704.84).  
3. Make sure the chromedriver.exe (download it from https://sites.google.com/chromium.org/driver/, version>=2.22) is at the same path as the main script while running

### Running the Script

To get started, clone the repository and run: 

```
python web_scraping.py
```

### Config. File

The script provides four different modes of execution. To choose the mode, edit the configuration file.

* **Mode 1:**  
  * CITATION_LIST_ONLY: 0 or 1. If set as 1, the program will only generate the citation list. If you want to use this mode, specify a retracted article list file that already exists in the same directory as the script.
  
  * MAX_CITATION_NUMBER: A positive integer. The maximum number of titles within the retraction list that the user wants to search for generating the citation list.

* **Mode 2:**   
  * RETRACTION_LIST_ONLY: 0 or 1. When set as 1, the program will only generate the retraction list.

  * MAX_RETRACTION_NUMBER: A positive integer. The maximum number of retracted articles for generating the retracted article information list. (The minimum is 500 records if the total number of retracted articles is >500.)

* **Mode 3:** If CITATION_LIST_ONLY and RETRACTION_LIST_ONLY are both set to 0, the program will generate both files without any upper bound---MAX_CITATION_NUMBER and MAX_RETRACTION_NUMBER won't affect the program anymore.

* **Mode 4:** When the above two variables are set to 1. This is for the test only.

Other parameters within the configuration file:

* RETRACTION_LIST_NAME: The name of the retraced article information list file. It must end with a .csv

* CITATION_LIST_NAME: The name of the cited article information list file. It must end with a .csv.

* WEB_SCIENCE_USERNAME & WEB_SCIENCE_PASSWORD: email and password to log into Web of Science

* TITLE_WITH_DATE: For the cited article information collection only, the user can include the retraction/correction date within the article title for search (set to 1 then) or not (set to 0 then)

* CONTINUE_WRITE: Do you want to overwrite the existing information or not? If set to be 0, the program will clean all the existing information within the generated file and replace it with the new data. (Only available for citation list only mode or retraction list only mode.)

* WHERE_TO_START: Only useful when CONTINUE_WRITE been set to 1, tell the program where to start (which row or title to be the first one used for search)

* FAILED_SEARCH_FILE: The file name of the failed title search information. Must end with a .csv.

* CREATE_FAIL_FILE: If the user wants to create a file for recording the failed title search information, set this to 1, otherwise set it to 0 

### Possible Failed Search Conditions 

* The syntax of the title is not valid for Web of science. 

* Web of Science cannot find any record matching the title.  

* The article used for search has been cited 0 times. 

### Potential Issue 

The Number of Search Results Change: If the user searches "retraction of" and then refines with "RETRACTION" and "CORRECTION " and then sorts by "times cited-highest to lowest," it will show there are 9,599 records in total on the left-hand side. But if the user clicks "Add to Marked list" and fills the condition with "from 5500 to 6000", it will show you only 377 records, and the number on the left side will become 5876. The reason appears to be that the 9k results include duplicates.
