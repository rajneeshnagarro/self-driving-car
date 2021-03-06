## **Traffic Sign Recognition**

---

**Build a Traffic Sign Recognition Project**

The goals / steps of this project are the following:
* Load the data set (see below for links to the project data set)
* Explore, summarize and visualize the data set
* Design, train and test a model architecture
* Use the model to make predictions on new images
* Analyze the softmax probabilities of the new images
* Summarize the results with a written report

## Rubric Points
###Here I will consider the [rubric points](https://review.udacity.com/#!/rubrics/481/view) individually and describe how I addressed each point in my implementation.  

---
**Writeup / README**

1. Here is a link to my [project code](https://github.com/rajneeshnagarro/self-driving-car/blob/master/CarND-Traffic-Sign-Classifier/Traffic_Sign_Classifier.ipynb)

**Data Set Summary & Exploration**

I used the numpy library to calculate summary statistics of the traffic signs data set. Here is a basic summary of my data set:

* The size of training set is 34799
* The size of the validation set is 12630
* The size of test set is 4410
* The shape of a traffic sign image is (32, 32, 3)
* The number of unique classes/labels in the data set is 43

** Exploratory visualization of the data set 

* I pulled in random images and labled them with the correct names in reference with the CSV file to their respective ids.

![Random Images](https://github.com/rajneeshnagarro/self-driving-car/blob/master/CarND-Traffic-Sign-Classifier/images/writeup_image1.png)

* Then, I plot the occurence of each image class to get an idea of how the data is distributed. Here is a bar graph depicting the same:

![Image Classes - Data Distribution](https://github.com/rajneeshnagarro/self-driving-car/blob/master/CarND-Traffic-Sign-Classifier/images/writeup_image2.png)

### Design and Test a Model Architecture

As a first step, I decided to convert the images to grayscale because it remove the extra noise from the images.

Here is an example of a traffic sign images after grayscaling.

![Images after grayscale](https://github.com/rajneeshnagarro/self-driving-car/blob/master/CarND-Traffic-Sign-Classifier/images/writeup_image3.png)

As a last step, I normalized the image data because it helps in speed of training and performance. I tried different normalization functions and then settled on one which gave me better performance.

Here is an example of a normaized image:

![Normalized images](https://github.com/rajneeshnagarro/self-driving-car/blob/master/CarND-Traffic-Sign-Classifier/images/writeup_image4.png)

#### 2. Describe what your final model architecture looks like including model type, layers, layer sizes, connectivity, etc.) Consider including a diagram and/or table describing the final model.

My final model consisted of the following layers:

| Layer         		|     Description	        					| 
|:---------------------:|:---------------------------------------------:| 
| Input         		| 32x32x3 RGB image   							| 
| Convolution 5x5     	| 2x2 stride, same padding, outputs 28x28x6 	|
| RELU					|												|
| Max pooling	      	| 2x2 stride,  outputs 14x14x6 				|
| Convolution 5x5	    | 2x2 stride, valid padding, outputs 10x10x16      									|
| RELU					|												|
| Max pooling	      	| 2x2 stride,  outputs 5x5x16 				|
| Convolution 1x1	    | 2x2 stride, valid padding, outputs 1x1x412      									|
| RELU					|												|
| Fully connected		| input 412, output 120     									|
| RELU					|												|
| Dropout				| 50% keep        									|
| Fully connected		| input 120, output 84     									|
| RELU					|												|
| Dropout				| 50% keep        									|
| Fully connected		| input 84, output 43     									|

#### 3. Describe how you trained your model. The discussion can include the type of optimizer, the batch size, number of epochs and any hyperparameters such as learning rate.

* To train the model, I used a LeNet which was already provided. 
* Additionally, I used the AdamOptimizer with a learning rate of 0.00098. 
* The epochs used was 30 while the batch size was 100. 
* I was able to get around 94-95% accuracy with no changes on the test set.
* I think that better accuracy can be achieved if more data set images are generated.

#### 4. Describe the approach taken for finding a solution and getting the validation set accuracy to be at least 0.93. Include in the discussion the results on the training, validation and test sets and where in the code these were calculated. Your approach may have been an iterative process, in which case, outline the steps you took to get to the final solution and why you chose those steps. Perhaps your solution involved an already well known implementation or architecture. In this case, discuss why you think the architecture is suitable for the current problem.

My final model results were:
* training set accuracy of 0.932
* validation set accuracy of 0.999 
* test set accuracy of 0.957 (max)

If an iterative approach was chosen:
* What was the first architecture that was tried and why was it chosen?
I used the similar architecture taught by the Udacity instructors in the videos. It was choosen because I was getting the accuracy which was expected as result. 
* What were some problems with the initial architecture?
I faced fundamental problem of learning the architecture first and then finding out why grayscale and normalization help in getting better results. Also, I had to go through the videos and links to outside material to make it run beyond the default architecture provided. For example, some of the tutorial explained dropout is better if you have small data. Hence, rather than having more, I concentrated on using dropout on small data set.
* How was the architecture adjusted and why was it adjusted? Typical adjustments could include choosing a different model architecture, adding or taking away layers (pooling, dropout, convolution, etc), using an activation function or changing the activation function. One common justification for adjusting an architecture would be due to overfitting or underfitting. A high accuracy on the training set but low accuracy on the validation set indicates over fitting; a low accuracy on both sets indicates under fitting.
I had to adjust my architecture because of low accuracy. I added an extra convolution layer and then added dropout to get the desired accuracy.
* Which parameters were tuned? How were they adjusted and why?
I tuned Epoch, learning rate, batch size and also set drop out probability parameters. Epoch and batch size was adjusted because I was getting the desired accuracy. Dropout allowed me to achieve the output with the same data.
* What are some of the important design choices and why were they chosen? For example, why might a convolution layer work well with this problem? How might a dropout layer help with creating a successful model?
I used Dropout in my architecture. Dropout is a super technique for regularization so that my network is not relying upon any given activation and avoid overfitting. To make it learn different representations, I used this technique so that some of the information still remain.

#### 1. Choose five German traffic signs found on the web and provide them in the report. For each image, discuss what quality or qualities might be difficult to classify.

Here are the German traffic signs that I found on the web:

![alt text](https://github.com/rajneeshnagarro/self-driving-car/blob/master/CarND-Traffic-Sign-Classifier/new_german_sign_images/B.png) ![alt text](https://github.com/rajneeshnagarro/self-driving-car/blob/master/CarND-Traffic-Sign-Classifier/new_german_sign_images/C.png) ![alt text](https://github.com/rajneeshnagarro/self-driving-car/blob/master/CarND-Traffic-Sign-Classifier/new_german_sign_images/D.jpg) 
![alt text](https://github.com/rajneeshnagarro/self-driving-car/blob/master/CarND-Traffic-Sign-Classifier/new_german_sign_images/E.jpg) ![alt text](https://github.com/rajneeshnagarro/self-driving-car/blob/master/CarND-Traffic-Sign-Classifier/new_german_sign_images/F.png)
![alt text](https://github.com/rajneeshnagarro/self-driving-car/blob/master/CarND-Traffic-Sign-Classifier/new_german_sign_images/G.jpg)

I first had to resize these images. Then I grayscaled and normalized these images so that they can be fed to trained model to get the accurate results. 

#### 2. Discuss the model's predictions on these new traffic signs and compare the results to predicting on the test set. At a minimum, discuss what the predictions were, the accuracy on these new predictions, and compare the accuracy to the accuracy on the test set (OPTIONAL: Discuss the results in more detail as described in the "Stand Out Suggestions" part of the rubric).

#### 3. Describe how certain the model is when predicting on each of the five new images by looking at the softmax probabilities for each prediction. Provide the top 5 softmax probabilities for each image along with the sign type of each probability. (OPTIONAL: as described in the "Stand Out Suggestions" part of the rubric, visualizations can also be provided such as bar charts)

Here are the results of the prediction:

When I look at the top 3 results, I see that my model predicts first three images with realy high probability. For the, fourth and fifth images my model is unsure or worse than first three. Since for the unsure images, there is no correct class in given classes, my model could not predict in top 3(these classes does not exist in the training data)

The model was able to correctly guess 3 of the 5 traffic signs, which gives an accuracy of 60%. This compares favorably to the accuracy on the test set of images provided.

