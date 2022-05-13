# MINOR-2 - Image-Caption-Generator

Image captioning is an interesting problem, where you can learn both computer vision techniques and natural language processing techniques.

There are some well-known datasets that are commonly used for this type of problem. These datasets contain a set of image files and a text file that maps each image file to one or more captions. Each caption is a sentence of words in a language.
For our demo, we will use the Flickr8K dataset (images, text). This is a reasonably sized dataset that contains about 8000 images, which is sufficient to train our model without requiring a huge amount of RAM and disk space.

After downloading this to a ‘dataset’ folder, we see that it consists of three parts:

   **Image** files in the ‘Flicker8k_Dataset’ folder: This folder contains roughly 8000 .jpg files eg. ‘1000268201_693b08cb0e.jpg’
    
   **Captions** in the ‘Flickr8k.token.txt’ file in the main folder: It contains captions for all the images. Because the same image can be described in many different ways, there are 5 captions per image.

   **List of Training, Validation, and Test Images**   in a set of .txt files in the main folder: ‘Flickr_8k.trainImages.txt’ contains the list of image file names to be used for training. Similarly, there are files for validation and test.

Each line in the Captions file represents one caption. It contains two columns separated by a Tab. The format of each line is:
    “<image file>#i <caption>”, where 0≤i≤4 for each of the 5 captions.
    eg. “1000268201_693b08cb0e.jpg#1 A girl going into a wooden building .”**
    
**Training data pipeline**
We will build the pipeline for our deep learning architecture in two phases.

For the first phase, we use transfer learning to pre-process the raw images with a pre-trained CNN-based network. This takes the images as input and produces the encoded image vectors that capture the essential features of the image. We do not need to train this network further.

Attention helped the model focus on the most relevant portion of the image as it generated each word of the caption.
   
We then input these encoded image features, rather than the raw images themselves, to our Image Caption model. We also pass in the target captions corresponding to each encoded image. The model decodes the image features and learns to predict captions that match the target captions.
    
    
For the Image Caption model, the training data consists of:

The features (X) are the encoded feature vectors
The target labels (y) are the captions

**Pre-process Images**
We will use a pre-trained Inception model which is a well-known Image Classification model with excellent performance. This model consists of two sections:

The first section consists of a sequence of CNN layers that progressively extract the relevant features from the image to produce a compact feature map representation.
The second section is the Classifier that consists of a sequence of Linear layers. It takes the image feature map and predicts a class (eg. dog, car, house, etc) to which the feature belongs.
  
**For our Image Caption model, we need only the image feature maps, and do not need the Classifier.**
    
To prepare the training data in this format, we will use the following steps:
    Load the Image and Caption data
    Pre-process Images
    Pre-process Captions
    Prepare the Training Data using the Pre-processed Images and Captions
    
    
**Prepare Captions**
Each caption consists of an English sentence. To prepare this for training, we perform the following steps on each sentence:

**Clean** it by converting all words to lower case and removing punctuation, words with numbers and short words with a single character.

**Add** ‘<startseq>’ and ‘<endseq>’ tokens at the beginning and end of the sentence.
    
**Tokenize** the sentence by mapping each word to a numeric word ID. It does this by building a vocabulary of all the words that occur in the set of captions.

**Extend** each sentence to the same length by appending padding tokens. This is needed because the model expects every data sample to have the same fixed length.
    
  
**Image Caption Model with Attention**
The model consists of four logical components:

**Encoder**: since the image encoding has already been done by the pre-trained Inception model, the Encoder here is very simple. It consists of a Linear layer that takes the pre-encoded image features and passes them on to the Decoder.
  
**Sequence Decoder**: this is a recurrent network built with GRUs. The captions are passed in as the input after first going through an Embedding layer.
  
**Attention**: as the Decoder generates each word of the output sequence, the Attention module helps it to focus on the most relevant part of the image for generating that word.
  
**Sentence Generator**: this module consists of a couple of Linear layers. It takes the output from the Decoder and produces a probability for each word from the vocabulary, for each position in the predicted sequence.

  
NAME: NIHARIKA AGRAWAL, PRABHRAJ SINGH, PRADUMN NATHAWAT
  
BRANCH: B.Tech CSE AI&ML
  
SAPID: 500075359, 500076519, 500075307
  
BATCH: 4
