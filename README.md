# Supervised-Machine-Learning-Homework

So definately had a bit of a kurfuffle, I tried unzipping the csvs in resources since it made sense that if I needed for those csvs to run with the code for the graders, you can't unzip them in git.
At least, not that was my thinking, files are updated/changed locally and then pushed to the remote, so I would have no way to open them once they were there. 
So I decided to unzip and push them.

Reader, they are zipped for a reason. 

That reason being they are too large to be pushed unzipped and although I know how to add large files from that plugin that I downloaded and used once, 
I had the feeling that this was not the way to go about it. But I had forgotten about this and so when I did some work on they ipynb file and pushed it, 
I couldn't easily unstage the staged commit, there was one in the way, so I had to go to the git log and find it by its id and use git reset --soft <number>.

Got all that sorted out, all the files necessary are there and there are no huge ones. 

-------
Data Preperation

Started on the train_df first, inspected and saw that there are 86 columns, and calling train_df.head() does rows, but truncates columns like it does rows, 10 columns, a '...', and the last 10 columns.
So given that data preperation was stressed a few times in the readme, decided to investigate those, there were hidden columns that were strings, they were all numeric. 
Decision was to drop the 'Unnamed:0 and set the 'index' column to the actual index. both of these two columns have the same values, and index seemed like the natural fit. 

The rest were inspected with df.dropna() for the rows, and df.dropna(axis='columns'), neither had missing data. 
So good on that front, there are a few columns with string values, 'loan_status' being the most important. The others are home_ownership, verification_status, loan_status, 
pymnt_plan, initial_list_status, application_type, hardship_flag, debt_settlement_flag. I enocded all of those string numerically but then I realized the instructions said to use train dummies, so begrudingly did that instead. 
