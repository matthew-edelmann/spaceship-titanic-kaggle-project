# spaceship-titanic-kaggle-project

## Overview

This is a Kaggle project found at this link [Kaggle](https://www.kaggle.com/competitions/spaceship-titanic). The summary of the project can be found here:

"Welcome to the year 2912, where your data science skills are needed to solve a cosmic mystery. We've received a transmission from four lightyears away and things aren't looking good.

The Spaceship Titanic was an interstellar passenger liner launched a month ago. With almost 13,000 passengers on board, the vessel set out on its maiden voyage transporting emigrants from our solar system to three newly habitable exoplanets orbiting nearby stars.

While rounding Alpha Centauri en route to its first destination—the torrid 55 Cancri E—the unwary Spaceship Titanic collided with a spacetime anomaly hidden within a dust cloud. Sadly, it met a similar fate as its namesake from 1000 years before. Though the ship stayed intact, almost half of the passengers were transported to an alternate dimension!

To help rescue crews and retrieve the lost passengers, you are challenged to predict which passengers were transported by the anomaly using records recovered from the spaceship’s damaged computer system.

Help save them and change history!"

The data sets were provided by the project.

## Cleaning the Data

The data was for the most part clean. For the training data, I just removed the null data. For the testing data, I replaced the null values with the columns average. The reason I made these decisions was that for the training data I wanted the most accurate model posible, so I didn't want to infer anything. Luckily, there wasn't too many deleted rows from this.

I wanted the same for the testing data. However, this wasn't posible as the assignment required that every passenger was accounted for. So, I made the missing values the average, as that seemed like the most accurate way of determining the correct outcome.

## EDA

Before actually making the model, I wanted to do some exploritory data analysis. The first place to start I figured was a heatmap. This heatmap is designed to find which variables best correlated with whether a passanger was transported or not.

![Alt text](./pics/heatmap.png)

The biggest indicator of weather the passenger was transported, according to our heat map, is if they had elected to be put into suspended animation during the voyage.

The next thing to look at are some count plots of different variable types to see if any effected the journey. Let's start with home planet. Some passangers started from Earth, others Europa, and the last group was from Mars. Here is what we found:

![Alt text](./pics/HomePlanet.png)

People from Europa were likely to be transported while people from Earth were not. People from Mars were in the middle.

Similar to how we have 3 home planets, we have 3 destinations. Here is how they effected transportation rates:

![Alt text](./pics/Destination.png)

The destination doesn't seem to make a difference if it is to PSO J318.5-22. There is a slight chance higher of not being transported if the destination is to Trappist-1e. One has a higher chance of being transported if the destination is 55 Cancri e.

Some people opted into doing the trip in cryo sleep. This is a form of frozen hibernation were the person is awaken once the trip is over. Here is how it effected the transportation rate:

![Alt text](./pics/CryoSleep.png)

What we found earlier in the heat map that participating in CryoSleep greatly increases the chance of being transported is confirmed here.

Some customers opted to be VIP guests on the Space Titanic. Let's see how that effected there chance of being transported:

![Alt text](./pics/VIP1.png)

Surprisingly, paying for a VIP service actually decreases ones chance of being transported.

I wanted to look at the age distribution of those who were transported and those who were not. I did this with a violin plot. Here is my finding:

![Alt text](./pics/Age_violin.png)

The most noticiable difference in these plots is that young people are more likely too be transported. Checking the averages, this is true by, on average, 2.4 years.

## Modeling and Analysis

Before even starting the modelling, we needed a baseline. The baseline is that if you chose either all 1s or all 0s, how accurate the model would be. Our goal is to be higher than the baseline. Our baseline in this case was 50.36%. So we needed to do better than this.

For this project, I decided to go for a logistic regression model using a train test split. This is because the result is either a 1 (transported) or a 0 (not transported). Choosing my variables, I simply went over my heat map and added more variables depending on how correlated they were with the transported column until the model didn't continue to improve. I also found that adding a 2 degree polynomial feature improved the model. The model I used took these perameters from the dataset:

**'CryoSleep', 'RoomService', 'Spa', 'VRDeck', 'Age', 'FoodCourt'**

With this, the model produced these scores for the training and testing split sets:

Training R2: 0.7803794913201454
Testing R2: 0.7790556900726392

This is a decent model that isn't over or under fit and accounts for around 78% of the variance in the data. This was the models coefficients:

array([[ 9.18393977e-09, -1.24950910e-06, -6.92130469e-07,
        -7.97614095e-07,  1.62854565e-07,  9.30539856e-07,
         9.18393977e-09,  0.00000000e+00,  0.00000000e+00,
         0.00000000e+00,  2.62113522e-07,  0.00000000e+00,
         4.37939060e-08,  2.52364393e-07,  1.78104179e-07,
        -4.09094225e-05, -4.59975390e-08, -6.25133463e-07,
         5.17632809e-07, -1.90320989e-05, -1.39082179e-07,
        -4.46156288e-07, -2.24725805e-05,  3.30706228e-08,
         5.92694223e-06,  3.11228954e-05, -2.45876277e-08]])
         
I simply then had to apply this model to our testing set to get our predictions and submit them to Kaggle.

## Conclusion

In conclusion, I was able to make a simple model that accounted for around 78% of the varience in the data. This model was better than our baseline in calculating whether or not a passanger was transported. 

With further analysis, perhaps we can find a more accuate way of filling in the null data to get better results. And also, perhaps using a more robust model would give better results.

Overall, this project was a success since it created a fairly accurate model of how to determine whether or not a passenger was transported. 

