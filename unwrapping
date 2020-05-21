import cv2
import argparse
import numpy as np
import math

img = cv2.imread("./spherical/image.jpg",1)
height,width,planes = (np.shape(img))
ratio = height/width
dim = (int(720/ratio),720)
img_resize = cv2.resize(img, dim, interpolation = cv2.INTER_AREA) 
height,width,plane = np.shape(img_resize)
width_dst = height*2
dst_img = np.zeros((height, width_dst,3),dtype= int)

print(height)

for k in range(0,3):
    for i in range(1,height):
    
        altitude = abs(i-int(height/2))
                
        lat = np.sqrt(abs((height*height)/4 - (altitude*altitude)))
        lat = int(lat)
    
        if(lat==0):
            continue   
    
        left = (width/2) - lat
        left = int(left)
                    
        right = (width/2) + lat
        right = int(right)
        
        if(width%2==0):
            left=left-1
            right=right-1
        
        jump = width_dst/(2*lat)
        if(jump<1):
            jump=1
        #jump = int(jump)
        
           
        for j in range(left,right):
            position = int((j-left)*jump)
            #print("position is ",position,"j is ",j)
            if(position>=width_dst or j>=width):
                break;
                
            dst_img[i,position,k] = img_resize[i,j,k]
          
           
    #print(dst_img[0:123,0:149])            
    dst_img = dst_img.astype(np.uint8)
    #print(dst_img[300,:])

for c in range(0,3):    
    for i in range(1,height):
        pixel = 100;
        for j in range(width_dst):
            
            if(dst_img[i,j,c]!=0):
                pixel = dst_img[i,j,c]
               
        #print(pixel)
            if(dst_img[i,j,c]==0):
                dst_img[i,j,c] = pixel

           



cv2.imwrite('./panorama/input.jpg',dst_img)
