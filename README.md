#Udacity Student A/B Test Project

##Experiment Design

###Metric Choice

**Invariant Metrics:** number of cookies, number of clicks, click-through-probability

**Evaluation Metrics:** gross conversion, net conversion

####Invariant Metrics

**Number of cookies:** This metric is the number of cookies expected to view the course overview page. This metric is a strong invariant metric and a weak evaluation metric because it measures how many cookies get to the course overview page before the experiment is presented to them. I would expect this metric to be equally distributed between control and experiment groups and not have an effect on the experiment itself.

**Number of user-ids:** This metric is the number of users who enroll in the free-trial. This is not a good invariant metric because it is dependent on the experiment. It is also not a strong evaluation metric because the metric amount could be different between control and experiment groups, which would then skew the results of the experiment one way or the other.  

**Number of clicks:** This metric is the number of users that click the “Start Free-Trial” button, which happens before the experiment window is shown to the user. Since this metric is tracked before the experiment actually occurs, so it should not be used as an evaluation metric. I would expect the experiment and control groups to be equally distributed and not affect the experiment itself because the experience is the same for all users.

**Click-through-probability:** This metric is defined by dividing the number of unique cookies that click the “Start Free-Trial” page by the number of unique cookies that view the course overview page. This is a good invariant metric because it is defined when the experience should be the same for all users and not affect the experiment. I would also expect this metric to be evenly distributed between control and experiment groups.

####Evaluation Metrics

**Gross conversion:** This metric is defined by the number of user-ids that checkout and enroll in the free trial divided by the number of unique cookies that click the “Start Free-Trial” button. Since this metric is measured after users have seen the experiment, it is directly affected by it, which makes it a strong evaluation metric and vice versa as an invariant metric. I would not expect the control and experiment groups for this metric to be evenly distributed.

**Retention:** This metric is defined as the number of user-ids that stay enrolled passed the free-trial period divided by the number of cookies that clicked on the "Start Free-Trial" button. This is not a strong invariant metric since it is dependent on the experiment. It is a strong evaluation metric, however based on the experiment duration needed for this metric, I decided not to use it. I calculated that I would need to run the experiment for 119 days to match the amount of pageviews required for this metric (4,741,213 pageviews), which in my opinion, is too long to be justifiable.

**Net conversion:** This metric is defined by the number of user-ids that remained enrolled after the 14-day free-trial period divided by the number of cookies that click the “Start Free-Trial” button. Since this metric is correlated to the impact of the experiment being run, it is a strong evaluation metric, and a weak invariant metric, since it will most likely change based on the experiment. I would not expect either the control and experiment groups to be evenly distributed for this metric either.

To justify launching the experiment, both gross conversion and net conversion will need to be satisfied. Gross conversion will need to decrease and net conversion will need to increase. This will show that the number of users signing up for the free-trial is decreasing, but the number of users continuing past the free-trial increases.

###Measuring Standard Deviation

The baseline metrics I used for calculating the standard deviations below can be found in this [Google spreadsheet](https://docs.google.com/spreadsheets/d/1MYNUtC47Pg8hdoCjOXaHqF-thheGpUshrFA21BAJnNc/edit#gid=0).

| Metric | Standard Deviation |
| ------ | ------------------ |
| Gross conversion: | .0202 |
| Net conversion: | .0156 |

I expect the analytic and empirical variability to be similar for both of the evaluation metrics I chose. This is because analytical and empirical variability tend to be similar when the unit of diversion is the same as the unit of analysis. Both evaluation metrics I used have unique cookies as their unit of diversion and unit of analysis, thus their empirical and analytical variability should be similar.

###Sizing

####Number of Samples vs. Power
I did not use the Bonferroni correction during my analysis phase. The number of pageviews needed for my experiment is 685,325.

####Duration vs. Exposure
I chose to divert 85% of Udacity’s traffic for this experiment, which would require a 21 day duration for the experiment.

I chose to divert 85% of traffic because I thought this experiment is a relatively low risk for Udacity. From a high-level, the experiment only adds a small step in between users clicking on the “Start Free-Trial” button and actually starting their free-trial. However, to be safe I decided leave a small portion of the site’s traffic out of the experiment in case something were to go wrong, such as experiment bugs. This only increased the duration of the experiment by about 3 days, which I thought was justifiable.

##Experiment Analysis

The data for each group I used to calculate the information below can be found in this [Google spreadsheet](https://docs.google.com/spreadsheets/d/1Mu5u9GrybDdska-ljPXyBjTpdZIUev_6i7t4LRDfXM8/edit#gid=0).

###Sanity Checks

| Invariant Metric | Lower Bound | Upper Bound | Observed Value | Pass? |
| ---------------- | ----------- | ----------- | -------------- | ----- |
| Number of Cookies | 0.4988 |  0.5012 |  0.5006 | Yes |
| Number of clicks on “Start Free-Trial” button | 0.4959 | 0.5042 | 0.5005 | Yes |
| Click-through probability on “Start Free-Trial” button | 0.0812 | 0.0830 | 0.0822 | Yes |

###Result Analysis

####Effect Size Tests

| Evaluation Metric | Lower Bound | Upper Bound | Statistically Significant? | Practically Significant? |
| ----------------- | ----------- | ----------- | -------------------------- | ------------------------ |
| Gross Conversion | -0.0291 | -0.012 | Yes | Yes |
| Net Conversion | -0.0116 | 0.0019 | No | No |

####Sign Tests

| Evaluation Metric | P-Value | Statistically Significant? |
| ----------------- | ------- | -------------------------- |
| Gross Conversion | 0.0026 | Yes |
| Net Conversion | 0.6676 | No |

####Summary

I did not use the Bonferroni correction in my analysis for the following reasons.

  1. I thought my evaluation metrics would be correlated with one another, and the Bonferroni correction would be too conservative and possibly lead to not launching the experiment.
  2. Since all of my evaluation metrics must be satisfied to launch, the experiment is more prone to decisions based on false negative results. The Bonferroni correction is used to control false positives when using multiple metrics, which means the experiment results could be more prone to false negative results. Thus, it did not make sense to use this correction for this experiment.

####Recommendation

Since the requirements to launch this experiment were for both evaluation metrics being satisfied, I cannot recommend launching it. Gross conversion saw a statistically and practically significant decrease, but net conversion did not see a significant difference in either. I recommend running another experiment to gather more information on student’s frustration with the free trial program.

##Follow-Up Experiment

A possible follow-up experiment could be created to further address credentials pre-enrollment and also add an element post-enrollment to help students through their 14-day trial period.

Pre-enrollment, I feel that additional questions should be asked about a person’s credentials and background before recommending they enroll in the free-trial period. For example, some nanodegrees may require more programming and mathematical background than others. For those with heavier influence on those disciplines, ask the users about their background in them and then have them take a short quiz to quantify their backgrounds. If they do not pass the quiz, suggest they take a Udacity class that provides them background in the field they need to work on for free. If they do pass, they can enroll in the free-trial period.

The pre-enrollment experiment would be setup as follows with the following metrics.

**Design:** Users are either diverted into the experiment group, which completes the pre-requisites, or the control group, which is not filtered and enrolls in the free-trial normally.

**Null Hypothesis:** The additional pre-requisite measures will not increase the number of students that continue on past the free-trial period by the statistically significant difference defined.

**Unit of Diversion:** Similarly to how the original experiment was set up, the unit of diversion would be a unique cookie, and then user-id after a user enrolls in the free-trial period.

**Invariant Metrics:** These would be the same as the original experiment.

**Evaluation Metrics:** These would also be the same as the original experiment.

Post-enrollment, I think there could be a possibility to help users also. Udacity offers 1 on 1 coaching meetings, however meeting with students in the same fashion could be beneficial. If a user is feeling frustrated or stuck on a particular problem during their free-trial period, they could jump into a conversation with multiple other students that may be experiencing the same problem, and help one another through it. This may help students that don’t feel comfortable talking to coaches at first, but also gives them someone that’s comparable to them to talk with, which could also increase cross-student communication and engagement.

The post-enrollment experiment would be setup as follows.

**Design:** Users are either diverted into the experiment group, which has the ability to communicate interactively with other students or the control group, which works through the free-trial normally.

**Null Hypothesis:** The student collaboration functionality will not increase the number of students that continue on past the free-trial period by the statistically significant difference defined.

**Unit of Diversion:** The unit of diversion for this test would be user-id since the experiment occurs after the user already enrolls and has created an account.

**Invariant Metrics:** User-id would be the invariant metric because one could expect users to be equally divided between control and experiment groups.

**Evaluation Metrics:** Retention would be the evaluation metric because it measures what percentage of users stay enrolled past the free-trial period.
