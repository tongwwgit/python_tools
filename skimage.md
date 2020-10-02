#### 生成图片边缘

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
grad_h=sobel_h(fg255_blur) #水平边缘
grad_v=sobel_v(fg255_blur) #垂直边缘
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

