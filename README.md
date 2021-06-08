# Analyzing Celebrity Language on Twitter
Different social + political movements to be analyzed: 
1. COVID-19 (completed)
2. Election 2020 (data is retrieved, analysis is ongoing)
3. Black Lives Matter (data is almost retrieved)
4. TimesUp (still need to get data)

The involvement of celebrities in politics continues to increase, especially with the growth of social media platforms, like Twitter, that allow celebrities to interact with their fans and the public sphere is a completely new way. With the rise of the social media celebrity, celebrities are more aware of their own presence in the media and have used their status to their advantage, leveraging brand deals with huge corporations and earning exorbitant amounts of money. Social media is now a part of a celebrity’s status and recognition; celebrity fame is not only defined by their accolades but also by their presence on these social media platforms. Celebrities are now expected to be involved in political and social movements in some shape or form, facing pressure from both their corporate brand and their fans, whom they engage with through these social media applications. 


# COVID-19
Using natural language processing (NLP) techniques, like sentiment analysis and document similarity metrics, this study shows that celebrities on Twitter attempt to be very neutral in sentiment when discussing COVID-19 compared to the general public. Celebrities are defined as verified users by Twitter itself. Verified users, on average, use more neutral sentiment compared to unverified users. This can be attributed to the seemingly balanced role they play between being defined by their corporate brand and being relatable to their fanbase. When analyzing their similarities through document similarity metrics, verified and unverified users, however, do not seem to use significantly different language. This could be attributed to several factors, one of the biggest being that all of the tweets consider one topic.

## Data

The Twitter API is a programming interface that allows programmers to collect information concerning Twitter users, specific tweets, hashtags, etc. Tweepy is a Python library that allows programmers to access this API via Python itself (Roesslein, 2020). The data was procured through this package by searching the hashtag #covid19. Tweets were collected since July 25, 2020 with an initial 17,000 tweets and have continued to be collected since that date. The dataset currently contains 179,108 tweets, with 13 features. The features are as follows: 

•	user_name: the username of the individual who wrote the tweet
•	user_location: the location of the individual who wrote the tweet according to their bio (this is not mapped geographically and can be any text)
•	user_description: the bio or description of the individual who wrote the tweet according to their profile
•	user_created: the date that the account of the individual was created
•	user_followers: the number of followers that the individual had the time of writing the tweet
•	user_friends: the number of mutual followers (followers that the user also follows back) that the individual had the time of writing the tweet
•	user_favourites: the number of favorites for this user
•	user_verified: a Boolean (true/false) that states whether or not the user is verified by Twitter
•	date: timestamp of when the tweet was written and posted
•	text: the actual text of the tweet
•	hashtags: a list of any hashtags that were in the tweet
•	source: where the tweet was posted from (e.g. Twitter for iPhone)
•	is_retweet: a Boolean that states whether or not the tweet was retweeted from another user. This is False for all of the values in the dataframe

There are 22,974 tweets made by verified users and 153,906 tweets made by unverified users. 

## Models

NLP tasks are generally approach one of two ways: statistical NLP or rule-based NLP. The terminology is deceiving, as rule-based NLP tends to employ more statistical methods while statistical NLP tends to employ more traditional linguistic roles. While statistical NLP is usually used to tackle modern NLP problems and is considered the superior approach, rule-based approaches are greatly welcomed in several cases: (1) a domain specific problem that would not be satisfied by state-of-the-art models, (2) lack of labeled data, and (3) limited funding for training. Moving forward, I will use this rule-based approach because I lack labeled data and any financial rescue.

### VADER 

Valence Aware Dictionary and sEntiment Reasoner (VADER) is one of the most powerful rule-based sentiment analysis models. It is a lexicon sentiment analysis tool that is specifically used for social media content, so it is the best suited model for sentiment analysis of tweets. NLTK, another Python library, is a well-documented and powerful natural language toolkit that contains a model for VADER. The module outputs four polarity scores for each tweet: (1) negativity, (2) positivity, (3) neutrality, and (4) compound. The compound score is an aggregate of the first three scores, and the first three scores always add up to one. 

For example, the tweet ‘hey and wouldnt it have made more sense to have the players pay their respects to the a’ received a polarity score of 0.075 negative, 0.802 neutral, 0.123 positive, and 0.2263 compound under the VADER model. As you can see, 0.075 + 0.802 + 0.123 adds up to 1.0. The compound number is not simply an average of the first three polarity scores as it employs a bit more strategy in understanding the sentence as a whole. 

## Hypothesis Testing 

As I noted previously, the number of unverified users exceeds the number of verified users by a wide margin. This makes it quite difficult to see whether or not the difference between verified and unverified users is statistically significant. In order to compare the difference between the two groups of users and perform a hypothesis test, I sampled 20,000 tweets for each group instead of generating value counts for the entire dataset.

The compound polarity score is, again, an aggregate of the positive, negative, and neutral polarity scores. These polarity scores are different from the labels in Table 1, which were created based on the compound polarity score. The mean for the unverified users sample of compound polarity scores is approximately 0.0470. The standard deviation for the unverified users sample of compound polarity scores is approximately 0.412. The mean for the verified users sample of compound polarity scores is approximately 0.0611. The standard deviation for the verified users sample of compound polarity scores is approximately 0.384. All of these numbers were rounded off with three significant figures.

Because the standard deviations for the verified user group and the unverified user group are quite different, I used Welch’s t-test to perform the hypothesis test. I received a test statistic of 3.53, rounded to three significant figures. The p-value was 0.000409, rounded to three significant figures. With an alpha of 0.1, we can reject the null hypothesis that stated that there was no difference in sentiment between verified and unverified user populations.  
