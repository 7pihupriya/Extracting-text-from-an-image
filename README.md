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

## Gaussian Blurring

Gaussian blurring is applied to reduce high frequency noise. Smooth the image using a 5x5 Gaussian.

![grayscale_array](https://user-images.githubusercontent.com/53252686/86603311-79b94600-bfc1-11ea-9108-46e055da7bd8.jpeg)

## Blackhat Operation

We then apply a blackhat morphological operation to the blurred, grayscale image.A blackhat operator is used to reveal dark regions against light backgrounds.Since the passport text is always black on a light background. Below you can see the output of applying the blackhat operator:

![blackhat](https://user-images.githubusercontent.com/53252686/86604332-dec16b80-bfc2-11ea-82bf-d4ac0c186f62.jpg)
###### Applying the blackhat morphological operator reveals the black MRZ text against the light passport background.

The next step is to try to detect the actual lines of the MRZ:
First, we apply a closing operation using our rectangular kernel. This closing operation is meant to close gaps in between MRZ characters. We then apply thresholding using Otsu’s method to automatically threshold the image:

![rectthresh](https://user-images.githubusercontent.com/53252686/86604950-abcba780-bfc3-11ea-8825-5903aaea0d21.jpg)
###### Applying a closing operation using a rectangular kernel to close gaps in between the MRZ characters

Here we perform another closing operation, this time using our square kernel. This kernel is used to close gaps between the individual lines of the MRZ.A series of erosions  are then performed to break apart connected components that may have been joined during the closing operation.

![sqthresh](https://user-images.githubusercontent.com/53252686/86605472-6065c900-bfc4-11ea-9c7f-4a1366512013.jpg)
###### A second closing operation is performed, this time using a square kernel to close the gaps in between individual MRZ lines.

## Contours

The last step is to find the contours of our thresholded image. We then take these contours and sort them based on their size in descending order and use contour properties to identify the MRZ.We start looping over our sorted list of contours. For each of these contours, we’ll compute the bounding box and use it to compute two properties: the aspect ratio and the coverage ratio. The aspect ratio is simply the width of the bounding box divided by the height. The coverage ratio is the width of the bounding box divided by the width of the actual image.The MRZ is rectangular, with a width that is much larger than the height. The MRZ should also span at least 75% of the input image.

![Final_Image](https://user-images.githubusercontent.com/53252686/86606500-b5560f00-bfc5-11ea-991e-6d8125b3453a.jpg)


Extract the ROI from the image and draw a bounding box surrounding the MRZ.

![roi](https://user-images.githubusercontent.com/53252686/86606886-331a1a80-bfc6-11ea-877f-8c6faa411fc5.jpeg)






 
