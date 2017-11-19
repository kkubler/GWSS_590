# GWSS_590
Class Project

# Introduction
Joy Buolamwini, in her TED talk on algorithmic bias, mentions how fast bias can spread online. In the wake of Milo Yiannopoulus's speaking tour last year, one of the critiques I kept hearing about the counter-protesters is that they "burned shit, knocked people unconscious, and hit women". This separation between people and women seemed to spread quickly as a way to admonish those that protested Milo's talks. Below is an attempt to map the spread of this phrase through the internet. 
Although the origins of this story can most likely associated with Kiara Robles being hit with a flag pole, this project focuses less on the origins of the story and more on its evolution.

# Methods
Without the use of keyword or text scraping software, the data collection for this project was simply done through google searches. As a result of this the data set I am using for analysis is by no means complete, but rather a hopefully insightful snapshot.

## Summary Table
```{r df table, cache=TRUE, include=FALSE}
Digital_Object_Dataset_Sheet1 %>% 
  select(Website, Date, `News Type`, Comments, Shares) %>% 
  pander()
```

# Results

The first visualization is a timeline showing when each news article was published. For articles that span the entire day, no specific time of publication was available. This type of visualization highlights the speed at which objects, images, and phrases move throughout the internet. 
```{r timevis, cache=TRUE, include=FALSE}
library(timevis)
#manipulate data for timeline visualization
data.timevis <- data.frame(
  id = 1:11,
  content = c("USA Today College", 
              "KTLA 5", 
              "The American Mirror", 
              "Breitbart", 
              "NBC Bay Area", 
              "The Daily Caller", 
              "CNN", 
              "The Washington Times",
              "Information Liberation",
              "Russia Today",
              "ABC 7 News"),
  start = c("2017-02-01 22:55:00", #these datapoints have a specific publication time
            "2017-02-02 19:34:00", 
            "2017-02-01", #these do not
            "2017-02-01", 
            "2017-02-02 16:31:00", 
            "2017-02-02 2:17:00",
            "2017-02-02", 
            "2017-02-02",
            "2017-02-02",
            "2017-02-02 16:17:00",
            "2017-02-03"),
  end = c(NA, 
          NA,
          "2017-02-02", #The data points that have ranged throughout the entire day of publication have no publish time.
          "2017-02-02",
          NA,
          NA,
          "2017-02-03",
          "2017-02-03",
          "2017-02-03",
          NA,
          "2017-02-04")
)
timevis(data.timevis)
```
*For this timeline visualization I used the timevis code written by Dean Attali.

The next two graphs focus on the overall impact of the selected articles. In this case, impact is measured by total number of comments on and shares of the articles. Since both comments and shares were not available for all the articles in the dataset, usng both of those variables to represent impact helps fill in some of the gaps in the data.

Make sure you get rid of cluttered x axis
```{r comments graph, cache=TRUE, include=FALSE}

com_graph <- Digital_Object_Dataset_Sheet1 %>% 
  select(Website, Comments, `News Type`)

com_graph %>%
  na.omit() %>% 
  ggplot(aes(x=Website, y=Comments, fill = `News Type`, size = 5)) + 
  geom_bar(stat = "identity") +
  theme_bw()
  
```
