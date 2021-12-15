# Sevilla Interview Analysis- Final Report
Angela Krak

December 15, 2021


## 1. The Purpose

The primary goals of this project were to transcribe data from a previous investigation, organize the transcriptions in a way that was suitable for data analysis, and observe trends in the interviews. One strength of the study was using computational methodology to conduct quantitative analysis on data that would otherwise be largely analyzed using qualitative methods. Preparing the data and conducting frequency analyses can allow trends to emerge that would require much more manual labor to discover. Though this final project focuses on frequency analyses, it leaves the door open for qualitative methodology such as discourse analysis via keyword extraction in the future. 

On a more basic level, this project is the first analysis that I have conducted on transcription data. It can be overwhelming to have hundreds of utterances from speakers- what should be the focus? Which responses or sentiments are commonly shared across participants? These questions arise without even considering the topic of the interviews, which add other options for analysis. Establishing a workflow for transcription, organization, and basic analysis allowed me to manage the data in this project, and will make life much easier for any interview data that I collect in the future! 

## 2. The Topic

As mentioned, the data from the current project were previously collected during a larger project that I was conducting in Seville, Spain. I am interested in speech perception of sociophonetic traits, especially ones that can be connected to regional prestige or stigma. The project focused specifically on perception of word-initial [s], which in Peninsular Spanish, varies by place of articulation. Central Spain produces an apico-alveolar variant [s], and the variety is viewed as the national standard (Penny, 2004). In southern Spain, especially in Seville capital, the place of articulation of 's' is dental. The speech in Seville is considered to have covert prestige, though it cannot compete with the prestige from central Spain (Hernández-Campoy & Villena-Ponsoda, 2009). Finally, in the outskirts of Seville exists another variant, which is an 's' production with interdental mixing. This variant is highly stigmatized, and has no prestige at any level (Regan, 2017). Seville capital and the outskirts are very geographically close, and they share cultural pride for the region in which they live, Andalusia. However, there is evidence that prestige variants from central Spain are spreading through the south (Regan, 2017), introducing a unique relationship between identity and prestige.

## 3. The Data
The data from the current project consist of transcriptions from a brief sociolinguistic interview. I asked each participant 5 questions, which have been translated below:

- 1. Where are you from? Have you always lived in Spain?
- 2. What is your opinion of the linguistic variety that exists within Andalusia?
- 3. Have you traveled outside of Andalusia, but within Spain? When you leave the region, do you receive any comments about your accent?
- 4. Do you think there is representation of the Andalusian accent in the media, movies, etc?
- 5. Do you think that stereotypes about the Andalusian accent are changing now, or that they still remain?

Each participant could speak for as long as they wished. In total, data were collected from 24 participants, but only 22 have been analyzed in this final project (one speaker was not from Seville, and the audio from the other was not optimal). The duration of the audio analyzed in this project totaled to 1 hour, 3 minutes and 4 seconds. The average length of each sound file was approximately 3 minutes long. I transcribed all data, checking with a native speaker from Seville when clarification about utterances was necessary. Since the content of the data is most important for this project, no repetitions were transcribed unless speakers repeated themselves for emphasis. I also chose not to include restarts, fillers, and utterances produced by anyone other than the participant being interviewed. 
 
## 4. The Organization
When completing the transcriptions, I created one text file per interview question and saved the file as the participant code_Q1-5. Participant codes were randomly generated 3-digit numbers, as all data are anonymous in this project. The file naming system streamlined the data organization process in R because I was able to use the file names to extract both the participant and question information. The tidy text format (Wickham, 2014) was used to organize the data for frequency analysis, meaning that each utterance had to be split into separate rows by token. `unnest_tokens()` was used to conduct this step Thus, the overall data frame with all questions and tokens consisted of 6,187 words/rows in this format. There were 5 columns: word, line number, file name, participant, and question. The tidy text format is useful for frequency analysis, but would not be very informative for qualitative analysis in which utterance extraction is needed. However, it is easy to access the data in utterance form before `unnest_tokens()` was implemented.

## 5. The Analysis
The primary analyses conducted on the data were to collect frequency trends, both within the set as a whole and in each individual question. While I was transcribing the data, I had an idea of which words would arise in the summaries because of similar sentiments being expressed across multiple speakers. However, before being able to see accurate frequency trends, a few steps had to be taken. First, Spanish stop words were removed so that highly frequent function words such as articles and pronouns would not interfere with counts. I had to modify the existing list of stop words, as there were not enough items included in the initial list of 300 words. I added connectors like "entonces" and "pues" to the list of stop words, as well as a few other items that did not contribute meaning to the data set. After using the `count()` function on the overall data set that excluded stop words, there were 2,497 rows. 

![Sevilla Word Frequency](Sevilla_Words.png)

Unsurprisingly, the most frequent words from the whole data set were **acento**, meaning "accent", and **andaluz**, referring to the Andalusian varieties. Since I was particularly interested in the results from questions 3-5 due to questions posed, I did a frequency analysis of each question. Though I cannot show the full token counts of these data for privacy reasons, the top results have been plotted in graphs using `ggplot()`. 

One frequent term in question 3 was **gracioso**, meaning "fun" or "funny". According to the frequency results, this item appeared 9 times in Q3. It ocurred to me that this term should be more frequent, as it was by far one of the most repeated adjectives across participants. I then realized that a lemmatizer would need to be added in the future to combine **gracioso** with its feminine and plural forms as well. Another interesting item in Q3 was the word **chistes**, which means "jokes". This word was used 5 times by speakers who expressed that often when they traveled outside of their region, people ask them to tell jokes.  

![Q3 Frequency Plot](Q3_freq.png)

In question 4, participants were asked whether they felt there was accurate representation of their accent in the media and in movies. Frequent items included the words **representación**, "representation", **películas**, "movies", and **actores**, "actors". One interesting item that was repeated 5 times was the word **exagera**, "exaggerate". Some speakers expressed that they did not like when their accent was exaggerated in the movies by actors who were not from southern Spain. A lemmatizer would also help in this question, as the noun **exageración**, "exaggeration", also appeared in the set at a lower frequency. 

![Q4 Frequency Plot](Q4_freq.png)

In question 5, participants were asked whether or not they felt that the stereotypes about their accent were changing or still remained. The words **permanecen**, "they remain", and **cambiando**, "changing", are represented in the frequency plot. However, a keyword analysis would be necessary to analyze these terms and extract the utterances themselves, since **no** was included as a stop word.  

![Q5 Frequency Plot](Q5_freq.png)

## 6. Conclusions

In summary, I learned how to organize transcription data and prepare it for quantitative analysis, an approach that can better inform qualitative observations by bringing to light important frequency trends in a quick and efficient way. I also learned the importance of tailoring methodology to suit the data set of study. For example, I added more items to an existing list of Spanish stop words, as the presence of connectors was muddying the frequency data. For this particular project, it is also important to consider the lemma of the item, since the inclusion of different parts of speech/singulars/plurals can impact how frequent a token appears in the counts. 

## 7. Works Cited

Hernández-Campoy, J.M., & Villena-Ponsoda, J.A. (2009). Standardness and nonstandardness in Spain: dialect attrition and revitalization of regional dialects of Spanish. *International Journal of the Sociology of Language, 2009*(196-197), 181-214.

Regan, B. (2017). A study of ceceo variation in Western Andalusia (Huelva). *Studies in Hispanic and Lusophone Linguistics, 10*(1), 119-160. 

Penny, R. & Sánchez-Méndez, J. (2004). Variation and change in Spanish. Madrid: Gredos.

Wickham, Hadley. (2014). "Tidy Data." *Journal of Statistical Software 59*(1): 1-23. 



