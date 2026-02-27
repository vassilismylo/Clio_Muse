Repository for creating the presentation to CLIO-MUSE at 4/3/2026

Instructions to run the jupyter file:

1) Create a folder called data.
2) Inside this folder create a folder called raw and a folder called clean.
3) Inside the raw folder create a folder called events_raw and a folder called users_raw
4) Put the events csv data we have from clio inside the events_data folder.
5) Put the users csv data we have from clio inside the users_data folder. 
6) Open convert_to_parquet.ipynb, read the instructions at the top to set up the dependencies either using uv or pip
7) Run the convert_to_parquet notebook. 

You will now have a events.parquet file inside the clean folder. 
This will be read much quicker than a csv and cause less memory problems. 
