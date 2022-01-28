---
layout: post
title: Box Office Data Visualization Lab
subtitle: Free POPCORN if you read my lab!
cover-img: /assets/img/films.jpg
tags: [labs, data]
author: Jack Komaroff
---
**By Jack Komaroff**

## My Code

The following is my *Data_Vis_lab.ipynb* file which contains the code that I used to answer the lab questions and generate the graphs.

```py
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt

ratings = pd.read_csv("../Datasets/HighestGrossers - Copy.csv")
sns.boxplot(data=ratings[ratings["MPAA RATING"] =="PG-13"], x="MPAA RATING", y="TOTAL IN 2019 DOLLARS (in 100 millions)", palette="Greens")

sources = pd.read_csv("../Datasets/HighestGrossers - Copy.csv")
sns.set(font_scale = 0.7)
sns.lineplot(data=sources, x=sources["YEAR"],y=sources["TOTAL IN 2019 DOLLARS (in 100 Million $)"],palette="Reds")

sources = pd.read_csv("../Datasets/WideReleasesCount.csv")
sns.set(font_scale = 0.7)
sns.lineplot(data=sources, x=sources["YEAR"],y=sources["TOTAL MAJOR 6"],palette="Reds")

sources = pd.read_csv("../Datasets/WideReleasesCount.csv")
sns.set(font_scale = 0.7)
sns.lineplot(data=sources, x=sources["YEAR"],y=sources["TOTAL OTHER STUDIOS"],palette="Reds")

grossers = pd.read_csv("../Datasets/TopDistributors.csv")
sns.set(font_scale = 0.55)
sns.barplot(data=grossers, x=grossers["DISTRIBUTORS"],y=grossers["AVERAGE GROSS (IN 10 Million $)"])


```
## Analysis

As a film-lover, I wanted to take a look at a popular film finance dataset. This kaggle dataset was actually multiple datasets in one, but I decided to focus on the dataset that described the highest grossing films of the last 25 years. I also decided that looking at the distribution of films by different major studios (and indie studios) might be a fruitful way to explore how much of Hollywood is controlled by the big 6 studios (Disney, Sony, Paramount, Universal, Warner Bros, and 20th Century Fox). 

Starting off with the wide releases distribution dataset, I looked at the trend of how many films were the big 6 releasing compared to the indie studios. Both of these graphs looked at the year on the X-Axis and the number of films released on the Y-Axis .  As you can see, the indie studios are generally increasing the number of films that they release every year. When looking at the major studios, they appear to be generally decreasing the amount of films that they release, presumably as their smaller films move to that studios streaming service and the blockbuster landscape becomes more competitive. Big studios want to "eventize" their films and with less of them on the theatrical calendar, that becomes easier. Whereas indie studios are clearly ramping up their releases to reach more demographics with different types of films in order to make enough money to stay afloat in this competitive landscape. 

[Major 6 Studios - # of Releases](https://drive.google.com/file/d/1clbdifbR3BCEylMLiskZg4mfz8F5qhxr/view?usp=sharing/)

[Indie Studios - # of Releases](https://drive.google.com/file/d/1OV7Y3R83rWadAMnSdQryeuriKiT7KkVc/view?usp=sharing/)

Additionally, I looked at a dataset that showed the average gross for a particular studios’ film. I then created a bar graph that had the studio name on the X-Axis and the average gross in 10 million dollars on the Y-Axis. This showed, as we might expect, that the big players like Disney and Universal are producing consistent hits and other studios are struggling. Interestingly, Dreamworks is averaging similar box office numbers to the other top studios. This is due to less frequent, but consistently high performing films, as opposed to the generally high performing films of Disney that are released far more often.

[Distributor - Avg Film BO](https://drive.google.com/file/d/1qhcg8Y01y1cO9chLV1xkFb2gSBNV10E-/view?usp=sharing/)

For the final dataset, I looked at the highest grossing films of each year (for 25 years). One graph that I wanted to create was a line graph of the box office of each of these films to see the state of the theatrical experience in the 21st century. This graph tells us that, naturally, moviegoers come out in cycles. Every few years there is a megahit Marvel or Star Wars film that brings everyone to the cineplex, but otherwise the box office numbers are at consistent levels.

[BO of the highest grossing film by year](https://drive.google.com/file/d/1fk5EPiYpivyjyI_AMNiH3ZPiAQ6AkZgy/view?usp=sharing/)

With more of these megahits coming out every year, the time between bumps is decreasing, and the graph is trending upwards. 
With this dataset, I also wanted to look at where most of the top performing films (that are usually PG-13) fit in terms of box office revenue. For this question, I used a box plot to determine that IQR for these high performing PG-13 films was around $450,000,00 to $700,000,000. This number is a great benchmark for determining if a year was generally good for the box office. 

![BO of the top grossing films - Box Plot](https://github.com/jkom23/websiteAoD/blob/master/assets/img/boxplot.png?raw=true)
![[BO of the top grossing films - Box Plot2]]({{site.baseurl}}/assets/img/boxplot.png)

Looking at this datset more closely, we see these summary statistics. 
|       |        YEAR | TOTAL IN 2019 DOLLARS (in 100 millions)|
|------:|------------:|----------------------------------------:|
| count |   27.000000 |                            2.700000|
|  mean | 2008.000000 |                            5.537170|
|   std |    7.937254 |                            1.699856|
|   min | 1995.000000 |                            2.044178|
|   25% | 2001.500000 |                            4.544314|
|   50% | 2008.000000 |                            5.160503|
|   75% | 2014.500000 |                            6.641301|
|   max | 2021.000000 |                            8.658428|
The year column is obviously not important, but we see that the mean of these top grossing films is 5.54 hundred million dollars and the standard deviation is 1.70 hundred million.  This is the same data that we would see in the box plot, but it is illustrated very clearly in the table (instead of the general conclusions that the box plot provides).

For 2021, up until December, Shang-Chi was the leader of the domestic box office with around $225,000,000. This number is outside of the IQR for the highest performing film of the year, therefore demonstrating the poor state of the box office during the pandemic. However, when Spider-Man: No Way Home released in December, it became the highest grossing film of 2021 with around $720,000,000 (and counting). This is slightly above the IQR that we just calculated and this shows that the box office is back on track for 2022 and healthy compared to the past years’ data. 
The largest limitation of this analysis is my inexperience with seaborn and data visualization overall. We have just started learning to use this program so a lot of the more advanced analytical data tools are not yet known to me. With more practice with this software, I'm sure I could overlay lines, apply best fit curves, and other important features that could improve the quality of my data analysis. 

Thanks for reading!
