# Kickstarting with Excel

## Overview of Project
Louise is looking to compare her fundraising campaign results for her play "Fever" to other similar fundraisers. She would like to know how her fundraiser could be more successful based on launch date and funding goal.  

### Purpose

The purpose of this analysis is use historical data from past successful, failed, and cancelled campaigns to determine the optimal launch date and funding goal for a fundraising campaign for a Theater Play. 

## Analysis and Challenges

Below I will discuss my analysis

### Analysis of Outcomes Based on Launch Date

I began with looking at outcomes based on launch date and determined it would be best to group campaigns by month.

First from the raw data time was in Unix timestamps and had to be converted to a more readable day-month-year format. This was done using the formula below:

    =(J2847/60/60/24)+DATE(1970,1,1)
     - J2847 is the cell of the Unix timestamp
     - "/60/60/24" converts from seconds to days
     - That is then added to Jan 1 1970 because Unix timestamp is the amount of seconds from midnight that date.

I created a Year column using the =YEAR() formula in excel to help with further filtering

A pivot table was then created using Parent Category and Years as filters, Outcomes as columns, Date Created Conversion(months) as rows, and Count of Outcomes as Values. The pivot table was then filtered to only show the Theater Parent Category and Column Labels were sorted descending (Z to A) and "live" campaigns were filtered out due to not being relevant to the analysis we are conducting.  The pivot table can be seen below. 

#### Table 1. Theater Outcomes VS Launch Date Pivot Table
![Theater_Outcomes_vs_Launch_Pivot_Table](https://user-images.githubusercontent.com/57120024/156237918-db6b6b61-db0b-486f-b13b-95da2fb8bda6.png)


### Analysis of Outcomes Based on Goals

After I determined optimal launch month, I went on to look at optimal funding goal.

I started by making new a sheet and table shown below. The goals were divided into ranges, below 1000, above 50000, and everything in between in ranges of 5000. The number of successful/failed/canceled columns were then populated using a countifs function. An example of the formula is:

    "=COUNTIFS(Kickstarter!D:D, ">=1000",Kickstarter!D:D, "<=4999",Kickstarter!F:F,"successful", Kickstarter!R:R,"plays")" 
    
        - the first set of arguments, Kickstarter!D:D, ">=1000",Kickstarter!D:D, looks for goals above the lower value
        - the second, Kickstarter!D:D, "<=4999",looks for goals below the upper value
        - the third, Kickstarter!F:F,"successful", whether the campaign was successful, failed, or canceled
        - the final, Kickstarter!R:R,"plays", filters the campaigns to the play subcategory

A sum function was then used to total the number of campaigns per goal range to be used to determine the percentage of each outcome. The percentage was a simple number of outcomes divided by the total campaigns. The results of this table can be seen below.

#### Table 2. Outcomes VS Goals

![Outcomes_VS_Goals_table](https://user-images.githubusercontent.com/57120024/156238194-5518a524-8cfc-41ae-b7d9-e2f8f812daec.png)


### Challenges and Difficulties Encountered

## Results

- What are two conclusions you can draw about the Outcomes based on Launch Date?

    1. The best month to launch a campaign is in the month of May. From the past data there were 111 successful campaigns out of 166 launched, about a 67% chance of success. 

    2. Beginning and end of year should be avoided when starting a campaign.

    A chart showing Outcomes based on launch date can be seen below
    
   
   ![Theater_Outcomes_vs_Launch](https://user-images.githubusercontent.com/57120024/156238487-0ec695cb-711d-4696-992b-17c98f67426c.png)
  #### Figure 1: Theater Outcomes VS Launch Date


- What can you conclude about the Outcomes based on Goals?

    Campaign goals below 20000 have a 50% or higher chance of success, so one should aim to keep their project goal below this. There were some instances of campaigns with goals between 35000 and 45000 where the campaigns had a 67% success rate but there are minimal data points for this so I cannot say with confidence that this is accurate. 

    A chart of Outcomes based on goals can be seen below


![Outcomes_VS_Goals](https://user-images.githubusercontent.com/57120024/156238479-b29f1eda-0cd6-41f5-a289-d7dad973d9e6.png)

#### Figure 2: Outcomes VS Goals


- What are some limitations of this dataset?

    The data set just looks are raw numbers and does not consider any more information about each campaign. There are many other factors that can weight on the success of a fundraising camping, such as the people involved, director, actors, etc. Location of campaign is also not considered. Along with location the campaign goals are in different currencies, they were not converted to a common currency, such a US dollar, when the analysis was conducted due to the complexity of conversion rates and inflation to find current date equivalence. 

- What are some other possible tables and/or graphs that we could create?

     There many other possible tables and graphs I could have created. First, I would have looked at further filtering to just which country Louise is in and to the subcategory of plays for outcome by launch date. This would give us a better picture of how her campaign compared to others since there are many differences between countries and types of theater productions.

     Another factor not considered is the length of the campaign. The raw data gives us launch date and deadline. I see the length of the campaign as just as important as the launch date. So, we could create a graph of "Outcome by Campaign Length" and even "Outcome by Campaign Finish Month".
