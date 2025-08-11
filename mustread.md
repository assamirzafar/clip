by John Robinson @johnrobinsn
Video Search
In this article, I'll describe a tiny video search engine and indexer that will let you search through a video with descriptive "natural language" queries and find matching frames of video. All the code is included in a Google Colab Notebook. So even if you don't have your own cuda-capable GPU, you can easily run the code yourself without setting up anything on your own computer.

OpenAI's CLIP model was one of the biggest advancements in computer vision last year. CLIP integrates both vision and language into a single multimodal model. This model was trained on 400 Million image/text pairs obtained by crawing the Internet. An image along with it's english language text caption is an example of an image/text pair. This approach allowed the CLIP team to leverage the Internet as a large source of "prelabeled data" without needing to manually label any of the images themselves. Another advantage to this approach is that english language captions typically encode much more about what is happening in the image than a simple class label like "dog" or "cat". This additional context allows the model to develop clusters of latent features within the model for abstract concepts across both images and text. This gives CLIP the ability to generalize to classes of objects that it hasn't been directly trained on.


https://www.storminthecastle.com/posts/video_search/

his proect's colab
https://colab.research.google.com/drive/1B5Chwhp2c6tUoP3lVybWjrHuQbuoxZDY?usp=sharing#scrollTo=iuD4yjd7D9wE
