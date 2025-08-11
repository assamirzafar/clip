by John Robinson @johnrobinsn (only first two links are by him)
Video Search 

In this article, I'll describe a tiny video search engine and indexer that will let you search through a video with descriptive "natural language" queries and find matching frames of video. All the code is included in a Google Colab Notebook. So even if you don't have your own cuda-capable GPU, you can easily run the code yourself without setting up anything on your own computer.

OpenAI's CLIP model was one of the biggest advancements in computer vision last year. CLIP integrates both vision and language into a single multimodal model. This model was trained on 400 Million image/text pairs obtained by crawing the Internet. An image along with it's english language text caption is an example of an image/text pair. This approach allowed the CLIP team to leverage the Internet as a large source of "prelabeled data" without needing to manually label any of the images themselves. Another advantage to this approach is that english language captions typically encode much more about what is happening in the image than a simple class label like "dog" or "cat". This additional context allows the model to develop clusters of latent features within the model for abstract concepts across both images and text. This gives CLIP the ability to generalize to classes of objects that it hasn't been directly trained on.

https://www.storminthecastle.com/posts/video_search/

his proect's 
colab https://colab.research.google.com/drive/1B5Chwhp2c6tUoP3lVybWjrHuQbuoxZDY?usp=sharing#scrollTo=iuD4yjd7D9wE


# Contrastive Language-Image Forensic Search


## Overview

CLIFS is a proof-of-concept for free text searching through videos for video frames with matching contents.
This is done using [OpenAI's CLIP](https://openai.com/blog/clip/) model, which is trained to match images with the corresponding captions and vice versa.
The searching is done by first extracting features from video frames using the CLIP image encoder and then
getting the features for the search query through the CLIP text encoder. The features are then matched by similarity
and the top results are returned, if above a set threshold.

To allow easy use of the CLIFS backend, a simple web server running django is used to provide an interface to the search engine. 


## Examples
To give an idea of the capability of this model, a few examples are shown below, with the search query in bold and the result below.
These search queries are done against the 2 minute Sherbrooke video from the [UrbanTracker Dataset](https://www.jpjodoin.com/urbantracker/dataset.html).
Only the top image result for each query is shown. Note that the model is in fact quite capable of OCR.

#### A truck with the text "odwalla"
![alt text](media/odwalla.jpg)
======

#### A white BMW car
![alt text](media/bmw.jpg)
======

#### A truck with the text "JCN"
![alt text](media/jcn.jpg)
======

#### A bicyclist with a blue shirt
![alt text](media/bicyclist.jpg)
======

#### A blue SMART car
![alt text](media/smart.jpg)
======

## Setup
1. Run the setup.sh script to setup the folders and optionally download a video file for testing:
```sh
./setup.sh
```

2. Put your own video files that you want to index in the `data/input` directory

3. Build and start the search engine and web server containers through docker-compose:
```sh
docker-compose build && docker-compose up
```

Optionally, a docker-compose file with GPU support can be used if the host environment has a NVIDIA GPU and is setup for docker GPU support:

```sh
docker-compose build && docker-compose -f docker-compose-gpu.yml up
```
 
4. Once the features for the files in the `data/input` directory have been encoded, as shown in the log, navigate to [127.0.0.1:8000](http://127.0.0.1:8000) and search away.



