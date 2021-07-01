# Self-Driving-Car

**Data Procuring:**
1.	We obtain path to images and also we obtain angles.
Data Pre-processing
1.	We convert our angles to radians, as suggested by Nvidia architecture we are using steering angle in radians rather than in degree.
Split the data:
1.	We now split the data in 80:20 ratio. After splitting the data we have 36324 images in train data and 9082 images in validation data
Base Model:
Description: When we obtain our steering angle in radians and plot them we see that our steering angles are centred around 0. Also, in problem statement we have to come up with an architecture which can help us predict steering angles. Thus, it is a regression problem. In regression we have studies variation around the mean, in our case we can consider mean angle as our base model prediction in explanation we can say that initially we are taking prediction of every input to be 0. Also, whatever model we build now, has to be better than this.
With our base model we have following metrics values:
Test_MSE(MEAN):0.191127
Test_MSE(ZERO):0.190891

**Resizing Images:**
Initially our images are of size 455(width)*256(height) pixels and we have resized the image to 200*66. We initially obtained the height required to cover the pixels which covers the road, which is 150 pixels. 

**X_train** is the list which contains the array of all these images. Similarly, X_val is the list which contains the array of the images. We dump the X_traina and X_val to pickle files. After loading them we resize them in the following pattern rows*columns*channels. Where number of rows=66,columns=200 and number of channels=3

**Building Model with Nvidia Architecture:**
Description: Our Architecture consist of 5 Convolutions and 3 fully connected layers. Out of 5, 3 are 5X 5 convolution of size 24,36 and 48. Whereas the other two are 3X3 convolutions of size 64,64. The feature map obtained after convolution operation is 1 X 18 X 64. The output from the feature map is then passed through the dense network where we have 4 dense layers of 1164,100,50 and 10 respectively.

Note: The 5X5 convolutions are performed with a stride of 2, whereas 3X3 convolutions are non strided.

**Activation Function:**
We want the activation function that gives output in the range of [-pi,pi], we know tan inverse(atan) function gives output in the range of [-pi/2,pi/2], thus we multiply it by 2 to obtain the output in the required range.

Model optimization:
We use Adam optimizer in this case which has initial learning rate of 0.0001. We train the weights of our network to minimize the mean-squared error between the steering command output by the network

**Results:** The least validation loss that we get is 0.1907 which is marginally better than our dummy model.


