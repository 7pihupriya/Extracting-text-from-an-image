# Extracting-text-from-an-image
## Objective : Detecting machine-readable-zones in a passport image

The MRZ region in passports or travel cards fall into two classes: 
Type 1 and Type 3. Type 1 MRZs are three lines, with each line containing 30 characters. 
The Type 3 MRZ only has two lines, but each line contains 44 characters. 
In either case, the MRZ encodes identifying information of a given citizen, including the type of passport, passport ID, issuing country, name, nationality, expiration date, etc.

MRZ detection using only basic image processing techniques such as thresholding, morphological operations, and contour properties. 
import our necessary packages. And have OpenCV installed already. We’ll also need imutils, my collection of convenience functions to make basic image processing operations with OpenCV easier. We can install imutils  using pip.

 Loads our original image from disk and resizes it to have a maximum height of 390 pixels.
 ![shanti](https://user-images.githubusercontent.com/53252686/86601213-a881ed00-bfbe-11ea-9037-24142ff444b9.jpeg)
 ###### Our original passport image that we are trying to detect the MRZ 
            
Load the image, resize it, and convert it to grayscale            

Gaussian blurring is applied to reduce high frequency noise. Smooth the image using a 5x5 Gaussian.
![grayscale_array](https://user-images.githubusercontent.com/53252686/86603311-79b94600-bfc1-11ea-9108-46e055da7bd8.jpeg)

 
