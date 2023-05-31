# Assignment 4 - Using finetuned transformers via HuggingFace
This is the fourth assignment out of five in the Language Analytics course

# Contribution
This assignment was started along with my fellow students and later modified and finished by myself. I also looked to the notebooks from class that handled examples of ```Huggingface``` pretrained models and how to use them in a pipeline. 

# Ross' instructions
In previous assignments, you've done a lot of model training of various kinds of complexity, such as training document classifiers or RNN language models. This assignment is more like Assignment 1, in that it's about *feature extraction*.

For this assignment, you should use ```HuggingFace``` to extract information from the *Fake or Real News* dataset that we've worked with previously.

You should write code and documentation which addresses the following tasks:

- Initalize a ```HuggingFace``` pipeline for emotion classification
- Perform emotion classification for every *headline* in the data
- Assuming the most likely prediction is the correct label, create tables and visualisations which show the following:
  - Distribution of emotions across all of the data
  - Distribution of emotions across *only* the real news
  - Distribution of emotions across *only* the fake news
- Comparing the results, discuss if there are any key differences between the two sets of headlines

## Tips
- I recommend using ```j-hartmann/emotion-english-distilroberta-base``` like we used in class.
- Spend some time thinking about how best to present you results, and how to make your visualisations appealing and readable.

# Data
The data used for this assignment is once again the [_Fake or Real News_](https://www.kaggle.com/datasets/jillanisofttech/fake-or-real-news) dataset provided by Kaggle user Jillani Soft Tech. When unzipped, the dataset consists of a CSV with 4 columns: index, title, text and label. This assignment works with the titles under the labels column in the CSV in order to use a pretrained Huggingface model. The dataset will be unzipped from within the _emotion_class.py_ script.

# Packages
* ```pandas``` is used in the process of reading CSV's to dataframe and also for the purpose of concatenating 
* ```matplotlib``` is used to make interpretable plots
* ```os``` is used to navigate paths
* ```transformers``` is used to import pipeline
* ```TensorFlow``` is used in order for everything to run
* ```zipfile``` is used to unzip the data 

# Methods
For this assignment there is a single python script that completes the task at hand. It is called _emotion_class.py_ and is located in the _src_ folder. The script starts by unzipping the data into the _in_ folder. Then it loads and filters the data by only selecting the "label" column. Then it proceeds to classify emotions for every line in "labels" via the ```j-hartmann/emotion-english-distilroberta-base``` from ```HuggingFace```. Then a for loop is initiated. It iterates through the data and appends emotion count. Then the script proceeds to use ```matplotlib``` to create bar plots that display the emotion distribution for all the titles, all the fake news titles and all the real news titles. For this part of the code, i consulted the following [link](https://pythonbasics.org/matplotlib-bar-chart/) for insight into how to set up a bar plot. The bar plots are saved to the folder called _figs_. The script also saves CSV files for each of the three previously mentioned subset of data. Those are located in the _out_ folder

# Discussion of results 
Diving into the emotion distribution, it is clear that what we might generalize in advance is the case for the "anger" and "disgust" emotions. They are both more abundant in the Fake news titles than in the Real new titles. However one thing that surprises me is that the Fake news titles seem to be more joyful than the real ones. However when you consider it, it is of course easier to cover up for the negative details of a story if a journalist already has decided to write untruthful articles. The fact that the "surprise" emotion also is more frequent in the Fake news titles doesnt surprise me since news media often rely on shock factor in generating as many clicks as possible. This is a point that i base on the contemporary media trajectory of click bait based news.

# Usage
* First you need to download the data from this [Kaggle](https://www.kaggle.com/datasets/jillanisofttech/fake-or-real-news) and make sure to put it into the _in_ folder.
* Then you run ```bash setup.sh``` from the command line to install packages and create a virtual environment
* !OBS! i had sometimes [issues](https://www.datasciencelearner.com/modulenotfounderror-no-module-named-transformers-solved/) with the installment of transformers, so run this before running the script to be safe: ```pip3 install transformers```
* Run ```source ./assignment4_env/bin/activate``` to activate the virtual environment
* Then run the script ```python3 src/emotion_class.py```. The data will be unzipped into the correct location as the first thing from within the script
* The output of the script are located in two different folders. The bar plots are located in the _figs_ folder while the CSV's are located in the _out_ folder
