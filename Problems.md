To answer the questions that are in Ideas.md we need to define what we are going to do about these problems in the dataset:

1) If we want to cluster users, or run analysis on users, we need to define what a user is. There are user_id's and pseudo_user_id's but for many user_id's -- there are multiple pseudo_used_id's , and for many pseudo_user_id's -- there are many user_id's .

That means that user_id is not a robust way of identifying a user and pseudo user id is most likely the id of the specific device the users use to open the app. 

We need to define which users to use so that when we are clustering based on their behaviour, we do not count them twice and present the same user as different ones. 

2) Intended story order: We have story_id's for each tour, and there is a story order from the story_details csv. But we need to find which story_id's do not exist at all in the dataset from the csv and remove them from the "correct" order. If we want to include this as a feature we need to make story order robust so that we can determine which users actually listened the whole story correctly and did not jump around.


3) Try to understand the problems in the IOS users data. 

Firstly analyze the Android data and see if there are robust or if they have similar problems or that they make sense. 
After that we need to decide if there is a robust way of correct the IOS data or if there is no way we can use these data correctly so we will remove them. 

Maybe there are similar patterns in both platforms which could help us determine where a story should end, and pick that as end point in the IOS data. 


## Work done so far:

1) In user_id_analysis notebook we can see that pseudo user id is a robust enough authentication metric of counting users. Pseudo user id is most probably a device id that is assigned the first time a user opens the app with a specific device. After removing user id = 0 which is clearly a pre-authentication id / a id assigned when the system doesnt know who is logged in or just a test account (maybe the tester logs in when a user needs assistance, we are not sure) the results show that only 361 pseudo user id's contain more than 1 distinct user id. That means that user_id-pseudo_user_id is mostly a 1-1 relationship so we can be sure that clustering users that way is robust.

2) Here we compared 3 different sources of stories. 

First we got the story id's , story order and total stories of each tour from the story_details csv. 

Secondly we scraped the Clio-Muse website for tour info. We found for most of the tours: The total length of the tour and the total stories of the tour displayed in the website.

Thirdly we analyzed the events data and found the story_id's and total stories per tour from inside the data. 

We compared the three results and created the correct story order.

The problems were: In the story_details csv some tours contained more story_id's that we found in the website and in the events data. If the number of total stories in event data and in the website was the same, we can make the assumption that these stories inside the csv are previous stories or test stories, in any case they probably werent available to users, hence the discrepancy. 

In some tours, there were big discrepancies in the total stories found in the csv or the website compared to stories found in the data. These of course were cases of tours that were not listened or listened very little.

The story order is in story_order.parquet 
