# A/B-Testing
## Experiment Overview: Free Trial Screener

In the experiment, Udacity tested a change where if the student clicked "start free trial", they were asked how much time they had available to devote to the course. If the student indicated **5 or more hours per week**, they would be taken through the checkout process **as usual**. If they indicated **fewer than 5 hours per week**, a message would appear indicating that Udacity courses usually require a greater time commitment for successful completion, and **suggesting that the student might like to access the course materials** for free. At this point, the student would have the option to continue enrolling in the free trial, or access the course materials for free instead. This screenshot shows what the experiment looks like.

![Experiment Screenshot](https://github.com/mcgradyjason/AB-Testing/blob/master/Final%20Project-%20Experiment%20Screenshot.png)

The **hypothesis** was that this might set clearer expectations for students upfront, thus reducing the number of frustrated students who left the free trial because they didn't have enough time—**without significantly reducing the number of students** to continue past the free trial and eventually complete the course.


## Metric Choice
### Invariant Metrics

* Number of cookies: That is, number of unique cookies to view the course overview page. (dmin=3000)
* Number of clicks: That is, number of unique cookies to click the "Start free trial" button (which happens before the free trial screener is trigger). (dmin=240)
* Click-through-probability: That is, number of unique cookies to click the "Start free trial" button divided by number of unique cookies to view the course overview page. (dmin=0.01)

The choice of invariant metrics are listed above. Since the unit of diversion is a cookie, it's better to choose number of cookies rather than user-ids as invariant metrics for sanity check, we definitely want to make sure that control group and experiment group have equal amount of users assigned. Number of clicks is also favored, because it's a population sizing metrics that should be equally assigned to control and experiment group. CTR is simply a number calculated by number of cookies and number of clicks, this metrics is not expected to change while number of cookies and number of clicks are fixed.

### Evaluation Metrics

* Gross conversion: That is, number of user-ids to complete checkout and enroll in the free trial divided by number of unique cookies to click the "Start free trial" button. (dmin= 0.01)
* Retention: That is, number of user-ids to remain enrolled past the 14-day boundary (and thus make at least one payment) divided by number of user-ids to complete checkout. (dmin=0.01)
* Net conversion: That is, number of user-ids to remain enrolled past the 14-day boundary (and thus make at least one payment) divided by the number of unique cookies to click the "Start free trial" button. (dmin= 0.0075)

Selected evaluation metrics are listed above, the reason why gross conversion is chosen is that this metrics is expected to be lower in the experiment group compared to control group. The number of students who fininsh check out after clicked free trial button are expected to be reduced due to the warning in the experiment group. Given that number of cookies is fixed, the gross conversion will be different between two groups, which is a part of null hypothesis.

Retention is expected to be different between control and experiment groups. Null hypothesis states that showing up the warning will not reduce the number of students who past the free trial and finish the course. Like we discuss above, number of user-id to complete checkout will be expected to different between control and experiment groups, the retention will be also different, which makes it a good metrics for testing null hypothesis.

Net conversion should be roughly the same, since number of user-ids pass the free trial and number of cookies to click the button is fixed according to null hypothesis like we discussed above, it is also a good evaluation metrics.

