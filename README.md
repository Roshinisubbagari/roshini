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


![Figure_1](https://github.com/Roshinisubbagari/roshini/assets/169050913/a5e789c6-c8b3-4311-bf75-95322da99742)

## Bounding Boxes

a bounding box is a rectangular box drawn around an object or region of interest in an image. Bounding boxes are commonly used for tasks such as object detection and image annotation.

1.Import libraries

os - The operating system provides a platform, on top of which, other programs, called application programs can run.

csv - CSV files are a simple, versatile, and widely used format for storing and sharing structured data.

pil - python imaging library and its original library


1. Import libraries

import os

import csv

from PIL import Image, ImageDraw

2. Read the paths

csv_file = "/home/roshini-subbagari/Downloads/7622202030987_bounding_box.csv"

image_dir = "/home/roshini-subbagari/Downloads/7622202030987"

output_dir = "/home/roshini-subbagari/Downloads/7622202030987_with_boxes"

3. Directory Creation

os.makedirs(output_dir, exist_ok=True)

4. Specifying the draw_boxes, and crop the image functions.

def draw_boxes(image, boxes):

    draw = ImageDraw.Draw(image)
    
    for box in boxes:
            
        left = int(box['left'])
        
        top = int(box['top'])
        
        right = int(box['right'])
        
        bottom = int(box['bottom'])
        
        # Draw rectangle on image
        
        draw.rectangle([left, top, right, bottom], outline="blue")
    return image

def crop_image(image, boxes):

    cropped_images = []
    
    for box in boxes:
        # Extract box coordinates
        left = int(box['left'])
        top = int(box['top'])
        right = int(box['right'])
        bottom = int(box['bottom'])
        # Crop image based on box coordinates
        cropped_img = image.crop((left, top, right, bottom))
        cropped_images.append(cropped_img)
    return cropped_images

5. processing csv file
   
with open(csv_file, 'r') as file:

    csv_reader = csv.DictReader(file)
    
    for row in csv_reader:
    
        
        image_name = row['filename']
        
        image_path = os.path.join(image_dir, image_name)
        
        output_path = os.path.join(output_dir, image_name)
       
        image = Image.open(image_path)
        
        boxes = [{'left': row['xmin'], 'top': row['ymin'], 'right': row['xmax'], 'bottom': row['ymax']}]
        
        
        cropped_images = crop_image(image, boxes)
        
        for i, cropped_img in enumerate(cropped_images):
        
            cropped_img.save(os.path.join(output_dir, f"{i}_{image_name}"))  
        
        full_image_with_boxes = draw_boxes(image, boxes)
        
        full_image_with_boxes.save(os.path.join(output_dir, f"full_{image_name}"))

## Input

![7622202030987_f306535d741c9148dc458acbbc887243_L_487](https://github.com/Roshinisubbagari/roshini/assets/169050913/ed1fc0f6-cbd6-4f8c-8205-97acbdd3de78) 


## Output

![full_7622202030987_f306535d741c9148dc458acbbc887243_L_487](https://github.com/Roshinisubbagari/roshini/assets/169050913/2940e249-0848-4b6c-bbf0-bf3d6c1dfaf4) 


## Iteration

Here is the program explain the printing of first 10 numbers and in each ieration ,printing the sum of current and privious values

 num = list(range(10))
 it create a list called num containing from 0 to 9 and using range
 
previousNum = 0

Then ,variable previous num is 0

for i in num:

Next enter in to for loop iterates each element i in list num

    sum = previousNum + i

    It calculate the sum of current num and previous num store it i
    
    
    print('Current Number '+ str(i) + 'Previous Number ' + str(previousNum) + 'is ' + str(sum)) # <- This is the issue.
    
    previousNum=i 

    Finally it update the previous variable to be equal to the current num i before the next iteration

## Output

    Current Number 0Previous Number 0is 0
    
Current Number 1Previous Number 0is 1

Current Number 2Previous Number 1is 3

Current Number 3Previous Number 2is 5

Current Number 4Previous Number 3is 7

Current Number 5Previous Number 4is 9

Current Number 6Previous Number 5is 11

Current Number 7Previous Number 6is 13

Current Number 8Previous Number 7is 15

Current Number 9Previous Number 8is 17


## Webcam

A webcam is a digital camera designed for capturing video or images in real-time and streaming them to a computer or over the internet. Webcams are widely used for video conferencing, live streaming, security monitoring, and capturing images for various purpose

1.import library 

import cv2

2.This creates a VideoCapture object (vid) to capture video from the default webcam

vid = cv2.VideoCapture(0) 

3.the camera is open and ready to use. If not, print an error message. 

if (video.isOpened() == False):  
    print("Error reading video file") 
4. The frame width,height from the camera and convert it to an integer.

frame_width = int(video.get(3)) 
frame_height = int(video.get(4)) 

5.The size of the output using the video frame width and height.

size = (frame_width, frame_height) 

   
result = cv2.VideoWriter('a.avi',  
                         cv2.VideoWriter_fourcc(*'MJPG'), 
                         10, size) 
    
while(True): 
    ret, frame = video.read() 
  
    if ret == True:  
  
        # Write the frame into the 
        # file 'filename.avi' 
        result.write(frame) 
        cv2.imshow('Frame', frame) 
  
        # Press S on keyboard  
        # to stop the process 
        if cv2.waitKey(1) & 0xFF == ord('s'): 
            break
  
    # Break the loop 
    else: 
        break
  
# When everything done, release  
# the video capture and video  
# write objects 
video.release() 
result.release() 
    
# Closes all the frames 
cv2.destroyAllWindows() 
   
print("The video was successfully saved")



## Output

https://github.com/Roshinisubbagari/roshini/assets/169050913/4b8e90a0-363d-40c2-8c31-f8ab2f4fd646



    





        








