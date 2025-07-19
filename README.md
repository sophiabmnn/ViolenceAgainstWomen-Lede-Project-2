# Lede Project 2: One week of violence against women in Germany

This is my submission of my second project during the Lede Program for Data Journalism (https://ledeprogram.com/). Text and data have not been editorially reviewed or fact-checked.

You can find my notebook here: https://github.com/sophiabmnn/ViolenceAgainstWomen-Lede-Project-2/blob/main/Project-2-ViolenceagainstWomen.ipynb
 
 A csv-file with the results of my analysis is stored here: https://github.com/sophiabmnn/ViolenceAgainstWomen-Lede-Project-2/blob/main/df_final.csv

## Aim

According to official statistics, tens of thousand women in Germany become victims of sexual and domestic violence every year. As such high numbers often remain abstract, I want to describe: How much violence against women happens in one single week?

## Proceeding

### Data Source

I decided to choose German police press reports as a base of my analysis. The website presseportal.de (https://www.presseportal.de), owned by the press agency „news aktuell“, publishes such reports of local police stations in Germany. 

The advantage of these reports is that they provide quite a few details for each case. Therefore, the victims do not remain simple numbers, but become women with a story. 

The downside, of course, is that these reports are not an official statistic. The police stations probably do not publish every single case of violence. Therefore, all numbers should be considered as minimum of cases, not as an absolute number.

### Scraping

I scraped all local German police reports for one week, between 06/30/2025 and 07/06/2025 - that was just the last week before my analysis. One should be aware that the observation period is defined by when a report for a case was published, not when the case actually happened. Therefore, there a some cases from the week(s) before in my data - and probably also several ones which occurred in the week itself were published after 07/06/2025.

Apart from the release date of the press report, I scraped the headline, the description and the location of the cases.

### Categorization

I trained an AI-model to classify whether a police reported was about „violence against women“ or not. The model I used was gpt-4.1-mini from OpenAI. My precision score was 88.89% percent in the end, my recall score 80.00%. As a consequence, there are probably some reports about violence against women which I missed. 

Every single report which was classified as „violence against women“ by the AI was checked manually. I thereby tried to differentiate: What is ostensibly violence against women - and where were women only involved? For example, I didn't classify a robbery of a woman as “violence against women” - but there are of course more ambiguous cases.

In a next step, I categorized whether the alleged perpetrator was from the private environment of a woman. Also for this, I used the gpt-4.1-mini from OpenAI for a first classification, but checked everything manually.

Lastly, I categorized which form of violence occurred: „Harrassment“ means for example verbal harrassment or threatening, „physical violence“ involves physical contact and homicide means that at least one person died as a consequence of the alleged case. Again, I used the gpt-4.1-mini from OpenAI for a first classification, but checked everything manually.

### Cleaning

Duplicates: In some cases, the police issued more than one report about the same case within the week. I tried to account for these duplicates by filtering for more than one case of the same violence type in the same location. I then manually deleted these duplicates.

Geolocating: With the help of Google’s Geocoding API, I searched for the coordinates of the locations in the reports to be able to map them.

### Results

The analysis shows that there were at least 57 reports of violence against women released within the observation period. These 57 reports included 27 cases of (verbal) harassment, 26 cases of physical violence and 4 cases of homicide (including one case in which not a woman, but a third party was killed). The majority of the reported cases occurred in a public environment - which indicates that there might be a high number of unreported cases from the private environment.

## Learning

My first attempt was to scrape far more data than one week - but it was just too much data (a week alone took already several hours to scrape). Therefore, I had to adjust my focus a little bit. Also, I missed to scrape to URL of the press reports - which was quite annoying, as I had to search all of them manually later on. 

If I had more time, I would try to scrape the data for a longer period and look for even more systematic kinds of violence - maybe it would be possible to find patterns in the data.
