<!-- .slide: data-background-image="images/RH_NewBrand_Background.png" -->
## The Headliner <!-- {.element: class="course-title"} -->
### Advanced ML Operations <!-- {.element: class="title-color"} -->
AI500 <!-- {.element: class="title-color"} -->






## 🥅What our goal is🥅

- We want to find out if a song will be a hit…
- by sending in some song characteristics…
- and getting a probability for each of the 72 countries where it most likely will be popular



## 😣 Pain Point 😣

- Some users are complaining that the inputs for seeing where a song will be popular are not intuitive, and that they don’t understand the output.
- What’s so hard with just looking in our index at https://jukebox-records.com/jukebot/info/tools/details/countries/indexes and seeing what country #51 is….?
- But, the boss says the user is always right so I guess we have to fix it…
- We briefly added the pre-and-post processing steps in our client, but John updated the model 15 minutes after that and now the predictions make no sense at all.



## Slide 5

![Image](images/6-the-headliner/slide_5_image_0.png) <!-- {.element: class="image-no-shadow image-medium"} -->



## ❓ Quiz ❓

- Why do we want to use pre-and-post processing?
- Because AI models get stage fright and need a warm-up and cool-down routine.
- To clean and transform data before training/serving, and to ensure model outputs are properly formatted for real-world use.
- To make the AI feel special, like a spa day before and after hard work.
- Because without it, the AI might start speaking only in riddles and ancient prophecies.



## We don’t just work with raw data

- Pre-processing
- Post-processing
- 15
- AI predicting dogs name
- Benji
- AI predicting dogs name

![Image](images/6-the-headliner/slide_7_image_3.png) <!-- {.element: class="image-no-shadow image-medium"} -->
![Image](images/6-the-headliner/slide_7_image_4.png) <!-- {.element: class="image-no-shadow image-medium"} -->
![Image](images/6-the-headliner/slide_7_image_9.png) <!-- {.element: class="image-no-shadow image-medium"} -->
![Image](images/6-the-headliner/slide_7_image_12.png) <!-- {.element: class="image-no-shadow image-medium"} -->
![Image](images/6-the-headliner/slide_7_image_13.png) <!-- {.element: class="image-no-shadow image-medium"} -->
![Image](images/6-the-headliner/slide_7_image_16.png) <!-- {.element: class="image-no-shadow image-medium"} -->
![Image](images/6-the-headliner/slide_7_image_17.png) <!-- {.element: class="image-no-shadow image-medium"} -->
![Image](images/6-the-headliner/slide_7_image_18.png) <!-- {.element: class="image-no-shadow image-medium"} -->
![Image](images/6-the-headliner/slide_7_image_21.png) <!-- {.element: class="image-no-shadow image-medium"} -->
![Image](images/6-the-headliner/slide_7_image_23.png) <!-- {.element: class="image-no-shadow image-medium"} -->
![Image](images/6-the-headliner/slide_7_image_24.png) <!-- {.element: class="image-no-shadow image-medium"} -->
![Image](images/6-the-headliner/slide_7_image_25.png) <!-- {.element: class="image-no-shadow image-medium"} -->
![Image](images/6-the-headliner/slide_7_image_27.png) <!-- {.element: class="image-no-shadow image-medium"} -->
![Image](images/6-the-headliner/slide_7_image_28.png) <!-- {.element: class="image-no-shadow image-medium"} -->
![Image](images/6-the-headliner/slide_7_image_29.png) <!-- {.element: class="image-no-shadow image-medium"} -->



## KServe Transformers

- Processing not packaged with the model
- Processing packaged with the model
- This we can do with our modelcar.
- But we still need to use the artifacts somehow.

![Image](images/6-the-headliner/slide_8_image_5.png) <!-- {.element: class="image-no-shadow image-medium"} -->
![Image](images/6-the-headliner/slide_8_image_6.png) <!-- {.element: class="image-no-shadow image-medium"} -->



## KServe Transformers

- Kserve allows you to custom-define pre-and-post steps to your model

![Image](images/6-the-headliner/slide_9_image_2.png) <!-- {.element: class="image-no-shadow image-medium"} -->


Note:
The pre-and-post steps are defined in Python with KServe SDK. The pre-and-post steps can be inside the same pod as the model runtime or in a separate pod.



## 😣 Pain Point 😣

- I think… I think we are popping off!
- We are getting so much traffic!
- Wait… we are getting so much traffic…?
- “PETER HOW IS THE MODEL DOING??”



## Models as stateless microservices

- MODEL
- MODEL SERVICE
- MODEL
- MODEL
- APP
- SCALE HORIZONTALLY
- PHASED ROLLOUTS
- MODEL
- MODEL*
- MODEL1
- MODEL2
- MODEL3
- MULTIPLE TRIALS
- APP
- APP


Note:
ML model stateless microservice called through an API, returns prediction on sample wrapped by container orchestrated by OpenShift built-in load balancing automatic scaling rolling updates to prevent downtime service mesh for A/B testing & shadow scoring



## Remember to update your MLOps Venn Diagram 🤗

- New tasks:
- Pre-and-post process data
- Manage deployments

![Image](images/6-the-headliner/slide_15_image_1.png) <!-- {.element: class="image-no-shadow image-medium"} -->