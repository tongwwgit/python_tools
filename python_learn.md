* 对象.astype(): 用来转换数据类型
* Python assert（断言）用于判断一个表达式，在表达式条件为 false 的时候触发异常。

### Python装饰器

装饰器是增强函数或类的功能的一种函数，拓展函数功能

```python
import time
#定义装饰器：装饰器参数是一个函数，返回值也是一个函数，作为参数的这个函数func()就在返回函数wrapper()的内部执行。
def deco(func):
    def wrapper():
        startTime = time.time()
        func()
        endTime = time.time()
        msecs = (endTime - startTime)*1000
        print("time is %d ms" %msecs)
    return wrapper

#使用装饰器
@deco
def func():
    print("hello")
    time.sleep(1)
    print("world")

if __name__ == '__main__':
    f = func #这里f被赋值为func，执行f()就是执行func()
    f()

```



常见的内置装饰器有三种，@property、@staticmethod、@classmethod



#### @property

python的@property是python的一种装饰器，是用来修饰方法的。https://zhuanlan.zhihu.com/p/64487092
我们可以使用@property装饰器来创建只读属性，@property装饰器会将方法转换为相同名称的只读属性,可以与所定义的属性配合使用，这样可以防止属性被修改。

#### python中@staticmethod  静态方法

该方法不强制要求传递参数(该函数不传入self或者cls)，不能使用类变量和实例变量，如下声明一个静态方法：
class C(object):
    @staticmethod
    def f(arg1, arg2, ...):
        ...
以上实例声明了静态方法 f，从而可以实现实例化使用 C().f()，当然也可以不实例化调用该方法 C.f()

#### python中@abstractmethod 抽象类方法

class IStream(metaclass=ABCMeta):
	@abstractmethod
	def read(self, maxbytes=-1):
		pass
抽象类的一个特点是它不能直接被实例化，抽象类的目的就是让别的类继承它并实现特定的抽象方法

print(__file__)                  #打印文件当前的位置
os.path.splitext(path_dir)[1]       取出文件扩展名
np.round() 方法返回浮点数x的四舍五入值。

#### cv2库的使用

色彩空间转化函数 cv2.cvtColor( )进行色彩空间的转换:opencv中有多种色彩空间，包括 RGB、HSI、HSL、HSV、HSB、YCrCb、CIE XYZ、CIE Lab8种

* 在图像读取方法cv2.imread中使用0或者cv2.IMREAD_GRAYSCALE读取灰度图
  因为默认cv2.imread读取的是彩色图，若输入灰度图，3个通道值一样
  image_array=cv2.imread(image_path,0)

#### pip install相关的问题总结

* pip安装包的三种方式
  * pip install xx : 在线安装，会安装该包的相关依赖包, 如果网络不好可以使用国内镜像，方法为： pip install xx -i http://xx
  * 离线安装：如果下载得到的是.tar.gz压缩包，解压，在解压目录的当前文件夹下，打开DOS命令运行：python setup.py install 
  * 离线安装：.whl 文件安装： 当前目录下运行： pip install ×××.whl

* **pip install -e . **   可以git clone到本地后进入文件夹    pip install -e .　安装 

  pip会自动将包复制到site-packages。 这样pip可以直接从一个version control system(VCS)安装包，比如git.

   it can actually be useful if you want to run your packages with python package.py and you import other modules of your project from that file. The command makes them findable! What it does is :

  * installs site-packages/PackageName.egg-link file
  * adds path to site-packages/easy-install.pth
  * optionally installs CLI targets in <venv>/bin

* **python setup.py install** 主要是安装典型第三方包，这种包比较稳定，不再需要你去编辑、修改或是调试。
* **python setup.py develop** 当你安装一个包后，这个包需要你不断修改，这样你就不得不重新安装，这时就采用这种安装方法。
* Python及其一些模块安装包里可能有setup.py，是用来执行安装的

### numba.jit 加速python代码

python由于它动态解释性语言的特性，跑起代码来相比java、c++要慢很多。**numba是一款可以将python函数编译为机器代码的 JIT(just in time 即时)编译器**，经过numba编译的python代码（仅限数组运算），其运行速度可以接近C或FORTRAN语言。numba的作用是给python换一种编译器。

用numba非常简单，只需要将**numba装饰器**应用到python函数中，无需改动原本的python代码，numba会自动完成剩余的工作。numba可以把各种具有很大loop的函数加到很快的速度，擅长处理循环，喜欢numoy函数但numpy的加速只适用于numpy自带的函数。但要注意的是，numba对没有循环或者只有非常小循环的函数加速效果并不明显

```python
# 用numba加速的求和函数
@nb.jit()
def nb_sum(a):
    Sum = 0
    for i in range(len(a)):
        Sum += a[i]
    return Sum
```

```python
@nb.jit(nopython=True,fastmath=True) 牺牲一丢丢数学精度来提高速度
@nb.jit(nopython=True,parallel=True) 自动进行并行计算
切记一定要用nopython。默认都是True的
```



#### Ipython 

%time可以测量一行代码执行的时间
%timeit可以测量一行代码多次执行的时间