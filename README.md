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

Consideration hypothesis
--------
I think that the random forest classifier will do a better job than the logistic regression model, because a decision tree irrerates X number of times and averages the output, 
but ech one of those individual outputs is attempting to make the best possible solution, and then each one of those solutions is randomly sampling the dataset by RNGing the inputs, 
but they aren't over represeneted if an instance occured multiple times because, you know, randomness.

Consideration hypothesis the second
-----------
Okay so on the unscaled tests, the training scores of the LR and RFC is where one expects it on the LR and something is off on the RFC because I don't care how good it is, 
it shouldn't be 100%. Were not comparing it to itself, and when considering the testing scores, yes there is the drop-off of improvement, but it actually seems like the Logistic Regression did better because its a drop in accuracy by 12% 
but when compared to the drop in accuracy of the random forest classifier, which dropped by 37%, comparatively it seems like it is doing better.

Hypothesis testing
--------------
So in review, the random forest was not better, but I think that something is off and I will have to go back and check. 
Its either the case that when comparing training data to itself should always return 100% accuracy, seen here in the training score of 1.0 of the RFC but NOT OF the LR model which was like 0.62, and this is on the unscailed. 
But that didn't play out, and so something was off in the beginning I think with the RFC, and this becomes magnified in the scaled portion. 
Again, here the LR just does a 'better' job, it improved at each step of this analysis, and its not great, each of the improvements but they are marginally better by some like some 10% increase each time. 
I included the confusion matrix and classifcation report just to check myself, and then went back over them with the accuracy printed value to double check myself and there is something up with the random forest from the beginning. 
It was either the random_states being set at 42 in the beginnging, and that clouded it from that point forward, or I messed something up that someone will udoubtedly point out to me.

But at the end of the day it was the logistic regression model that was better, its improved with scaling, and it has a believable breakdown on the accuracy, confusion matrix and classification report.

------------
So I was completely wrong in my assumption that the random forest would do a better job than the logisitic regression when, but that was the case, 
it was both moving from the scaled to the unscaled, and it was born out by multiple measures including the confusion matrix. the classification report and the accuracy. 
There was something off with the random forest classifier each level of analysis and I performed the post-scaling analysis of it as well and its just weird. 
I renamed the report from the initial submission.
