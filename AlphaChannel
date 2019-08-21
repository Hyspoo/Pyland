#叠加带Alpha通道的前景手势于任意背景图上
import cv2 as cv
import numpy as np

foreground = cv.imread("hand.png", cv.IMREAD_UNCHANGED)
background = cv.imread("bg.jpg")

#分离出前景的alpha通道，并使其独立成图
b,g,r,alpha = cv.split(foreground)
foreground_BGR = cv.merge((b,g,r))
alpha = cv.merge((alpha,alpha,alpha))

#将alpha的数值设在0-1之间
alpha = alpha.astype(float)/255

#将前景图、背景图全部改成float类型
foreground_BGR = foreground_BGR.astype(float)
background = background.astype(float)

#将前景乘以alpha权重，背景乘以反alpha权重
foreground_BGR = cv.multiply(alpha, foreground_BGR)
background = cv.multiply(1.0 - alpha, background)

#叠加前景、背景
outImage = cv.add(foreground_BGR, background).astype(np.uint8)

cv.imwrite("final.jpg", outImage) #, [int(cv.IMWRITE_JPEG_QUALITY),90]) #该参数用于压缩导出的jpg图片，90为压缩百分比

"""cv.imshow("hand+BG", outImage)
cv.waitKey(0)
for i in range(1,5):
    cv.destroyAllWindows()
    cv.waitKey(1)"""
