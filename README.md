# Sibling Interactions on Twitter
## A Sample Identified by Tweets About National Siblings Day on April 10, 2018
This is a class project for Timothy Brick's HDFS 597 "Mining Internet with Python" at the Pennsylvania State University.
* Copyrights to Xiaoran Sun, MS, and Timothy Brick, Ph.D., at the Pennsylvania State University.
* For citation, please contact Xiaoran Sun xiaoran.sun@psu.edu

## Study Background
Siblings play important role in one another's development (Dunn, 1983; McHale, Updegraff, & Whiteman, 2012). Research on siblings has used global questionnaires and interviews to examine their relationships and interactions, mostly through *offline* activities. However, although social media has become an important part of many people's life, especially among youth and young adults (Pew Research Center, 2016), we know much less about how they interact *online*, including on social media (LeBouef & Dworkin, 2017). Twitter is a platform that people use for social networking and obtaining information (Zhao & Rosson, 2009). I use Twitter to examine sibling interactions online because it provides free, open source data through the API, and previous research has used data from Twitter to capture interactions between romantic partners (Garimella, Weber, & Cin, 2014).

Identifying sibling users on Twitter can be time-consuming, involving a large amount of human annotation work (Sun, Chi, Yin, & McHale, in progress). However, the National Sibling Day on April 10 may allow us to identify sibling Twitter users in a more efficient way. On that day, #NationalSiblingsDay (and other similar hashtags) is a trending topic on Twitter, and people tend to tweet that topic and mention their siblings in the tweet. Therefore, collecting tweets about that topic on that particular day and utilizing a subset of those where one user mentions the other(s), we are likely to identify sibling users in a potentially reliable way.

## Method
### Streaming Tweets about National Siblings Day
Starting from 9pm, April 9th, until 4am, April 11st, I used Twitter Streaming API to filter realtime tweets that have any of the hashtags (case-insensitive), including "#nationalsiblingday", "#nationalsiblingsday", "#nationalsibday", "#nationalsibsday", "#siblingday", "#siblingsday", "#sibday", and "#sibsday", and/or any of the key words, including "sibling day", "siblings day", "sibling's day", "sib day", "sib's day", and "sibs day". I stored the tweets in json format on my disk. 

The corresponding code file is `DiskListener.py`, created by Timothy Brick, with little edits by Xiaoran Sun for filtering criterion.

This resulted in 383,040 tweets, with the total data file size as around 2.5GB. To get these raw data, please contact Xiaoran Sun.

### Pre-Processing Raw Data Files and Reading in Raw Data
The raw data file (in json) is too large and when it's read in Jupyter as a whole, my laptop would crash. Therefore, I used bash command (on the Terminal application) to separate the json file by lines into separate text files.

To separate a big json file into smaller files that are not larger than 30,000 lines, I used:
`split -l 30000 filename.json`

But these smaller files cannot be read directly into jupyter due to their incompleteness. Therefore, at the beginning of each file, I had to make sure there was or I added a `[`, and at the end of each file, `]`.

To check whether these files are complete as json lists and also get to know the length of each file, I used (bash command):
`jq '. | length' SmallFileName`. When checked by this command, there was some parse error or EOF with some small files, and I found that it was because `"` at the beginning or the end was reformatted into `“` or `”`. These quotation marks had to be formatted back. I did it manually, but I know it is better to write codes for this task and I will update on this soon.

### Text Analyses
Before identifying siblings using the data, I would like to know what the users were talking about when they tweeted about National Siblings Day, using text analyses. Before analyses, I expected that possibilities include:
  * individual human users mentioned their siblings on Twitter and celebrate the day,
  * individual human users post past pictures with their siblings in memory of their experiences,
  * non-human accounts celebrate the day for example, by mentioning how siblings are precious,
  * non-human bussiness accounts make promotions for this day.
Text analyses conducted include:
  * 

