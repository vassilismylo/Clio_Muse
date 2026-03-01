## Explaining the dataset

events_data:

Description: Contains all the application events that happened for the specific month
- event_date: The day the event happened, written as numbers in year-month-day order
- event_timestamp: The exact moment the event happened, stored as microseconds since January 1, 1970 (Unix epoch)

These two are used to create the column event_datetime by converting the timestamp to datetime.


- event_name: The type of action the user did, such as updating audio playback time

This is the most important column. There are 96 different event names. 
Based on their names, they can be divided into two distinct groups. Events that are navigating the app (see navigating_events.txt) and events that are connected to listening to a tour. The logic here was if there tour id is not null, the event is a listening one (like story_listened_20, story_start).

If the tour id is null, then the event is not connected to a listening one, it is navigating the app, (like screen_view and click_purchases_tab)

In the listening_events dataframe , i have ordered it by pseudo_user_id and the datetime it happened. So if someone starts reading it, it starts with one user and all their "listening" actions sequentially based on time. Read through the pages to understand better what is happening.

- platform: The device or system the user was using

This is the most important distincion. IOS users in the listening_events, unfortunately dont have events like story_start, story_end and other. There is only events like time_update, story_listened_20 , 40, 60, 80.

Android users dont have the event time_update, their journey through listening a tour is more detailed, with start_tour, start_story, story_listened, story_end, tour_end and events like that. 

- language: The language setting of the app
Self explanatory

- user_id: The internal numeric ID that identifies the user
- user_pseudo_id: An anonymous ID used to track the user without personal information (not signed in)

These are interesting. When a user opens the app for the first time, regardless if he signs up or not, he is assigned a pseudo_user_id by the app, that can monitor his behaviour without tracking his personal information. This distinct pseudo_user_id is not temporary, it is saved even after the user closes the app (i think so), so that makes the classic user_id only usefull when examining the users dataset. 

- tour_id: The ID of the tour the user was listening to (look at tour_title_mapping.csv for info)
Here these are also interesting.

These are the tour id's, there is also mapping of the names in the tour_title csv. 

- story_id: The ID of the specific story within the tour

Every tour contains multiple stories. These stories are small in length, and their id's are sequential numbers in every tour. So for example tour 512 has stories 28001, 28002, 28003, exc... 
The stories are what the user sees or listens to. The user can skip a story, go back to the previous, choose between stories so just jump to the last one and other stuff like that. Thats why it could be easy to analyze the user's behaviour when listening a tour.

- lang_id: The ID of the story language (look at id_language_mapping.csv for info)
Self explanatory

- audio_time_played: Time of audio when user pressed play

This column is associated with only one event_name: play
This is the time of audio of the STORY when user pressed play. Of course for the play button to be available, the story has to have been paused. If you see , before almost audio_time_played, there is a audio_time_paused with the same value, tour_id,story_id, user_id exc...
Also the stories as we said are small. One tour might be 70 minutes long but contain 85 stories. That means that these stories are by average less than a minute long, so this explains why the majority of values in both audio_time_played and audio_time_paused are really small numbers. (majority under a minute, mean of like 2 seconds) 

- audio_time_paused: Time of audio when user pressed pause

this column is associated with only one event_name: pause

The same as audio_time_played, just this comes first. 

# Outliers

There is a user_id of 0 that has like 800k lines while the next biggest user id or pseudo_user has 10k lines so that might be a test user admin acount. Also he has 8k different distinct pseudo_user_id's


