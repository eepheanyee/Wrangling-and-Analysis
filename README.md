## Reporting: wrangle_report

##### A journey through the data wrangling process

### Extracting Data

I started the process by gathering the data from the 3 different sources using 3 methods.  
  - The tweet_archive dataset was downloaded and imported using the pandas read_csv method
  - The image prediction data was downloaded using the requests library and the provide url then the data was stored into a file
  - The twitter api was used to programmatically download tweet data from twitter and store it in a json file. This took a while as there were a lot of tweet data to receive and the twitter api has to sleep after a while before continuing.

### Assessing Data

I assessed the datasets programmatically and visually to check for quality and tidiness issues. The issues I discoverred are below:
  - There were missing data in the a lot of the missing columns in both the tweet_archive and tweet_json datasets.
  - Some of the columns had incorrect data types and need to be changed.
  - The datasets included not only tweets but also retweets. The retweets had to be dropped because we were focusing on just the main tweets
  - Some of the dog names were in accurate, etc.
For the tidiness, I also found some issues:
  - I needed to merge data in some columns of the image prediction and tweet archive data sets to form new columns, dog_breed and dog_stage.
  - The tweet_archive and tweet_json datasets had a lot of common column and one had to be dropped.\

### Cleaning Data

Now, unto the messy part. I proceeded to clean all the issues earlier detected. Here are some of the techniques used in cleaning the data.
  - I first made a copy of all three data sets.
  - I started with missing values. The expanded_url column of twee_archive dataset coould be gotten by concatenating the tweet_id and url columns which is what I did to fill up the missing values.
  - Other columns with missing values more than 50% of the total data available were dropped using the pandas drop method
  - I removed the retweet data by matching regex expressions and finding tweets that started with the `RT` marker.
  - I then replaced all the irregularities in the name columns with none as extraction from the available data was not feasible.
  - I merged the dog stage columns into one by defining a function that checks the four columns and inserts the value that is not none in the dog_stage column, then I applied the function row by row.
  - Also defined a function to determine the dog breed by first checking the P_dog columns to make sure that the predictions are actual dog breeds, I then find the max of the p_conf columns to determine the best fit, then return the breed of the dog. This function was also applied row by row using the pandas apply function.
  -  After cleaning the individual datasets, I merged them to form one final `tweet_archive_master` dataset

### Storing Data

I proceeded to store the final master dataset into a new csv file before starting my analysis.
