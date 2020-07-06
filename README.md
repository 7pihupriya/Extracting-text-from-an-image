# Extracting-text-from-an-image
Objective : Detecting machine-readable-zones in a passport image

The MRZ region in passports or travel cards fall into two classes: 
Type 1 and Type 3. Type 1 MRZs are three lines, with each line containing 30 characters. 
The Type 3 MRZ only has two lines, but each line contains 44 characters. 
In either case, the MRZ encodes identifying information of a given citizen, including the type of passport, passport ID, issuing country, name, nationality, expiration date, etc.

MRZ detection using only basic image processing techniques such as thresholding, morphological operations, and contour properties. 
import our necessary packages. And have OpenCV installed already. We’ll also need imutils, my collection of convenience functions to make basic image processing operations with OpenCV easier. We can install imutils  using pip.

 Loads our original image from disk and resizes it to have a maximum height of 390 pixels.
  
