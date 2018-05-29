---
layout: post
title:  "Low light face recognition with OpenCV"
date:   2018-05-14
categories: ml
---

During ScalaDays Berlin 2018, which I attended, organisers had a small task for each talk - audience counting. As I've heard about OpenCV pre-trained models for face recognition for instance, I've decided to test it on larger photos, with more faces.

The Script is super simple:

```
import cv2             
import matplotlib.pyplot as plt                        
%matplotlib inline                               

def image_faces(image_path):
    # pre-trained face detector from OpenCV
    face_cascade = cv2.CascadeClassifier('haarcascades/haarcascade_frontalface_alt.xml')

    # load color (BGR) image
    img = cv2.imread(image_path, 0)
    # img = cv2.imread("/Users/misza222/audience5.jpeg", 0)

    # search for faces in the image
    faces = face_cascade.detectMultiScale(img)

    # for demonstration of what was detected draw bounding box for each detected face
    for (x,y,w,h) in faces:
        # add bounding box to color image
        cv2.rectangle(img,(x,y),(x+w,y+h),(255,0,0),2)

    # convert BGR image to RGB for plotting
    cv_rgb = cv2.cvtColor(img, cv2.COLOR_GRAY2RGB)

    # display the image, with bounding boxes
    plt.imshow(cv_rgb)
    plt.show()

    return len(faces)


# to call the method
nr_faces = image_faces("/Users/misza222/audience9.jpeg")

print("Number of faces on the image: " + nr_faces)
```

but the results on images of the audience were disappointing. Reasons:

 - images were in low light
 - images were blurry
 - pre-trained classifier was only trained on ppl that were facing the camera
