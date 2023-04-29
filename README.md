# TED-Talk-Topic-Predictions

[Final Report.pdf](https://github.com/cccc237/TED-Talk-Topic-Predictions/files/11358286/Final.Report.pdf)


## Introduction

TED talks are videos online that present an idea within 18 minutes to ensure audiences are attentive throughout the entire talk. However, transcripts are often long and tedious to read through. Speakers also have to spend a certain amount of time to determine the most suitable and interesting title for the talk. To help shorten the time it takes to categorize the talks for events or time it takes to search, our team is aiming to predict the theme of the talk using machine learning from the script.[1] Moreover, to help give an idea to all TED Talk listeners and the public on how many related groups of words were used among the accumulated TED Talks over the past few years, our team would also generate graphs consisting of clusters of data points.

## Why Problems are Interesting and Important

Given the script of a speech, it is interesting to obtain the major themes of the talk from supervised learning. This problem is important because it can help save TED talk event organizers time in planning events. Sometimes it is hard to identify what the major themes are in a long piece of text or speech for both speakers and audiences. As well, TED could hold events consisting of a variety of themes rather than talks with similar themes in a single event when the organization is able to discover the themes from the speech.[1]

Among all the accumulated TED talks generated over the past few years, it is important to see how many distinct categories there are regardless of the TED Talk topics. For example, finding the number of distinct transcripts categories out of all the transcripts in our data file. Even if there are around 30 topics identified in total, the content could actually be overlapping, producing a result of only a few clusters. This is interesting as it gives the general public and students an idea of the number of cluster groups among all the intelligent TED Talk content created.

## Data Description 

The dataset used in this project was “TED Talks by ID plus transcripts and LIWC and MFT plus views”, a CSV file from Data World.[2] Before cleaning the data, there were 2475 rows, with each row being a distinct TED talk. The original dataset had 124 columns, which included “id, speaker, headline, URL, description, transcript_URL, month_filmed, year_filmed, event, duration, date_published, views_as_of_06162017, tags, transcript”. However, most of these columns were not used because the main goal is to use the transcript to predict the category, which is described further below.

### Categorization of Tags

Each row in the TED Talk is associated with a various number of tags. Since multiple tags could not be predicted, some further categorization was needed. Through Excel, the team found there to be 416 unique tags. From those tags, the team manually categorized them into 22 categories, which are: Arts/Music/Entertainment, Animals/Aliens, Technology, Health/Science, History, Earth/Environment/Ecosystem, Politics, Career, TED, Religion, World, Education, Media, Family/Life, Law/Crime, Identity, Business, Emotions/Behaviour/Humanity, Safety Concerns, Charity Efforts/Activism, Food, and Travel. This was determined to be the best way to categorize tags because that way we can look up the context to each tag and make sure they were categorized accurately. 

After obtaining the categories, the tags for all TED talks were parsed, and matched with the appropriate category. Then, the category that occurs the most frequently is chosen as the dominant category for the TED talk. For instance, if a TED talk had tags animation, art, and DNA, the categories would be Art/Music/Entertainment, Art/Music/Entertainment, and Health/Science, respectively. Thus, the dominant category for the TED talk would be chosen as Art/Music/Entertainment because it’s the most frequent category. 

This methodology was applied to all TED talks using formulas in Excel. A new column in the CSV file was created called ‘category’, which became the class variable being predicted. The category column would contain one of the 22 categories for each TED talk.

### Data Cleaning

After categorizing the tags, the next step was to clean the data. Some of the TED Talks had categories of N/A, because there was no dominant category. Thus, those TED Talks were removed, now left with 2032 rows (2032 TED Talks). As well, all columns except category and transcript were removed, since the features that are used in this project are from the TFIDF and count vectorizer,

Text pre-processing was done on the transcript column. The goal is to use the words in the transcript to predict the category of the TED talk, but some words won’t be as useful as others for prediction. The first step was to remove stopwords, so unimportant words like “I”, “and'' are not included in the features. The next step is to remove punctuation, as they are not important either. Finally, the stem words were found in the transcripts to determine the root words that would possibly later become the features after applying the TFIDF and count vectorizer. The stemmer was used instead of the lemmatizer because it was more effective in getting the root word.

Furthermore, a column called “category_number” was created that maps the category name to a number through a dictionary. This was created so that the order of the coefficients would be known for logistic regression, and the axis of the confusion matrices could be understood. The dictionary is also in order of highest to lowest volume of TED talks.

