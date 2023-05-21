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
Once the data was loaded in and in the desired format, I created the measures needed. I started by creating a measure to sum together the values.
```
Character Value = 
SUM(Characters[Value])
```
I then used this measure to create a ranking measure that ranked the characters based on the user selections.
```
Character Rank = 
RANKX(
    ALLSELECTED(Characters[Character]),
    [Character Value],
    ,
    ,
    Dense)
```

I created the same measure for each of the other tables. I then created an overall value measure and rank measure which summed together the outputs of each of the variables. 

The first report page only looks at the characters table so I created a parameter to use in both the visuals that switches between the value and the rak. The user can then select which they are interested in. 
```
Character Parameter = {
    ("Character Rank", NAMEOF('Characters'[Character Rank]), 0),
    ("Character Value", NAMEOF('Characters'[Character Value]), 1)
    
```

The other slicer on the first page is the character weight so the user can look at combinations of heavy/light/medium weights. The first visual shows the values per attribute for each mario character. I added in the weighted colour in the background so the user can quickly see what is driving the overall value. 
![image](https://github.com/Hannahllmm/Power-BI-Projects/assets/39679731/ad6ae93c-926d-4f13-93de-06cb71c4f8d1)


The second visual shows the percentage each attribution makes up of the overall attribute. It shows the same data as the other visual but sometimes it's easier to see which attribute is weighted the highest based on area rather than colour.
![image](https://github.com/Hannahllmm/Power-BI-Projects/assets/39679731/de7025d6-6edc-42c2-ba2b-75410f6576e1)

The second page allows user so test out making kart selections to see how that affects the over all values. Again I created a parameter, this time to switch between the overall value and rank so the user can switch between the two. I used the same table visual as on the previous page, this time there are more slicers for the suer to choose from.

![image](https://github.com/Hannahllmm/Power-BI-Projects/assets/39679731/4b5b14a2-4e32-4f41-966e-dd3a522980e4)

