TL;DR - An end-to-end event extraction and summarization system.

News event Extraction and Classification -

The following scripts are run in the same order as below:

1. Classifier_Builder.ipynb - Jupyter notebook for building classifier for KNN, Naive Bayes and Logistic regression
			      Input for this script - Final_Data (Directory)
			      Output for this script - TFIDF_Vector.pickle, phasr_4_model.sav (Classifier model)

2. Doc2Vec_Classifier.ipynb - Jupyter notebook for building classifier for Doc2Vec
			      Input for this script - Final_Data (Directory)
			      Output for this script - phasr_4_model.sav (Classifier model)

3. Live_Data_Classifier.ipynb - Jupyter notebook for building classifier for Doc2Vec
			        Input for this script - Final_Data (Directory)
			        Output for this script - phasr_4_model.sav (Classifier model)

4. TextRank.ipynb - Jupyter notebook for calculating keywords using TextRank and Coreference
	            Input for this script - Distributed_data_*.csv (Final CSV file containing data for all countries)
	            Output for this script - Distributed_data_textrank_*.csv (Final CSV file containing data with textrank keywords calculated)

News Please -

1. Install News Please.

2. Use config.cfg_mass, sitelist.hjson_mass to collect data for building classifier Model.

3. Use config_lib.cfg_live, sitelist_COUNTRYNAME.hjson (replace COUNTRYNAME with correcponding country) to crawl and clean Live news articles

NER tagging and Summarization -

sample_input.csv = Input file for the system. 
./output = Location where the output files are stored. 


The following scripts are run in the same order as below:
1. topic_modelling.ipynb - Jupyter notebook for topic modeling
			   Input for this script - sample_input.csv
			   Output for this script - ./output/topic_modelling.csv

2. extractor.ipynb 	-  Jupyter notebook for extracting all entities. 
			   Input for this script - sample_input.csv
			   Output for this script - ./output/final_data_with_lat_and_long.csv

3. evaluation.ipynb     -  Jupyter notebook for the evaluation of our system.
			   Input for this script - sample_input.csv 
						 - ./output/extracted_data.csv
			   Output for this script - ./output/ACLED_rouge_scores.txt
						  - (Printing the scores for each category in the console).

User Interface Setup -

1. Install Elastic search

2. Add Index CSE_635 as described in ElasticSearch_Index.txt to Elastic search.

3. Import Kibana dashboard and Visualizations from Kibana Admin console from KIbana_VIsualizations.json

4. Run Elasticsearch_Indexer.ipynb -  Jupyter notebook for Indexing articles into Elastic search
				      Input for this script - ./output/final_data_with_lat_and_long.csv