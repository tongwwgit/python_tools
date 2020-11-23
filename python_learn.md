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

用numba非常简单，只需要将**numba装饰器**应用到python函数中，无需改动原本的python代码，numba会自动完成剩余的工作。numba可以把各种具有很大loop的函数加到很快的速度，擅长处理循环，喜欢numoy函数但numpy的加速只适用于numpy自带的函数。但要注意的是，numba对没有循环或者只有非常小循环的函数加速效果并不明显.

在numb中必须使用明确数据类型的，不能使用列表，否则会报错

http://numba.pydata.org/numba-doc/0.17.0/reference/numpysupported.html

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

### 其他零散命令

* 对象.astype(): 用来转换数据类型

* Python assert（断言）用于判断一个表达式，在表达式条件为 false 的时候触发异常。

* 内置函数 dir() 函数不带参数时，返回当前范围内的变量、方法和定义的类型列表

* python中一个.py文件就是一个模块。文件名和模块名的差别只是有没有后缀。有后缀是文件名，没有后缀是模块名。

* 包的本质就是一个包含__init__.py文件的目录。导入包，本质上是导入了包中的__init__.py文件。

  

### 调试代码设置断点： import pdb; pdb.set_trace()

### PEP: Python Enhancement Proposals

PEP的全称是Python Enhancement Proposals，其中Enhancement是增强改进的意思，Proposals则可译为提案或建议书，所以合起来，比较常见的翻译是Python增强提案或Python改进建议书。

PEP 8 -- Style Guide for Python Code，编码规范（必读）

使用官方代码规范PEP8，中文版本见google开源项目指南。
强制要求缩进使用4个space，每行字符数不超过120。
代码格式化工具yapf, autopep8，pep8ify，可通过pip安装和使用。
pycharm，sublime等可通过搜索yapf，pep8等安装格式化插件



#### Python语言规范

* 不要在函数或方法定义中使用可变对象作为默认值.
* 尽可能使用隐式的false, 例如: 使用 if foo: 而不是 if foo != []:
* 不要在行尾加分号, 也不要用分号将两条命令放在同一行.
* 换行问题：Python会将 圆括号, 中括号和花括号中的行隐式的连接起来 ，不要额外的换行符
* 缩进：禁止用tab, 严格用4个空格控制缩进
* 空行：顶级定义之间空两行, 方法定义之间空一行
* 空格：
  * 括号内不要有空格
  * 不要在逗号, 分号, 冒号前面加空格；但应该在它们后面加(除了在行尾).
  * 参数列表, 索引或切片的左括号前不应加空格.
  * 在二元操作符两边都加上一个空格, 比如赋值(=), 比较(==, <, >, !=, <>, <=, >=, in, not in, is, is not), 布尔(and, or, not). 算术操作符两边的空格可加可不加，保持一致即可
  * 当’=’用于指示关键字参数或默认参数值时, 不要在其两侧使用空格.
* Shebang (也称为Hashbang)是一个由井号和叹号构成的字符串行(#!)， 用于指定脚本的解释器
* 注释：
  * 函数注释：文档字符串(必须三重双引号)，注释Args:       Returns:
  * 块注释和行注释： 对于复杂的操作, 应该在其操作开始前写上若干行注释. 对于不是一目了然的代码, 应在其行尾添加注释.
* 字符串： 为多行字符串使用三重双引号”“”而非三重单引号
* todo注释：为临时代码使用TODO注释,
* 导入格式：按照以下顺序：标准库导入，第三方库导入，应用程序指定导入
  * python的标准库是随着pyhon安装的时候默认自带的库。
  * python的第三方库，需要下载后安装到python的安装目录下，不同的第三方库安装及使用方法不同。



### Python中双下划线相关

```python
__init__.py的作用
(1) 用于package的标识，如果没有该文件，该目录就不会认为是package。__init__.py里面可以为空
(2) 定义__all__用来模糊导入。__all__ 关联了一个模块列表，当执行 from xx import * 时，就会导入列表中的模块
(3) 里面可以填写需要导入的import

如果目录中包含了 __init__.py 时，当用 import 导入该目录时，会执行 __init__.py 里面的代码。
```



### Pycharm

pycharm配置autopep8： https://www.pianshen.com/article/4161789718/

* 格式化命令：选择代码右键-external tools-autopep8
* 注释快捷键： ctrl+ /