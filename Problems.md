To answer the questions that are in Ideas.md we need to define what we are going to do about these problems in the dataset:

1) If we want to cluster users, or run analysis on users, we need to define what a user is. There are user_id's and pseudo_user_id's but for many user_id's -- there are multiple pseudo_used_id's , and for many pseudo_user_id's -- there are many user_id's .

That means that user_id is not a robust way of identifying a user and pseudo user id is most likely the id of the specific device the users use to open the app. 

We need to define which users to use so that when we are clustering based on their behaviour, we do not count them twice and present the same user as different ones. 

2) Intended story order: We have story_id's for each tour, and there is a story order from the story_details csv. But we need to find which story_id's do not exist at all in the dataset from the csv and remove them from the "correct" order. If we want to include this as a feature we need to make story order robust so that we can determine which users actually listened the whole story correctly and did not jump around.


3) Try to understand the problems in the IOS users data. 

Firstly analyze the Android data and see if there are robust or if they have similar problems or that they make sense. 
After that we need to decide if there is a robust way of correct the IOS data or if there is no way we can use these data correctly so we will remove them. 

Maybe there are similar patterns in both platforms which could help us determine where a story should end, and pick that as end point in the IOS data. 

