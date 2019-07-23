
# TL;DR
## An end-to-end event extraction and summarization system. 
The project entitles "TL;DR" describes a large-scale automated system for extracting violent incidents relating to protests/riots and violence against civilians. A comprehensive architecture is outlined that can identify, categorize, summarize and perform entity slot filling against the target event types. Furthermore, an attempt is made to relate the recorded events to politics and elections taking place in the countries India, Indonesia, and Thailand. This allows a better
understanding of the driving factors for these events.

## Getting Started

### Step 1: Crawling news articles

News Please -

1. Install News Please.

2. Use config.cfg_mass, sitelist.hjson_mass to collect data for building classifier Model.

3. Use config_lib.cfg_live, sitelist_COUNTRYNAME.hjson (replace COUNTRYNAME with correcponding country) to crawl and clean Live news articles


### Step 2: Classification of the articles:

The following scripts are run in the same order as below:

1. **Classifier_Builder.ipynb** - A classifier that classifies events described in the news articles.
			      
2. **Doc2Vec_Classifier.ipynb** - Using Doc2Vec we built the classifier.

3. **TextRank.ipynb** - Performed TextRank and Coref Resolution on the text to extract keywords.
	            
		    
### Step 3: NER tagging and Summarization System-

sample_input.csv = Input file for the system. 
./output = Location where the output files are stored. 

1. **topic_modelling.ipynb** - Topic Modelling for extracting topics from the news article.
			   *Input - sample_input.csv*
			   *Output - ./output/topic_modelling.csv*

2. **extractor.ipynb** 	-  An extractor to extract named entities from the news article. 
			   *Input - sample_input.csv*
			   *Output - ./output/final_data_with_lat_and_long.csv*

3. **evaluation.ipynb**  -  The evaluation of our system.
			   *Input  - sample_input.csv* 
						 - ./output/extracted_data.csv
			   *Output for this script - ./output/ACLED_rouge_scores.txt
						  - *(Printing the scores for each category in the console).*

### Step 4: User Interface Setup -

1. Install Elastic search

2. Add Index CSE_635 as described in ElasticSearch_Index.txt to Elastic search.

3. Import Kibana dashboard and Visualizations from Kibana Admin console from KIbana_VIsualizations.json

4. Run Elasticsearch_Indexer.ipynb -  Jupyter notebook for Indexing articles into Elastic search
				      Input for this script - ./output/final_data_with_lat_and_long.csv

# Example:

## Summary of a news article:

*Patna Bihar India, Apr 4 ANI Congress workers created ruckus at the party office here on Thursday in protest against the denial of ticket to former party MP Nikhil Kumar from Aurangabad parliamentary constituency. The workers
also shouted the slogan 'Nikhil Kumar Zinadabad.' Kumar was also present in the office when the ruckus took place. Kumar had successfully contested from the seat in 2004 when the Congress fought in alliance with the RJD and the LJP. Kumar, a former Delhi Police Commissioner, unsuccessfully contested from Aurangabad in 2014 against BJP s Sushil Kumar
Singh.*

**Date**: 4/4/2019
**ranked_list_PERSON**: [{'Kumar': 1.0}, {'Patna Bihar': 0.625}, {'Nikhil': 1.0}]
**ranked_list_ORG**: [{'Congress': 1.0},{'Kumar': 1.0}, {'ANI': 1.0}]
**Location**: ['India', 'Aurangabad', 'Patna', 'Bihar', 'India', 'Lok', 'Sabha']
From the above example, we can see that for the ‘PERSON’ entity, terms like ‘Nikhil’ and ‘Kumar’ have been given higher weight than ‘Patna Bihar’.
The date tagged by our system is accurate because ‘April 4th’ in the text and the ‘Thursday’ correspond
to the same day. Similarly, for the ‘ORG’, the term ‘Congress’ has a higher weight
