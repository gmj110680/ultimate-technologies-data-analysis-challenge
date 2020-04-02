## Ultimate Technologies Data Analysis Take-Home Interview Challenge
As part of my coursework for Springboard, I was tasked with completing a mock take-home interview assignment from a ficticious ride-share company, Ultimate Technologies, Inc.  The challenge consisted of three parts, which are laid about below in full along with summaries of my answers/conclusions for each part.

You can access and review a more detailed explanation of my analysis, along with the source code, [here](https://github.com/gmj110680/ultimate-technologies-data-analysis-challenge/blob/master/Ultimate_Technologies_Data_Analysis_Interview_Challenge_Solution.ipynb).  I also have included in this repository the narrative questions and the two .csv files containing the data needed to complete this challenge.

### Part I - Exploratory Data Analysis
The logins.json file contains (simulated) timestamps of user logins in a particular geographic location. Aggregate these login counts based on 15-minute time intervals, and visualize and describe the resulting time series of login counts in ways that best characterize the underlying patterns of the demand. Please report/illustrate important features of the demand, such as daily cycles. If there are data quality issues, please report them.

### Part 1 Answer
Based on some data exploration and visualization, I concluded that the demand for Ultimate's services peaked daily during the lunchtime hours, the dinnertime hours, and latenight hours when people are returning home from the nightlife scene.  I also determined that the demand for Ultimate's services were lowest on Monday and gradually increased throughout the week with the greatest demand on the weekend.  Finally, there appeared to be a seasonal increase in demand for Ultimate's services as the weather warmed up.

### Part 2 - Experiment and Metrics Design
The neighboring cities of Gotham and Metropolis have complementary circadian rhythms: on weekdays, Ultimate Gotham is most active at night, and Ultimate Metropolis is most active during the day. On weekends, there is reasonable activity in both cities.

However, a toll bridge, with a two-way toll, between the two cities causes driver partners to tend to be exclusive to each city. The Ultimate managers of city operations for the two cities have proposed an experiment to encourage driver partners to be available in both cities, by reimbursing all toll costs.

#### Part 2 Question 1
What would you choose as the key measure of success of this experiment in encouraging driver partners to serve both cities, and why would you choose this metric?

#### Part 2 Question 1 Answer
Determining the key measure of success largely is dependent upon the client's ultimate goal. Here, I am provided with only a limited description stating that Ultimate desires "to encourage driver partners to be available in both cities." The most likely scenario is that Ultimate currently is experiencing issues with a disproportionate number of partner drivers servicing one city over another at particular times (most likely Metropolis during weekdays and Gotham during weeknights due to demand).

Given this understanding, the likely best metric to measure driver availability throughout both cities is customer wait time within the region. If the driver partners are all making themselves available in both cities at all times, then that should result in a more even geographical distribution of available drivers and, hence, less time on average for customers in the region to have to wait for the closest available driver. So, I would measure the average customer wait time within a particular unit of time to observe whether the experiment successfully reduces that metric. This would be particularly appealing because the wait time for each customer transaction can easily be measured and recorded accurately.

If Ultimate prioritizes profitability, however, I would use overall profitability (with consideration of the extra toll reimbursement costs) within a particular unit of time. The success of the experiment would be measured by whether Ultimate's profitability increased during the time periods when it was reimbursing tolls to its drivers. This may not be the best metric to evaluate the experiement given that we know that the particular demands in each city are unequal during certain days/times, meaning that an even distribution of drivers between the two cities during those time periods may not maximize profits for the company.

Finally, Ultimate could try to use the geo-location capabilities of its drivers' smartphones to periodically report each driver's specific location during a shift. While this would report directly relevant data, it likely would not be comprehensive given that it would likely get compliance pushback from drivers complaining about privacy concerns and the intrusive nature of tracking that data. I therefore would not recommend using this metric.

#### Part 2 Question 2
Describe a practical experiment you would design to compare the effectiveness of the proposed change in relation to the key measure of success. Please provide details on:
a. how you will implement the experiment;
b. what statistical test(s) you will conduct to verify the significance of the observation; and
c. how you would interpret the results and provide recommendations to the city operations team along with any caveats.

#### Part 2 Question 2 Answer
To test the effectiveness of reimbursing all toll costs for drivers, I would set up a time period (preferably 6 months or longer to collect a large sample of data) where I would alternate between periods (likely on a weekly basis) when Ultimate did reimburse and did not reimburse its drivers for tolls incurred. I would record the wait time for each customer request during this time period.

Once enough data has been collected, I would generate bootstrap samples with replacement for both datasets (the wait times when drivers were receiving toll reimbursements data and the wait times when drivers were not receiving toll reimbursements data) and calculate a distribution of the average wait times for both datasets over that time period. I would then conduct a traditional hypothesis test with the null hypothesis being that the difference between the average wait time distributions of the two datasets is caused by random chance. I would plot the average wait time distributions for both datasets and evaluate how much of the average wait time distribution for reimbursed tolls dataset falls outside of the 95% confidence interval of the average weight time distribution for the non-reimbursed tolls dataset (assuming the use of a standard p-value of 0.05 to measure significance). I would then be able to determine how likely it is that reimbursing tolls to drivers significantly impacted (postively or negatively) the average weight time for customers.

When interpreting the results, I would not only analyze the overall average wait times for the entire region, but also how the average wait times were impacted within each city. In particular, I would analyze the weekday and weeknight results for each of the cities because we know that the demands for rides fluctuates during the week (with Metropolis being more active during the day and Gotham more active at night). I would want to see if the average wait time in Metropolis during weeknights and the average wait time in Gotham during weekdays decreased, as those numbers in particular may be an indication that reimbursing tolls is incentivizing the partner drivers to service those areas despite the lower demand. I would also want to observe whether the average wait time in Metropolis during the weekdays and the average wait time in Gotham during the weeknights has not increased significantly, as that could lead to overall lower customer satisfaction since the demand in those cities during those time periods is higher. These concerns aren't as prevalent over the weekend when the relative demand between the cities is more equal.

As for recommendations, I would inform Ultimate that overall the toll reimbursement experiment is working if it results in a reduction in the average customer wait time during those time periods. I would certainly include in my recommendations a specific discussion of the weekday and weeknight time periods where the relative demands between the two cities are uneven and the potential risks in trying to encourage drivers to be available in both cities during those time periods (e.g., decreased customer satisfaction, decreased revenue). The degree to which this would impact my recommendations, however, would depend on the results of the experiment.

### Part 3 - Predictive Modeling¶
Ultimate is interested in predicting rider retention. To help explore this question, we have provided a sample dataset of a cohort of users who signed up for an Ultimate account in January 2014. The data was pulled several months later; we consider a user retained if they were “active” (i.e. took a trip) in the preceding 30 days.

We would like you to use this data set to help understand what factors are the best predictors for retention, and offer suggestions to operationalize those insights to help Ultimate. The data is in the attached file ultimate_data_challenge.json. See below for a detailed description of the dataset. Please include any code you wrote for the analysis and delete the dataset when you have finished with the challenge.

1. Perform any cleaning, exploratory analysis, and/or visualizations to use the provided data for this analysis (a few sentences/plots describing your approach will suffice). What fraction of the observed users were retained?

2. Build a predictive model to help Ultimate determine whether or not a user will be active in their 6th month on the system. Discuss why you chose your approach, what alternatives you considered, and any concerns you have. How valid is your model? Include any key indicators of model performance.

3. Briefly discuss how Ultimate might leverage the insights gained from the model to improve its long-term rider retention (again, a few sentences will suffice).

*Data Description*
-  city: city this user signed up in
-  phone: primary device for this user
-  signup_date: date of account registration; in the form ‘YYYYMMDD’
-  last_trip_date: the last time this user completed a trip; in the form ‘YYYYMMDD’
-  avg_dist: the average distance in miles per trip taken in the first 30 days after signup
-  avg_rating_by_driver: the rider’s average rating over all of their trips
-  avg_rating_of_driver: the rider’s average rating of their drivers over all of their trips
-  surge_pct: the percent of trips taken with surge multiplier > 1
-  avg_surge: The average surge multiplier over all of this user’s trips
-  trips_in_first_30_days: the number of trips this user took in the first 30 days after signing up
-  ultimate_black_user: TRUE if the user took an Ultimate Black in their first 30 days; FALSE otherwise
-  weekday_pct: the percent of the user’s trips occurring during a weekday

### Part 3 Answer
Ultimate's goal is to improve its long-term rider retention, which I attempted to measure through the 'active' user metric. Based on my exploratory data analysis and model performance, it appears that the factors (of the factors I analyzed) that most often lead to a long-term rider are high volume usage during the first month of signing up, short trip distances, and using the ultimate black car service (especially during peak demand times when surge pricing applies). I therefore would recommend that Ultimate consider promotions that incentivize such behavior, such as offering discounted pricing (1) for new users, (2) for trips under a certain distance, and (3) for ultimate black car trips during the surge pricing periods when demand is high.
