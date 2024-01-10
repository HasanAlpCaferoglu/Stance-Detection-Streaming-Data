# STANCE DETECTION (ONLINE: STREAMING DATA)


### Authors:
Hasan Alp Caferoğlu
Ann Neşe Rende
Ekrem Polat

## Contents

In this part, the contents of the files are going to be explained briefly
- T5-Text Translation
- DistilBERT and LSTM
- LSTM with GloVe embeddings
- DistilBERT fine-tune
- DistilBERT with stream data

### T5-Text Translation
We utilized the XStance dataset in our project. However, the XStance dataset has sentences in German and French, so we need to translate them into English. Firstly, we uploaded our dataset to Google Drive and gave a path in Google Colab. Then, we eliminated unnecessary columns from the dataset. Since the translation process takes too long, we only take 10,000 data from the dataset. Finally, this code utilizes two pre-trained T5 models, French to English and German to English, to achieve this translation. Ultimately, we export the translated content as a CSV file for implementation.

#### Data Preprocessing
The following codes utilize the same data preprocessing. We first uploaded our dataset to Google Drive and gave a path in Google Colab. Then, we cleaned the dataset by removing mentions and #SemEval hashtags. Finally, we shuffled the dataset.


### DistilBERT and LSTM
Since this code includes DistilBERT and LSTM, it contains many parameters. Therefore, we used 12,000 rows from our dataset to avoid memory issues. Firstly, we tokenized our inputs with the DistilBERT tokenizer. Secondly, we extracted embeddings from tokenized inputs using a pre-trained DistilBERT model. In the next step, we formed our network containing embedding layers from DistilBERT, LSTM, and Dense layers. Finally, we trained our model, observed performance metrics, and evaluated our model on the test dataset. We also conducted several experiments by modifying both model structure and hyperparameters.


### LSTM with GloVe embeddings
In order to solve the memory issue and train the model with more data, we utilize word embeddings from GloVe. We add some helper functions to read GloVe embeddings from the file, load them to a dictionary, and create an embedding matrix which will be the input to LSTM. This time, instead of a DistilBERT tokenizer, we utilize a tokenizer from Keras. Moreover, we replace the Input layer in the bidirectional LSTM with an Embedding layer with the modified vector dimensions.

### DistilBERT fine-tune
After the data preprocessing part, we tokenized our inputs using an AutoTokenizer from the transformers library of Hugging Face. Then, we fine-tuned the DistilBERT model using the Hugging Face Training API. We plotted training performance metrics and evaluated the model on the test dataset. Also, we deployed our model to HuggingFace to use it in the streaming feature.

### DistilBERT with stream data
In this code, we utilized our DistilBERT model deployed to HuggingFace in the 4th step. We used different parts of data as a stream. Firstly, we fed into the stream data to our model. If the accuracy of the data is below 50%, we updated our model by retraining our model with stream data. We do not update the model if the accuracy is above 50%. This code includes several experiments with different stream data. In the end, we used 8,000 rows from XStance as 8 portions stream and observed none of them required updating the model.



