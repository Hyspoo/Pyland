import numpy as np
import cv2 as cv
import copy

drawing = False # true if mouse is pressed
ix,iy = -1,-1

# assert four image content with different function...
img = np.zeros((512,512,3), np.uint8) # the image shows on screen
img_live = copy.deepcopy(img) # apply drawRectangle method & remove quickly for real-time display
img_0 = copy.deepcopy(img) # saves the image in last-iteration
img_original = copy.deepcopy(img) # saves the original image
rectangleList = []

# mouse callback function
def draw_rectangle(event,x,y,flags,param):
    global ix, iy, drawing, img, img_live, img_0, img_original, rectangleList
    
    if event == cv.EVENT_LBUTTONDOWN:
        drawing = True
        ix,iy = x,y
    
    elif event == cv.EVENT_MOUSEMOVE:
        if drawing == True:
            cv.rectangle(img_live,(ix,iy),(x,y),(0,255,0),2)
            img = copy.deepcopy(img_live) 
            img_live = copy.deepcopy(img_0)

    elif event == cv.EVENT_LBUTTONUP:
        drawing = False
        rectangleList.append([(ix,iy),(x,y)])
        
        # set img_live blank
        img_live = copy.deepcopy(img_original)
        
        # draw rectangle using updated rectangleList
        for i in rectangleList:
            cv.rectangle(img_live,i[0],i[1],(0,255,0),2)
            
        img = copy.deepcopy(img_live)
        img_0 = copy.deepcopy(img)
        
        
cv.namedWindow('image')
cv.setMouseCallback('image', draw_rectangle)

while(1):
    cv.imshow('image',img)
    k = cv.waitKey(1) & 0xFF
    if k == 27:
        break

cv.destroyAllWindows()
