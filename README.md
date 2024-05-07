## Bounding_Boxes

1.INSTALL FOLLOWING PACKAGES

```csv,PIL```

2.CODE
```bash


import os
import csv
from PIL import Image, ImageDraw

# Define paths for CSV file, image directory, and output directory
csv_file = "/home/roshini-subbagari/Downloads/7622202030987_bounding_box.csv"
image_dir = "/home/roshini-subbagari/Downloads/7622202030987"
output_dir = "/home/roshini-subbagari/Downloads/7622202030987_with_boxes"

# Create output directory if it doesn't exist
os.makedirs(output_dir, exist_ok=True)

# Function to draw bounding boxes on an image
def draw_boxes(image, boxes):
    draw = ImageDraw.Draw(image)
    for box in boxes:
        # Extract box coordinates
        left = int(box['left'])
        top = int(box['top'])
        right = int(box['right'])
        bottom = int(box['bottom'])
        # Draw rectangle on image
        draw.rectangle([left, top, right, bottom], outline="blue")
    return image

# Function to crop image based on bounding boxes
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

# Open CSV file and process each row
with open(csv_file, 'r') as file:
    csv_reader = csv.DictReader(file)
    for row in csv_reader:
        # Get image filename from CSV row
        image_name = row['filename']
        # Construct full path to image
        image_path = os.path.join(image_dir, image_name)
        # Construct full output path
        output_path = os.path.join(output_dir, image_name)
        # Open image
        image = Image.open(image_path)
        # Extract bounding box coordinates from CSV row
        boxes = [{'left': row['xmin'], 'top': row['ymin'], 'right': row['xmax'], 'bottom': row['ymax']}]
        # Crop images based on bounding boxes
        cropped_images = crop_image(image, boxes)
        # Save cropped images
        for i, cropped_img in enumerate(cropped_images):
            cropped_img.save(os.path.join(output_dir, f"{i}_{image_name}"))  
        # Draw bounding boxes on full image
        full_image_with_boxes = draw_boxes(image, boxes)
        # Save full image with bounding boxes
        full_image_with_boxes.save(os.path.join(output_dir, f"full_{image_name}"))

```
## Histogram 
1.INSTALL FOLLOWING PACKAGES


```numpy,opencv,matplotlib```

2.CODE

```
import numpy as np
import cv2 as cv
from matplotlib import pyplot as plt
 
img = cv.imread('/home/roshini-subbagari/Desktop/archana/lily.jpeg')
cv.imwrite("/home/roshini-subbagari/Desktop/archana/lil.jpeg",img)
assert img is not None, "file could not be read, check with os.path.exists()"
color = ('b','g','r')
for i,col in enumerate(color):
 histr = cv.calcHist([img],[i],None,[256],[0,256])
 plt.plot(histr,color = col)
 plt.xlim([0,256])
plt.show()
```
## Webcame
```
# import the opencv library 
import cv2 
  
  
# define a video capture object 
vid = cv2.VideoCapture(0) 
  
while(True): 
      
    # Capture the video frame 
    # by frame 
    ret, frame = vid.read() 
  
    # Display the resulting frame 
    cv2.imshow('frame', frame) 
      
    # the 'q' button is set as the 
    # quitting button you may use any 
    # desired button of your choice 
    if cv2.waitKey(1) & 0xFF == ord('q'): 
        break
    # After the loop release the cap object 
vid.release() 
# Destroy all the windows 
cv2.destroyAllWindows()
```



