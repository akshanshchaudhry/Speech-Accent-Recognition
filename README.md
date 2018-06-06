# Speech-Accent-Recognition
A deep learning model is developed which can predict the native country on the basis of the spoken english accent


1. Overview:

	Using audio samples from [The Speech Accent Archive] (http://accent.gmu.edu/), I wanted to show that a deep neural network can classify the native language of a speaker.

2. Dependencies:

  	* Python 3.5 (https://www.python.org/download/releases/2.7/)
 	  * Keras (https://keras.io/)
  	* Numpy (http://www.numpy.org/)
  	* BeautifulSoup (https://www.crummy.com/software/BeautifulSoup/)
   	* Pydub (https://github.com/jiaaro/pydub)
  	* Sklearn (http://scikit-learn.org/stable/)
  	* Librosa (http://librosa.github.io/librosa/)

3. Data:

	I started with the data from The Speech Accent Archive, a collection of more than 2400 audio samples from people for over 177 countries speaking the same English paragraph. 	The paragraph contains most of the consonants, vowels, and clusters of standard American English. It wasn’t useful to use the 9 audio samples from Finland.

	For the purpose of this project, I focused on countries with the most abundant audio 	samples, and the languages that have distinctly different origins. I chose to work with English, Arabic and Mandarin. 

4. Model:

•	Converted wav audio files into Mel Frequency Cepstral Coefficients graph.

•	The MFCC was fed into a 2-Dimensional Convolutional Neural Network (CNN) to predict the native language class.

5. Challenges & Solutions:

•	Computationally expensive: Used only 3 accents of distinctive origins.

• Small dataset: MFCCs were sliced into smaller segments. These smaller segments were fed into the neural network where predictions were made. Using an ensembling method, a majority vote was taken to predict the native language class.


6. Running Model:
  
  ├── src   
        ├── accuracy.py
        ├── fromwebsite.py
        ├── getaudio.py
        ├── getsplit.py
        ├── trainmodel.py
  ├── models  
       ├── cnn_model138.h5
  ├── logs  
       ├── events.out.tfevents.1506987325.ip-172-31-47-225
  └── audio

Note- Run all the python files as described below on the terminal

###### To download language metadata from [The Speech Accent Archive] (http://accent.gmu.edu/index.php) and download audio files:

1. Run fromwebsite.py to get language metadata and save data to bio_metadata.csv

Command: `python fromwebsite.py bio_metadata.csv mandarin english arabic`

2. Run getaudio.py to download audio files to the audio directory. All audio files listed in bio_metadata.csv will be downloaded.

Command: `python getaudio.py bio_metadata.csv`

###### To filter audio samples to feed into the CNN:

1. Edit the filter_df method in getsplit.py
    * This will filter audio files from bio_metadata.csv when calling trainmodel.py

###### To make predictions on audio files:

1. Run trainmodel.py to train the CNN

Command: `python trainmodel.py bio_data.csv model5`

  * Running trainmodel.py will save the trained model as model50.h5 in the model directory and output the results to the console.
  * This script will also save a TensorBoard log file into the logs directory.


7. Performance

	With the three languages classification, the model was able to predict the correct native language around 85% accuracy when given an English sample, 57% accuracy when given an Arabic sample, and an 87% when given a Mandarin sample.

|Act/Pred|English|Arabic|Mandarin|
|:-:|:-:|:-:|:-:|
|**English**|238|5|0|
|**Arabic**|23|27|0|
|**Mandarin**|5|10|30|

