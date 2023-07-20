# Lyrics_Generation
Train a neural net to generate lyrics based on the provided melody.

The melodies are stored in .mid (MIDI files) and contain various types of information – notes, the instruments used etc.
Analysis of Midi files using the [Pretty_Midi library](https://github.com/craffel/pretty-midi/tree/main)


# Description:
During each step of the training phase, our architecture receives as input one word of the lyrics.
Words are to represented using the Word2Vec representation that can be found online (300 entries per term, as learned in class).
The task of the network is to predict the next word of the song’s lyrics. Please see the figure 1 for an illustration. You may use any loss function 


# Model Architecture:
 LSTM with dropout (rate 0.2) & dense layer with softmax activation function.
Compilation optimizer: Adam
Loss : categorical_crossentropy

![image](https://github.com/Habler-code/Lyrics_Generation/assets/69906239/83d61b7e-7e21-4bab-9d92-96267b7af17a)

# Melody Strategies:

We tokenised each song’s words, and further cleaned them by removing apostrophes.	They were then represented by a vector of length 300 from Google’s word2vec-google-news-300 (3 million 300-dimension English word vectors). Any words that were present in the lyrics but not in word2vec-google-news-300 were removed.
In addition, we removed non alphanumeric characters such; for example:
Is’nt -> isnt  
Melody strategy 1: We chose to create a notes window that advances every time a word is predicted by the model. We implemented this by taking the first 10 instruments in the melody, and then taking each instrument’s first 10 note pitches. We add those 100 notes to the vector representation of the first word and predict the second word. The notes input is padded with zeros when necessary. We then pair the next 10 notes with the second word to predict the third, and so forth.


# Melody strategy 2: 

We chose to create a chroma window that advances every time a word is predicted by the model. We divided the melody into as many parts as there are words in the song do discretise the continuous chroma frequencies. We then have a vector of size 12 representing the chroma key. We add the chroma to the vector representation of the first word and predict the second word. We then pair the next chroma key with the second word to predict the third, and so forth.

# Prediction Loop:

![image](https://github.com/Habler-code/Lyrics_Generation/assets/69906239/ef35610e-f4bd-4392-aa26-8e222b58221d)

