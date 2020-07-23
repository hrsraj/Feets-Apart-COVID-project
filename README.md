# Feets-Apart-COVID-project
# Made by Harsh Raj
# Better open it in Pycharm

import cv2

# initialize detector using cascade classifier
detector= cv2.CascadeClassifier("body_cascade.xml")

# provide path to video file or directly set to 0 for live detection
path = 'Path to video file'

# capture Video
cap = cv2.VideoCapture(0) # path can be place din place of 0

# iterate through video
while True:
    success, imag = cap.read() # read the image frames of video
    
    # resizing the video for better studying
    img = cv2.resize(imag,(500,300))
    
    # set images to gray for detection
    imgGray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)
    
    # store detected bodies in some variable
    bodies = detector.detectMultiScale(imgGray, 1.1, 2)

    # initialize variable to keep count of the number of people in the room
    counter = 0
    for (x, y, w, h) in bodies:
        counter += 1
        
        # setting room limit to 5 so that social distancing is maintained properly
        if counter >= 5:
            print ("Warning: Limit Exceeded")
            cv2.rectangle(img, (x, y), (x + w, y + h), (0, 0, 255), 2)
        else:
            cv2.rectangle(img, (x, y), (x + w, y + h), (255, 0, 0), 2)
    
    # show the result
    cv2.imshow("result", img)
    if cv2.waitKey(1) & 0xFF ==ord('q'):
        break
