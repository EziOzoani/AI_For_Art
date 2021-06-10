# AI_For_Art
[![made-with-python](https://img.shields.io/badge/Made%20with-Python-1f425f.svg)](https://www.python.org/)
[![made-with-Jupyter](https://img.shields.io/badge/Made%20with-Jupyter-1f425f.svg)](https://jupyter.org/try)





Style transfer is an optimisation problem, used to  minimisation the loss function. Taking two images (style image and x image ), the optimisation minimises the difference betweeen the images. It also makes use of zero shot or one shot learning, which is machine learning with very little data. 
The approached used is based on the paper A Neural Algorithm of [Artistic Style](https://arxiv.org/abs/1508.06576). Note: this ppaer used VGG-19 models for TensorFlow instead og VGG-16.


Network used is VGG16: it is an image classification convolutional network 
At each layer it apples a series of operations to the input image
Input image: matrix of values.

At each layer we have a stack of filters that are learned overtime
Filters: the filters are 3D vectors, which are a collection of matrics that are 2d, and the 3D is the rgb
At each of these filters, a matrix multiplication and then a summation operation occurs on te input image.
It acts as feture identifer
large number imples a feture is detected 
If not = zero.

It will output a feature map or an activation map (large matrix of values). We want to minimise the difference between our feature map and our content image.

#Input images
Content image: Image to modify 
Style image: we want to apply to content image
Mixed Image: empty, random nosie initilase dimage we will add to over time.

There is style loss and content loss and the combination of these using gradient value updates the mixed image.


#Dependecies 

- tensorflow
- matplotlib
- python 3

Running on Jypyter Notebook 
 

## Helper fucntions 
The following are used to handle image manipulation:

- Load the image: Loads an image and returns it as a numpy array of floating-points
- Save the image: The image is  numpy array with pixel-values between 0 and 255, which is saved as jpeg-file.
- Plot images: It plots the content, mixed and style-images.

## Loss Functions 

  - Mean Squared Error: The mean sqaured error is the average of the sqaure of the difference between the output feature map and our image.
                        The difference is subtracted, then squared and finally we excute a reduce mean.
                           
                        Reduce Mean: Finds the average of all vlaues inside of the matrix.
                        The smaller the means squared error, the closer you are to finding the line of best fit.
                        Given the input tensors (a, b), this function defines the mean squared error and outputs a scaler value.
    
  - Create Content Loss Function: Creates the loss-function for the content-image.  
                                    It is the Mean Squared Error of the feature activations in the given layers in the model, between the content-image and the mixed-image. 
                                    A minimised content-loss means that the mixed-image has feature activations in the given layers that are very similar to the activations of the content-image.
   
   - Gram Matrix: For the style image we want to measure which features in the style-layers activate simultaneously for the style-image, and then copy this activation-pattern to the mixed-image.
                  So we use the gram matrix, which is 4D tensor and it the matrix product between our initial matirix and then its transposed ( filpping it by 90 degrees ).
                  In the gram matrix we are measuring the correlations between our feature vectors after flattening the filter image into vectors
                  
                  If an entry in the Gram-matrix has a value close to zero then it means the two features in the given layer do not activate simultaneously for the given style-image, and vice versa.
                  If an entry in the Gram-matrix has a large value, then it means the two features do activate simultaneously for the given style-image. 
                  The creation a mixed-image that replicates this activation pattern of the style-image, is then needed.
             
   - Create Style Loss Fucntion: It creates the loss-function for the style-image. 
                                 It is similar to the content loss fucntion, but the Mean Squared Error for the Gram-matrices is used instead of the raw tensor-outputs from the layers.
                                
                                
   - Denoise Loss Function: It creates the loss-function for denoising the mixed-image, using the  [Total Variation Denoising](https://en.wikipedia.org/wiki/Total_variation_denoising) algorithm.
                            
                        
                           Total Variation Denoising: It shifts the image one pixel in the x- and y-axis and calculates the difference from the original image. 
                                                      It then takes the absolute value to ensure the difference is a positive number, and sums over all the pixels in the image. 
                      
     This creates a loss-function that can be minimised, allowing the suppression of some of the noise in the image e.g blurriness.
                           
  
                            
   
   
     
## - [ ]Style Transfer 
