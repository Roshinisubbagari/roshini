## Histogram 

A histogram is a graphical representation that shows the distribution of a dataset, typically used to visualize the frequency of different values within a set of data.A histogram represents the distribution of pixel intensities in an image.
## PACKAGES

opencv, numpy, matplotlib

## Histogram uses

Image Processing 

Machine Learning 

Data Analysis
## Program 
1. Import libraries

import numpy as np

import cv2 as cv

from matplotlib import pyplot as plt
 2.Reads an image from the specified file path using.
 
img = cv.imread('/home/roshini-subbagari/Desktop/archana/lily.jpeg')

3.The image is loaded, it saves a copy of the image to a new file path using.

cv.imwrite("/home/roshini-subbagari/Desktop/archana/lil.jpeg",img)

assert img is not None, "file could not be read, check with os.path.exists()"
color = ('b','g','r')

for i,col in enumerate(color):

4.Calculates the histogram of the image for the current color channel.

 histr = cv.calcHist([img],[i],None,[256],[0,256])
 
 plt.plot(histr,color = col)
 
 plt.xlim([0,256])

 5.This function displays the plot showing the color histograms for the blue, green, and red channels.
 
plt.show()

## Input

![lily](https://github.com/Roshinisubbagari/roshini/assets/169050913/a47b03f5-714b-4f95-98ac-a384440db7ea)

## Output









