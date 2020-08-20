# A/B testing to determine an effective intervention to decrease early Udacity course cancellation

This is the final project of [A/B testing course taught by Google](https://www.udacity.com/course/ab-testing--ud257). 

## Experiment Description
At the time of the experiment described herein, the Udacity course home pages have two options: "start free trial" and "access course materials." Clicking "start free trial" prompts the user to enter their credit card information, subsequently enrolling them in a 14 day free trial of the course, after which they are automatically charged. Users who click "access course materials" will be able to view course content but receive no coaching support, verified certificate, or project feedback.

For this experiment Udacity tested a change wherein those users who clicked "start free trial" were asked how much time they were willing to devote to the course. Users choosing 5 or more hours per week would be taken through the checkout process as usual. For users indicating fewer than 5 hours per week a message would appear indicating the need for a greater time commitment to enable success and suggesting they might like to access the free content. At this point the student would have the option to continue enrolling in the free trial or access the course materials for free.

This screenshot shows the experiment:
![Image](https://github.com/miayuxin/udacity-ab-testing/blob/master/Image/Experiment%20Screenshot.png)


## Experiment Design
The initial unit of diversion to the conrol and experiment groups is a unique cookie. However, once a student enrolls in the free trial, they are tracked by user-id. The same user-id can't enroll more than once. Users who don't enroll are not tracked by user-id. 

Note that the uniqueness of a cookie is determined per day.

### Metric Choice

#### Invariant Metrics

- #### Number of cookies: 
  The number of unique cookies to visit the course overview page. This is the unit of diversion and even distribution amongst the control and experiment groups is expected. It is therefore appropriate as an invariant metric.


- #### Number of clicks: 
  The number of users (tracked as unique cookies at this stage) to click the free trial buttion. This is appropriate as an invariant metric but not an evaluation metrice. Equal distribution amongst the experiment and control groups would be expected since at this point in the funnel the experience is the same for all users and therefore elements of the experiment would not be expected to impact clicking the "start free trial" button.

- #### Click-Through-Probability: 
  Unique cookies to click the "start free trial" button per unique cookies to view the course overview page. Equal distribution amongst the experiment and control groups would be expected since at this point in the funnel the experience is the same for all users and therefore elements of the experiment would not be expected to impact clicking the "start free trial" button.

#### Evaluation Metrics:

- #### Gross conversion: 
  This is the number of user-ids to complete checkout and enroll in the free trial per unique cookie to click the "start free trial"  button. Dmin = 0.01
  
- #### Retention:  
  This is the number of user-ids to remain enrolled past the 14 day trial period, making at least one payment, per number of user-ids to complete checkout. The practical minimum difference Dmin = 0.01
  
- #### Net conversion:
  
  This is the number of user-ids to remain enrolled past the 14 day trial, making at least one payment, per the number of unique cookies to click the "start free trial" button. dmin = 0.0075

## Measuring standard deviation

- Gross conversion:	0.0202

- Retention: 0.0549

- Net conversion: 0.0156


## Sizing

The calcations are based on the baseline conversion data, provided by Udacity. 

### Number of samples vs. power
Pageviews required for each metric were calculated using an alpha value of 0.05 and beta value of 0.2.

Pageviews for each evaluation metric to achieve target statistical power.

#### Gross Conversion

- Baseline conversion: 20.625%
- Minimum detectable Effect: 1%
- alpha: 5%
- beta: 20%
- 1 - beta: 80%
- Sample size = 25,835 enrollments/group
- Number of groups = 2 (experiment and control)
- Total sample size = 51,670 enrollments
- Clicks/pageview: 3200/40000 = 0.08 clicks/pageview
- Pageviews = 645,875

#### Retention

- Baseline conversion: 53%
- Minimum detectable effect: 1%
- alpha: 5%
- beta: 20%
- 1 - beta: 80%
- Sample size = 39,155 enrollments/group
- Number of groups = 2 (experiment and control)
- Total sample size = 78,230 enrollments
- Enrollments/pageview: 660/40000 = 0.0165 enrollments/pageview
- Pageviews = 78,230/.0165 = 4,741,212

#### Net conversion

- Baseline conversion: 10.9313%
- Minimum detectable effect: 0.75%
- alpha: 5%
- beta: 20%
- 1 - beta: 80%
- Sample size = 27,413 enrollments/group
- Number of groups = 2 (experiment and control)
- Total sample size = 54,826
- Clicks/pageview: 3200/40000 = 0.08 clicks/pageview
- Pageviews = 685,325

### *Pageviews required: 4,741,212*

## Experiment Analysis

The experimental data is provided by [Udacity](https://github.com/miayuxin/udacity-ab-testing/tree/master/Data), I will provide on my GitHub. 

### Sanity checks

For invariant metrics we expect equal diversion into the experiment and control group. We will test this at the 95% confidence interval.

![Image](https://github.com/miayuxin/udacity-ab-testing/blob/master/Image/Sanity%20check.png)

### Result analysis

95% Confidence interval for the difference between the experiment and control group for evaluation metrics.

![Image](https://github.com/miayuxin/udacity-ab-testing/blob/master/Image/Result.png)

### Sign test

![Image](https://github.com/miayuxin/udacity-ab-testing/blob/master/Image/Sign%20test.png)

## Conclusion 

At this point, once we have seen that the actual underlying goal we had was not reached (increase fraction of paying users by asking them in advance if they have the time to invest in the course), we can only recommend to not continue with change. It may have caused a change in Gross conversion, but it didn't for net conversion.


