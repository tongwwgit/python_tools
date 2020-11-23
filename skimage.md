#### 生成图片边缘

边缘检测的本质是微分，如上图所示，当相邻两个像素点的灰度值差异越大时，也就是其斜率越陡，也就是微分值越大，进而通过这个来判断边缘，实际中常用差分，x方向和y方向。

```python
from skimage.filters import gaussian, sobel_h, sobel_v, sobel
from skimage.segmentation import find_boundaries
import cv2

image=cv2.imread('binary_value_figure',0)
#image是binary mask, 二维numpy,值为0，1
fg=(image==1)
edge=find_boundaries(fg)  #得到边界
edge=edge.astype(np.uint8)
#生成方向
fg255=(fg*255).astype(np.uint8)
fg255_blur=gaussian(fg255,sigma=2) #局部高斯模糊
grad_h=sobel_h(fg255_blur) #横向梯度： 算子使用3*3矩阵和原始图片做卷积得到
grad_v=sobel_v(fg255_blur) #纵向梯度
orient_angle = np.arctan2(grad_v, grad_h) + np.pi #可直接生成每一点的方向，范围是[0,2pi]

#sobel方法直接生成边缘
edge_sobel=sobel(image_array)    #返回的是array of float，非边缘的地方值为0
```

#### 提取图片的skeleton, skeleton的node graph

```python
from skimage.morphology import skeletonize,thin
#二者无明显区别
#thin
#image_array:Zeros represent background, nonzero values are foreground.
skeleton = morphology.thin(image_array)
skeleton=skeleton.astype(np.uint8)
#skeletonize
skeleton = morphology.skeletonize(image_array)
skeleton=skeleton.astype(np.uint8)

#安装sknw:   https://github.com/Image-Py/sknw  可以提取skeleton的node graph

```

