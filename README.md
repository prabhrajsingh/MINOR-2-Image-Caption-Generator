# MINOR-2 - Image-Caption-Generator

Image captioning is an interesting problem, where you can learn both computer vision techniques and natural language processing techniques.

Deep Learning Photo Caption Generator and create an image caption generation model using Flicker 8K data. This model takes a single image as input and output the caption to this image.

To evaluate the model performance, we have used bilingual evaluation understudy BLEU. 

We will build the pipeline for our deep learning architecture in two phases:
    For the first phase, we use transfer learning to pre-process the raw images with a pre-trained CNN-based network. This takes the images as input and produces the  encoded image vectors that capture the essential features of the image. We do not need to train this network further.
  
  We then input these encoded image features, rather than the raw images themselves, to our Image Caption model. We also pass in the target captions corresponding to each encoded image. The model decodes the image features and learns to predict captions that match the target captions.
