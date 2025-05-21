Id	ActivityDate	TotalSteps	TotalDistance	TrackerDistance	LoggedActivitiesDistance	VeryActiveDistance	ModeratelyActiveDistance	LightActiveDistance	SedentaryActiveDistance	VeryActiveMinutes	FairlyActiveMinutes	LightlyActiveMinutes	SedentaryMinutes	Calories




## FINDINGS 
• There are 35 unqiue Ids in database (457 rows in total with no missing value)
• The data records activity of 35 users from 2016-03-12 to 2016-04-12 --> 14.74 average records per unique Id (min : 8, max : 32)
• TrackerDistance and TotalDistance data is almost same --> Tracker is very accurate
• Calories have high corr with :
    TotalDistance > TrackerDistance > TotalSteps > VeryActiveMinutes > LightActiveDistance > VeryActiveDistance
• Calories have low to negligible corr with :
    ActivityDate < SedentaryMinutes < SedentaryActiveMinutes < LoggedActivityDistance
• Data in LoggedActivityDisctance and TotalDisctance varies significantly with many records as 0 --> Majority times data is not logged      manually
• VeryActiveDistance and VeryActiveMinutes have many records as 0 --> Many users do not regularly have high intensity sessions
• TotalSteps and TotalDistance are highly proportional and can be used to generate a new feature StepsIntensity
• Pattern of Calorie burned across the time frame is somewhat similar among all users with regularly occuring crests and troughs
• Few users have logs recorded before majority started 
• Calories burned by each user on each day varries a lot with difference of about 1000 Calories 
• There is high non linearity in the plot of TotalSteps/Distance vs Calories for each Id --> Efforts put by different people for each step varies
• Many users with appx. zero VeryActiveDistance have noticeable calorie burn (due to light or moderate activities) but more VeryActiveDistance implies more calories burnt
• VeryActiveIntensity proves to be a better feature to judge Calorie burn
• Sedentary-activity has no or very-insignificant role in Calories burnt
• Light-Activity-Intensity has somewhat ploynomial relation with Calories burnt



# Prediction approach 
• Instead of using the pre-given features we can generate more useful features with more defined relation to target column for e.g. :
    1. TotalSteps and TotalDistance can be combined to obtain StepsIntensity
    2. VeryActiveDistance and VeryActiveMinutes can be combined to VeryActiveIntensity

• Features like ActivityDate, Id, LoggedActivitiesDistance and those related to Sedentary-Activity can be dropped
• Features related to Light-Activity can be used as it is
• Moderate-Activity features can be utlized for model buidling 

# Models to be used
• Gradient Boosting models could work efficiently for our non-linear data. Would also help deal with outliers
• Random Forest Regressor is also a good model for our purpose as its' less sensitive to hyperparameters 