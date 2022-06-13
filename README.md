# Data Science Guided Capstone

Hello students!
Welcome to the Data Science Guided Capstone! 

## Getting Started

Start by forking this repository to your personal GitHub account and cloning the fork to your local machine. 

**Note**: If forking and cloning a repo is new to you and/or github is new to you then it is strongly suggested to use [GitHub desktop](https://desktop.github.com/) and follow instructions in the docs [here](https://docs.github.com/en/free-pro-team@latest/desktop/contributing-and-collaborating-using-github-desktop/cloning-and-forking-repositories-from-github-desktop).

From https://github.com/springboard-curriculum/DataScienceGuidedCapstone press the green "code" dropdown and then press "Open with GitHub Desktop". This will fork the springboard repository into your own github account and then clone that fork to your local machine - it is in here that you will do your work and push your changes back to your fork of the repo in your own github account. 

You will find the notebooks in the Notebooks/ directory. 

You will find instructions on how to complete and submit each step of the Guided Capstone in the course materials. Each subunit will focus on one step of the Capstone, corresponding to a step of the Data Science Method. Find the Jupyter Notebook corresponding to the subunit you are working on, and open it. Follow along as you are guided through the work, and fill in the blanks!

When you are done with the notebook, push the changes to your personal GitHub account.

## Pipenv

The `Pipefile` has all the python dependencies and requirements you should need. So you can use [Pipenv](https://pipenv-fork.readthedocs.io/en/latest/) if you want to create a seperate python environment for this project. 

To install pipenv see [here](https://pipenv-fork.readthedocs.io/en/latest/#install-pipenv-today).

To create the env and install the required libraries (once you have pipenv installed) you can just do:
```
pipenv install
```

Then to activate the env and launch jupyter from this env you can do something like the below two commands:
```
pipenv shell
jupyter lab
```
## Data Science Problem
The purpose of this data science project is to come up with a pricing model for ski resort tickets in our market segment. Big Mountain ski resort suspects it may not be maximizing its returns, relative to its position in the market. It also does not have a strong sense of what facilities matter most to visitors, particularly which ones they're most likely to pay more for. This project aims to build a predictive model for ticket price based on a number of facilities, or properties, boasted by resorts (at the resorts). This model will be used to provide guidance for Big Mountain's pricing and future facility investment plans.
## Data Wrangling
### Raw Data
After importing the raw data in `ski_resort_data.csv`, we determine the following response variables: `AdultWeekday` is the price of an adult weekday ticket, and `AdultWeekend` is the price of an adult weekend ticket. The other columns are potential features. Below we show the record for our ski resort.

| Name |	Big Mountain Resort |
| ---- | --- |
| Region |	Montana |
| state |	Montana |
| summit_elev |	6817 |
| vertical_drop | 2353 |
| base_elev | 4464 |
| trams |	0 |
| fastEight | 0 |
| fastSixes |	0 |
| fastQuads |	3 |
| quad |	2 |
| triple | 6 |
| double | 0 |
| surface | 3 |
| total_chairs | 14 |
| Runs | 105 |
| TerrainParks | 4 |
| LongestRun_mi |	3.3 |
| SkiableTerrain_ac |	3000 |
| Snow Making_ac |	600 |
| daysOpenLastYear |	123 |
| yearsOpen |	72 |
| averageSnowfall |	333 |
| AdultWeekday |	81 |
| AdultWeekend |	81 |
| projectedDaysOpen |	123 |
| NightSkiing_ac | 	600 |

`fastEight` has the most missing values, at just over 50%. Unfortunately, you see you're also missing quite a few of your desired target quantity, the ticket price, which is missing 15-16% of values. `AdultWeekday` is missing in a few more records than `AdultWeekend`. What overlap is there in these missing values? This is a question you'll want to investigate. You should also point out that `isnull()` is not the only indicator of missing data. Sometimes 'missingness' can be encoded, perhaps by a -1 or 999. Such values are typically chosen because they are "obviously" not genuine values.

Inspection of categorical variables shows there are two 'Crystal Mountain' resorts, but they are clearly two different resorts in two different states. This is a powerful signal that you have unique records on each row.

What's the relationship between region and state? `Region` has some non-state names such as Sierra Nevada, Salt Lake City, and Northern California. The vast majority of the differences are in California, with most Regions being called Sierra Nevada and just one referred to as Northern California.

How's your geography? Looking at the distribution of States, you see New York accounting for the majority of resorts. Our target resort is in Montana, which comes in at 13th place. You should think carefully about how, or whether, you use this information. Does New York command a premium because of its proximity to population? Even if a resort's State were a useful predictor of ticket price, your main interest lies in Montana. Would you want a model that is skewed for accuracy by New York? Should you just filter for Montana and create a Montana-specific model? This would slash your available data volume. Your problem task includes the contextual insight that the data are for resorts all belonging to the same market share. This suggests one might expect prices to be similar amongst them. You can look into this. A boxplot grouped by State is an ideal way to quickly compare prices. Another side note worth bringing up here is that, in reality, the best approach here definitely would include consulting with the client or other domain expert. They might know of good reasons for treating states equivalently or differently. The data scientist is rarely the final arbiter of such a decision. But here, you'll see if we can find any supporting evidence for treating states the same or differently.
