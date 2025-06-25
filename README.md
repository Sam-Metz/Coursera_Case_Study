# Coursera_Case_Study
I analyze the data of Fitbit users to derive marketing insights for my stakeholders. This is a case study for my Google Data Analytics Certificate.
## Prompt
* You are a data analyst for a company called Bellabeat. Bellabeat makes wearable fitness devices.
* Your team has been asked to anazlyze trends in smart fitness device usage in an effort to help Bellabeat reach their target market more effectively.
* This data set about fitbit users is provided by the company: [https://www.kaggle.com/datasets/arashnic/fitbit]
* Questions:
    * What are some trends in smart device usage?
    * How could these trends apply to Bellabeat's customers?
    * How could these trends influence Bellabeat's marketing strategy?
### Phase One: Ask
* Are users wearing the watch as a fashionable accessory? Do they wear it all day?
* Do users frequently log their weight in the device?
* What time of day do users typically exercise?
* How far do users go during a workout?
* How long do users workout for?
* How hard do users workout?
* How much sleep do the users get per night?
### Phase Two: Prepare
* Is the data reliable?
    * For purposes of this case study, I will use this data set. However, it is important to note the we are trying to make a claim about Fitbit users. Therefore, our population would be 38.5 million people. If we wanted to make claims about this population with 95% certainty, we would need a sample size of at leat 385 participants. If this were a real life scenario, I would recommend that we find a more representative data set.
    * Further, the source of this data is Amazon Mechanical Turk. Therefore, this dataset is not random and it was not vetted for bias.
* Is the data the original set?
    * Yes
* Is the data comprehensive?
    * The data includes enough information to allow us to answer our questions about the users included.
* Is the data current?
    * This data set is updated annually.
### Phase Three and Four: Process and Analyze
* Are users wearing the watch as a fashionable accessory? Do they wear it all day?
    * For this task, I used the heartrate_seconds_merged.csv tables. There is one for the first date range (3/12-4/11), and one for the second date range (4/12-5/12). A preview of this table is shown below. A user must be wearing the watch for their heartrate to be tracked. Therefore, this table will show us how long each user wears their watch:
    * ![Heartrate Table Example](heart_rate_table.jpg)
    * First, I cleaned this data by formatting the id’s to a number and expanded the date row to include all information.
    * Second, I uploaded the tables to Bigquery.
    * Third, I applied the following steps to the datasets for both date ranges:
         * I found the number of days that each user was wearing their fitbit during the date range.
            * To do this, I applied the following SQL query to the heartrate table:
            * ![Day Count Query](day_count_query.jpg)
            * Below is the table created by this query:
            * ![Day Count Table Example](Day_Count_Table_Example.png)
                 * I then ran the following query on the table above to find the total number of days per user during the range:
                 * ![Day Count Final Sum Query](Day_Count_Final_Sum_Query.png)
                 * Below is the table that resulted from running this query:
                 * ![Days by User Table Example](Days_By_User_Table_Example.png)
         * Now that I knew the total number of days per user for this date range, I needed to find the number of hours that each user wore the watch during the date range.
            *  To do this, I ran the following query on the original heart rate table:
            *  ![Hour Count Query1](Hour_Count_Query1.png)
            *  This resulted in the following table with the start and end time on each day for each user:
            *  ![Hour Count Table1](Hour_Count_Table1.png)
            *  Then, I ran the following query on the table above to add the total duration per user:
            *  ![Hour Count Query2](Hour_Count_Query2.png)
            *  This resulted in the following table:
            *  ![Hour Count Table2](Hour_Count_table2.png)
            *  I joined this table with the day count table using the following query:
            *  ![Hour Count Query3](Hour_Count_Query3.png)
            *  This resulted in a table that shows the Fitbit Id, total days the fitbit was used, and the total hours the fitbit was used. Below is a snip of the table for the 3/12-4/11 dataset:
            *  ![Hour Count Table3](Hour_Count_Table3.png)
         * Since I applied these steps to both date ranges, I ended up with 2 tables.
            * I combined these tables in Excel and added.  
            * In a new tab, I used a sumif function to total the number of hours per user in one column and the number of days per user in another.
               * I added a third column that divides the hours used by the days used to find each user's average daily use.
            * In a new sheet, I created a table that used a countif function to add the number of users that fell within each usage range as shown below:
            *  ![Final Usage Range Table](Final_Usage_Range_Table.png)
            * I used Excel to create a chart from this table as shown below:
            * ![Final Usage Range Chart](Final_Usage_Range_Chart.png)
* This chart shows us that most fitbit users wear their watch between 12 and 24 hours per day. My recommendation to my stakeholders would be to market their product to users who are looking for a fashionable watch that they can wear all day, not just while working out. 
