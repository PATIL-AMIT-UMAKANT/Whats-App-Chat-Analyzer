# WHATS-APP-CHAT-ANALYZER

<br>Analyzing the chats<br>

![Whats app chat Analyzer](https://user-images.githubusercontent.com/94529852/191577711-c3aae00f-44d9-47fc-9d04-632af164c64f.png)



## *Overview*

- [Introduction](#introduction)
- [Data Retrieval & Preprocessing](#data-retrieval--preprocessing)
- [Exploratory Data Analysis](#exploratory-data-analysis)

  - **[Overall frequency of total messages on the group.](#the-overall-frequency-of-total-messages-on-the-group)**
  - **[Top 10 most active days.](#top-10-most-active-days)**
  - **[Top 10 active users on the group (with a twist)](#top-10-active-users-on-the-group)**
    - Ghosts present in the group. (shocking results.)
  - **[Top 10 users most sent media.](#the-top-10-users-who-send-the-most-media)**
  - **[Top 10 most used emojis.](#top-10-most-used-emojis)**
  - **[Most active hours and days.](#top-10-most-used-emojis)**
    - Heatmaps of weekdays and months.
    - Most active hours, weekdays, and months.
  - **[Most used words - WordCloud](#most-used-words-in-the-whole-chat)**
  
- [Conclusion](#conclusion)

# *Introduction*:

Whatsapp has quickly become the world’s most popular text and voice messaging application. Specializing in cross-platform messaging with over 1.5 billion monthly active users, this makes it the most popular mobile messenger app worldwide.

- I thought of various projects on which I could analyse data like - *Air Quality Index* or The *cliched* *Covid-19 Data Analysis*.

- But I thought why not do **Data Analysis on a WhatsApp group chat** of *college students* and find out interesting insights about *who is most active, who are ghosts (the ones who do not reply), my sleep schedule,* *the most used emoji, the most actives times of the day, or does the group use phones during college teaching hours?* 

- These would be some interesting insights for sure, more for me than for you, since the people in this chat are people I know personally.

# *Data Retrieval & Preprocessing*
### Beginning. How do I export my conversations? From Where To Obtain Data?



- The first step is **Data Retrieval & Preprocessing**, that is to **gather the data**. WhatsApp allows you to **export your chats** through a **.txt format**. 

- Go to the respective chat, which you want to export!


- Tap on **options**, click on **More**, and **Export Chat.**



- I will be Exporting **Without Media.**



#### NOTE:
- Without media: exports about **40k messages **
- With media: exports about *10k messages along with pictures/videos* 
- While exporting data, *avoid including media files* because if the number of media files is greater than certain figure then not all the media files are exported.

### Opening this .txt file up, you get messages in a format that looks like this:


# *Exploratory Data Analysis*

### *Importing Necessary Libraries*

We will be using :
1. **Regex (re)** to extract and manipulate strings based on specific patterns.
    - References:
        - [Regex - Python Docs](https://docs.python.org/3/library/re.html)
        - [Regex cheatsheet](https://www.rexegg.com/regex-quickstart.html)
        - [Regex Test - live](https://regexr.com/)
        - [Datetime Format](http://strftime.org/)
2. **pandas** for analysis.
3. **matlotlib** and **seaborn** for visualization.
4. **emoji** to deal with emojis.
    - References:
        - [Python Docs](https://pypi.org/project/emoji/)
        - [Emoji](https://github.com/carpedm20/emoji)
        - [EMOJI CHEAT SHEET](https://www.webfx.com/tools/emoji-cheat-sheet/)
5. **wordcloud** for the most used words.
6. **datetime** for datetime manipulation.


### *Preparation and reading data*

Since WhatsApp texts are multi-line, you cannot just read the file line by line and get each message that you want. Instead, you need a way to identify if a line is a new message or part of an old message. You could do this use regular expressions, but I went forward with a more simple method, which splits the time formats and creates a DataFrame from a Raw .txt file.

While reading each line, I split it based on a comma and take the first item returned from the `split()` function. If the line is a new message, the first item would be a valid date, and it will be appended as a new message to the list of messages. If it’s not, the message is part of the previous message, and hence, will be appended to the end of the previous message as one continuous message.


# *Pre-Processing*

Firstly, let’s load our .txt into a DataFrame.



The dataset now contains 3 columns - DateTime String, User, and Message sent and their respective entries in 13655 rows.

**Let’s create some helper columns for better analysis!**


Now that we have a clean DataFrame to work with, it’s time to perform analysis on it. **Let’s start Visualizing!**



# *Exploratory Data Analysis*

At this point, I think I’m ready to start my analysis so I will plot a simple line graph to see the frequency of messages over the months. 

## The overall frequency of total messages on the group

I expect to see a nice line graph with crests and troughs in odd places.


## Top 10 Most Active Days
Grouping the data set by date and sorting values according to the number of messages per day.



Apparently, the group was very active on 13th September’20 because we were discussing fundamental yet tricky and brain-wracking “Guess the Output” Java questions!

## Top 10 active users on the group

Before analyzing, the top users, let’s find out how many ghosts are there in the group!



#### Shocking Result

- Total number of people who have sent at least one message on the group is 154.
- BUT, the total number of participants are 237.
- That means **81** people in the group have **not sent even a single message throughout these 9 months and 13500+ messages**.


### Now, *pre-processing the top 10 active users.*

Grouping the dataset by the user, and sorting according to the message count.



Now, I will plot the **Average Message Length of the messages sent by the Top 10 most active users**. *Let’s see the results now!*

### *Comparing the top 10 users!*

Now, first things first, since almost all the plots will be *comparing one person with another*, I’ll assign a **specific color to each person** so that it becomes **easy to identify each person among multiple plots**.

I could’ve used *seaborn’s color palette* but:

— Seaborn assigns *default colors* itself, but I wanted ***the color of a certain person to remain the same, no matter the plot.***

— Also, I wanted to try some different colors so I grabbed my color palette from [this website](https://coolors.co/).
#### Defining a function to tackle the problem.

I’m defining this function ***to maintain consistent colors for each person across all plots***. Since the order will vary depending on the plot, this is passed to the function which will *reorder colors in a particular order so that the color of a certain person remains the same no matter the plot*. This will help maintain ***consistency and readability*** amongst the many graphs I will be plotting.



Next, I made a dictionary where **each key is the name and the value for each would be their assigned color**. I create a function that reorders colors given a list of names to match the ordering of the plot. 

This function takes the ordered names as input and returns a reordered list of colors. This list has to be passed into the **`palette`** argument in a **seaborn plotting function.**


It’s really interesting to see plots like this side by side, because here comes the twist:

- Ironically, TK, the person who sent the **most amount of texts** (2000+), has the least messages’ length on average. This means this person sends broken and many WhatsApp messages in one go.

Here is a snippet of how TK sends messages:


Alright, moving on to a more detailed analysis of the dataset!

## The Top 10 users who send the most media

## Top 10 most used Emojis



### Which Emoji is the most used in the chat?



## Most active days, most active hours, most active months.



#### Pre-processing for most active hours.


### Which hour of the day are most messages exchanged?



### Pre-processing Weekdays and Months




### Visualization



## *Inferences*

- The group is **most active on Sundays**, and **least active on Mondays** (probably *Monday Blues*.)

- Also, **Saturday** has a *minor drop*, this is probably due to the fact that Saturday is the *first weekend after Friday* and people are usually taking a *rest* and doing other activities than messaging on their phones.

- The group has been recently very active, in September.


To get a clearer understanding, we will plot a combined graph — **Heatmap**.

#### Now, we will plot a heatmap, combining the above to bar plots, for a better understanding!


### Heatmap of Month sent and Day sent

##### Inferences

- The group is more active on weekends, throughout the months.
- September has the most lighter blue shades and more yellow gradients.
- This gives a *combined analysis*, which is really helpful in **real-time projects**.

## Most Used Words in the whole chat.



### Most Used Words in the chat

# *Conclusion*

**That’s it from my end! I hope you learned and enjoyed a lot!**

It’s really interesting to see the texting habits of people and incidents of daily life reflected in the text. I suggest you take a look at my code and apply it to your own group chats. However, some modifications will have to be done at the DataFrame creation part. 

If you’re interested, shoot me a message and I’ll help you out.


***Thank you for reading!*** *Let me know what you thought about this project.*
