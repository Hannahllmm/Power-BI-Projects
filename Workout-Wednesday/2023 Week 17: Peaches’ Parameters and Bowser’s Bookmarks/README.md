# 2023 Week 17: Peaches’ Parameters and Bowser’s Bookmarks

## Contents
- [Description](#description)
- [Data Transformation](#data-transformation)
- [Set-up](#set-up)

### Description
Find the full description of the project [here](https://workout-wednesday.com/pbi-2023-w17/). I added the data provided to excel and connected Power BI to that. I then created a report with one page that summarises characters base values and then another where the user can test out kart selections to see how that affects characters performance.

This is the first page of the report:
![image](https://github.com/Hannahllmm/Power-BI-Projects/assets/39679731/51b96317-bee0-48ff-bd61-cbdc68544b68)

This is the second page:
![image](https://github.com/Hannahllmm/Power-BI-Projects/assets/39679731/307a1a89-bc6d-4fb6-a5af-f074919f81ea)

### Data Transformation

This is a very simple report that connects to just one xlsx file. On each of the 4 tables I performed these transformations:

1. I unpivoted the data so all the attributes were in one column
2. I split the attributes by delimitor so the environment was in a column of its own
3. Renamed the columns and removed any not needed
4. I replaced the null values in environment with "All" as this was the overall value for each attribute
5. Finally I trimmed the attribute column to remove the white space

I repeated the same process for each of the tables. Lastly I created two new tables, one listing the distinct attributes and one listing the environment. These two tables could then be used as dimentions to link the other tables together. Ideally I would have created an ID column and linked the tables using that as relationships between numerical values is preferable to text for performance, but for such a small dataset it didn't matter.

This is how the tables are connected to each other:
![image](https://github.com/Hannahllmm/Power-BI-Projects/assets/39679731/aa4238dd-3bde-495f-bff8-275d53592185)


### Set-Up
Once the data was loaded in and in the desired format, I created the measures needed.
