# Sentiment Analysis

AFINN lexicon implementation for the Mensa group

## Installation
- Download this repository using `git clone https://gitlab.com/herts_mensa/sentiment_analysis.git` or just donwload as a zip file
- Install the latest python 3: https://www.python.org/downloads/. Make sure python binaries are in the system PATH. 
- open a terminal/command prompt and go to the "Sentiment Analysis" directory. For example
  - Windows: 
     - Click Start and type `cmd` and Enter: then `cd C:\herts\sentiment_analysis` If you downloaded to C:\herts directory
  - Linux/MacOS:
     - On the terminal type: `cd /home/herts/sentiment_analysis`
- Install the required dependencies: `pip3 install -r requirements.txt`. This should add install everything required to run the notebook
- After this is done, type in: `jupyter-lab` and press Enter. This should open a browser window showing the notebook. From this point on, we are ready to write code.

### Analysis approach walk-through
The approach followed in creating this notebook is as follows:
- Initialization
   - Create an AFINN object for parsing the data
   - Read and convert the data into a panda dataframe for analysis
   - Print the dataframe's preview, a truncated view of the data
- Generating the sentiment analysis 1. Afinn lexicon
   - With the dataframe created above, this step:
      - appends additional columns "score" and "sentiment_category". These indicate how each review is scored according to the   AFINN lexicon
   - For each entry, a score's sign indicates its category in the "sentiment_category" column, with zero indicating a neutral review
- Generating the sentiment analysis 2. Vader lexicon
   - Similar to the step above, but this time using the vader lexicon, for comparison. Note that the same sorted order from the afinn lexicon is preserved so the output is comparable to the one above. 
   - To make the comparison easier, the score and sentiment category are appended to the data frame to show a one to one view of the two lexicons. 
   - The vader lexicon differs from the afinn counterpart in the way the scores are computed. The vader lexicon scores betweeen -0.05 and 0.05 to destinguish negative and positive scores, whereas the afinn lexicon uses negative and positive numbers respectively to achieve the same
- Present sorted data
   - With the two lexicons evaluated, we then show the two side by side with the data
   - Results are sorted according to how helpful they were and the afinn score given.
   - Next the statistics for the data are given as a summary:
- Plot each lexicon's analysis as a bar graph
   - We plot the two lexicons' analyses as two column graphs side by side.
   - This enable us to see and compare the effects of the two lexicons. Of interest is how each inteprets the neutral and negative sentiment categories
- Normalization
   - Next,the dataframe is normalized in order seek correlations in how helpful a review is in relation to its length
   - To make this possible, the dataframe is parsed and all numeric entries that have NaN (representing entries the reviewer chose not to enter input) are then converted to zeros to enable anaylisis
   - Thereafter a new column is introduced - comment length which will show a numeric representation of the comment length of each entry.
   - A printout of the data with the new comment length column is then displayed
- Correlation
   - Using the panda library's corr() function, we collect relevant columns from the data frame and apply correlations
   - For comparison, we include both the afinn and vader scores in order to see the effects of each lexicon's correlation with the given data
   - We can deduce from this how a highly helpful comment correlates the afinn lexicon's score (higher value) vs the vader lexicon's score (relatively lower value)
- Visualizing effect of how helpful a review was voted against the length of its comment
   - To make sense of the correlation, we can graph the original dataframe's data, this time only showing the how helpful a review was found in relation to the length of its comment
   - For each of the lexicons, we plot each one, first with normal values including extremes, and then without extremes to get a more compact view of the data
- The above plots show again the difference between the two lexicons i.e.
   - Afinn lexicon relies on quantity of text
   - Vader lexicon relies on the content of the text
- Additional visualization
   - Only for viewing, below we create additional 3 dimensional graphs to see correlation among 3 points of data: helpful, comment length and score, where score can either be afinn or vader.
   - First we define the functions to process the two variations, then we plot out the 3D animations
- Showing only relevent data
   - As a last step, we strip down the data, outputting only the entries that have a helpful value greater than 15
   - This has the effect of trimming down the data to far fewer records

