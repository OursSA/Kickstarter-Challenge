# Kickstarting with Excel - Goals and Launch Date

## Overview of Project

### Purpose

This analysis was undertaken to understand the likelihood of success for a new play, "Fever," to reach its crowdfunding goals.
To do this, data was gathered regarding Kickstarter projects from the years 2009-2017.
By filtering the data to include only theater projects, it became possible to observe trends in when successful campaigns tended to launch, and what goal amounts of funding tended to be succesfully raised.
The objective is to identify what launch window and funding goal would contribute to the chances of a successful campaign.

## Analysis and Challenges

### Analysis of Outcomes Based on Launch Date

First, the data in the launched_at column was converted to readable dd/mm/yyyy format using division and Excel's built-in formatting menu.
For example, the code for row 2 was =(J2/(60*60*24))+DATE(1970,1,1)
The "category and subcategory" column was split into a separate parent category and subcategory, using the slash in each entry as a separator, using "text to columns."
Then, the newly converted dates were used in the creation of the pivot table seen in [this screenshot.](MonthlyAnalysis.png)
Filtering by Parent Category in the drop menu alllowed the chart to display just the relevant "theater" category, with the count of each outcome serving as the column label and the month of creation defining the rows.
This resulted in the following [Chart of outcomes based on launch date.](Theater_Outcomes_vs_Launch.png)

### Analysis of Outcomes Based on Goals

Because the subcategories had already been split from the parent categories in the creation of the previous table, it was now possible to identify kickstarters for plays specifically using the "subcategory" column.
From there, a new sheet was created. As shown in [this screenshot,](Goalstable.png) the goal categories were entered manually based on the outline in the challenge document.
It then became necessary to reference the original Kickstarter sheet in a series of COUNTIFS functions to determine how many projects in each range succeeded, failed, or were canceled.
For example, the counting for the $1000 to $4999 bin was done using the command =COUNTIFS(Kickstarter!F:F,"successful",Kickstarter!R:R,"plays",Kickstarter!D:D,">=1000",Kickstarter!D:D,"<=4999"). In subsequent columns, the word "successful" was swapped out to the corresponding column label.
Then, the total number of projects in each range was calculated using the SUM command, such as =SUM(B3:D3)
This allowed for the percentage of successful projects in each bin to be calculated using division, along with Excel's percentage format. For example, =ROUND(B3/$E3,2) gave the percentage of projects with goals between $1000 and $4999 that succeeded.
Lastly, the percentages were then plotted on a line graph using Excel's chart editor.
The end result was this [Chart of outcomes based on goals.](Outcomes_vs_Goals.png)

### Challenges and Difficulties Encountered

The primary challenges involved in this analysis related to selecting the proper subsets of the original data set. 
In the case of the launch date data, configuring the pivot table to include years as a filter while allowing rows to represent months took a fair bit of tinkering.
When working with the goal amounts, it became tedious to make the slight alterations needed in the "countifs" call to reflect the different dollar amounts each step of the way.
In retrospect, some of the latter difficulty could possibly have been alleviated by storing the key values in cells, then referencing them by their locations so that dragging the formula could automate some of the changes.

## Results

- What are two conclusions you can draw about the Outcomes based on Launch Date?

See the following [Chart of outcomes based on launch date](main/Theater_Outcomes_vs_Launch.png)

In general, the greatest number of campaigns tended to launch in May and June. These were also the months with the highest success rate.
The rate of successful campaigns trends downward toward the autumn and winter months, with December launches seeming particularly unlikely to be successful.
The number of canceled campaigns remains quite low compared to those that are completed throughout the year, but there is a small uptick in canceled campaigns in January.

- What can you conclude about the Outcomes based on Goals?

See the following [Chart of outcomes based on goals.](Outcomes_vs_Goals.png)
This chart shows the relative success of campaings in the "plays" subcategory, based on the amount of funding set as the campaign goal.
Plays with lower goals, under $5000, were successful at a rate of over 70%. This rate declined sharply after the $5000 mark.
Plays with goals in the $15000 to $19999 were about as likely to succeed as they were to fail; beyond this point, failures became more common.
Success became more common than failure again once goals were between $35000 and $45000, but this is likely an effect of small sample size. There were only 6 plays with goals between $35000 and $39999, and a further 3 plays with goals between $40000 and $45999.

- What are some limitations of this dataset?

The data only include campaigns from the Kickstarter platform, excluding other possible crowdfunding sources.
No campaigns from years more recent than 2017 are represented, so any recent changes in the trends noticed here are not shown.
The outcomes vs goals graph only had a few entries with goals of greater than $25000 to draw from, so the trends may not be as predictive for campaigns with higher goals.

- What are some other possible tables and/or graphs that we could create?

It may be beneficial to use an additional pivot chart to compare the success rate of projects that were given the "staff pick" and "spotlight" status versus those that were not. This could perhaps take the form of a stacked bar graph.
Using subtraction on the launch dates and deadlines, it would be possible to categorize the campaigns based on the amount of time they were active, so that a line graph could be used to look for any effects of a longer active period.
