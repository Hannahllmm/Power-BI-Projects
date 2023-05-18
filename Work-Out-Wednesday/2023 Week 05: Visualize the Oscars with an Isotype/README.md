# 2023 Week 05: Visualize the Oscars with an Isotype

## Contents
- [Description](#description)
- [Data Transformation](#data-transformation)
- [Set-up](#set-up)

### Description
Find the full description of the project [here](https://workout-wednesday.com/pbi-2023-w05/) including a link to the data used. I connected to the xlsx file provided and created a simple report with one graph showing the number of nominations per films in the 2023 oscars, users can filter the data be award categories.

This is the view the user sees initially:
![image](https://github.com/Hannahllmm/Power-BI-Projects/assets/39679731/109c86bd-a511-43da-a1ac-c91e88151db0)


After clicking on the hamburger this is what the user sees:
![image](https://github.com/Hannahllmm/Power-BI-Projects/assets/39679731/dfae7241-be14-4cb1-9cba-9ac38e475ceb)

They can then select the categories they're interested in and click the back button to view the graph again.

### Data Transformation

This is a very simple report that connects to just one xlsx file, so not much data transformation is needed. After connecting I filtered the data so only the awards data for 2023 was shown, I thien removed any columns that weren't needed.

```
let
    Source = Excel.Workbook(File.Contents("C:\Users\Hannah.Morrison\Power BI Projects\Oscars\the_oscar_award.xlsx"), null, true),
    oscar_awards_Sheet = Source{[Item="oscar_awards",Kind="Sheet"]}[Data],
    #"Promoted Headers" = Table.PromoteHeaders(oscar_awards_Sheet, [PromoteAllScalars=true]),
    #"Changed Type" = Table.TransformColumnTypes(#"Promoted Headers",{{"year_film", Int64.Type}, {"year_ceremony", Int64.Type}, {"ceremony", Int64.Type}, {"category", type text}, {"name", type text}, {"film", type text}, {"winner", type logical}}),
    #"Filtered Rows" = Table.SelectRows(#"Changed Type", each ([year_ceremony] = 2023)),
    #"Removed Other Columns" = Table.SelectColumns(#"Filtered Rows",{"category", "name", "film"})
in
    #"Removed Other Columns"
```

### Set-Up

I created a background for the report using Power Point which is helpful when you want static images and titles in the report as you don't need to spend time aligning all the visuals. 

Next I created a couple of measures. Firstly I created a Nominations measure to cound the nominations, this was used in the graph.
```
Nominations = COUNT(oscar_awards[name])
```
The other measure Selected Categories, outputs text which is isused to create part of the title on the page. This dynamically changes dependant on what the user has selected. 
```
Selected Category = 
IF(
    ISFILTERED(oscar_awards[category]),
    "For " &
    CONCATENATEX(
        VALUES(oscar_awards[category]),
        oscar_awards[category],
        ", "),
    "For all award categories")

//This outputs a list of the categories the user has selcted from the slicer, if all categories are selected then it outputs "all award categories"
```
I added this measure as the text in a shape. This alowed me to align the text as I wanted.
This is displayed when all categories are selected:

![image](https://github.com/Hannahllmm/Power-BI-Projects/assets/39679731/fedbaeb0-7d2c-4d73-91f9-fef00b0b8079)

This then changes when the user selects specific categories:

![image](https://github.com/Hannahllmm/Power-BI-Projects/assets/39679731/d6f0c8e2-8707-4c35-b3db-0230d981141a)

Then I downloaded the custom visualisation Infographic Designer 1.9.7, this is a brilliant tool allowing formatting options that the default graphs don't. I used little statues to show how many nominations each film had recieved. 

I added in a slicer with a background colour to match the rest of the report. I hid the different buttons and the slicer to create two bookmarks, one that displayed the default view of the report, and another with the slicer in view. I then linked the buttons to the relevant bookmarks. I turned off data in the bookmark so when the user closed the slicer the options they had selected stay. 

