Fundamentals of Computer Graphics

## 第一章：介绍

### 1.1 图形学领域

图形学主要包括三个领域分别为建模，渲染以及动画。

建模：用计算机以及数学知识处理形状和物体的表面性质

渲染：继承自艺术，处理3D模型的阴暗画面。

动画：通过图像创作视知觉的动作，用到渲染和建模。

相关领域有人机交互（UI），虚拟现实(VR)，视觉效果，图像处理，3d建模和计算摄影。

### 1.2 主要应用

几乎任何领域都可以用到一些图形学的内容，但主要为以下产业。

电子游戏，动漫，视觉效果，动作电影，CAD/CAM(计算机辅助绘图和计算机辅助制造)，模拟，医疗影像，信息可视化。

### 1.3 图形API

每个图形学程序都要用图形API和UI API。图像API用于输出画面，UI API用于接收输入。范例有JAVA，Direct3D和OpenGL。

### 1.4 渲染管线

过去基本处理方法为用管线地图联系3d图中的顶部位置和2d图中的屏幕位置，画出三角形。

现在大部分用z-buffer(深度缓冲)，z-buffer通过一个特殊的记忆缓冲区用暴力破解方式解决问题。

渲染管线的几何控制基本在四维空间中，其中三个坐标是传统的几何坐标，另一个为齐次坐标（humogeneous coordinate）,用于透视观察。所以处理渲染管线时，主要需要处理四阶矩阵和四维向量。这个四维系统是计算机系统中最美丽和微妙的系统之一，也是学习计算机图形学需要越过的最大障碍之一。

生成图像的速度主要取决于三角形绘制的数量。在观察景物时可以控制三角形数量来控制细节.

### 1.5 数字问题

IEEE定制了三个重要的浮点数，分别为正无穷，无穷小和NaN（无效数字，not a number）

这些式子中a为正数

> +*a/*(+*∞*) = +0
>
> *−a/*(+*∞*) = *−*0 
>
> +*a/*(*−∞*) = *−*0
>
> −a/*(*−∞) = +0
>
> *∞* + *∞* = +*∞*
>
> *∞−∞* = NaN
>
> *∞×∞* = *∞* 
>
> *∞**/**∞* = NaN
>
> *∞*/a = *∞* 
>
> *∞*/0 = *∞* 
>
> 0*/*0 = NaN

以下逻辑运算为真，

> 1.所有有限数比+*∞*小
>
> 2.所有有限数比−∞大
>
> 3.−∞比+*∞*小

有关NaN的运算结果

> 1.有关NaN的计算结果都为NaN
>
> 2.有关NaN的逻辑运算结果都为NaN

除数为+0的运算

>+*a/* +0 = +*∞*
>
>*−*a/ +0 = *−∞*

### 1.6 效率

一个启发：相比流程，程序员要更关注记忆通道模式。

使代码运行更快：

1.以最直接的方式编写代码。根据需求实时计算中间结果而不是储存他们。

2.在优化后编译。

3.用现有工具处理关键的瓶颈。

4.分析数据结构寻找优化局部的方法，尽可能使数据单元大小匹配目标结构的缓存/页面大小（cache/page size）。

5.如果分析显示瓶颈来自数学计算，检查编译器生成的汇编代码是否没有效率。尝试重写源码解决问题。

最重要的是第一步。

### 1.7 设计和编写图形程序

#### 1.7.1 类设计

一个普遍问题：位置和位移是否应该分为两个类

基本类：

- vector2： 一个储存x和y分量的二维向量。它将这些分量储存在一个长度为2的数组中来支持索引操作。同时操作还包括向量加法，向量减法，点乘，叉乘，标量乘法和标量除法。
- vector3：与vector2相似的三维向量类。
- hvector：具有四个分量的齐次向量。
- rgb：RGB颜色储存三个分量，操作包括RGB加法，RGB减法，RGB乘法，标量除法，标量乘法。
- transform：用于变换的四阶矩阵，操作包括矩阵乘法和成员函数，应用于坐标，方向和曲面法向量。
- image：有输出操作的RGB像素构成的二维数组。

可能也会为区间，标准正交基，坐标系添加类。

#### 1.7.2 Float vs. Double

减少内存使用和保持一致的内存访问要求使用单精度数据。

避免数值问题建议使用双精度数值。

权衡取决于程序，但建议在类定义中使用默认值。

#### 1.7.3 调试图形程序

建议的调试策略：

> 科学方法：创建一个图像，观察它有什么问题。提出一个导致问题的假设然后调试它。例子：“Shadow Acne"问题
>
> 将编码调试输出为图像：在许多情形中，在输出图像中可以知道最直接的调试信息。
>
> 使用调试器：在怀疑出现问题的地方调试，使用”条件断点（conditional breakpoint）“，并注意编译器给出的错误信息。
>
> 将数据可视化进行调试：将自己的数据绘好图，做好解释。

## 第二章：相关数学

### 2.1集和映射

属于：*a* *∈* **S**

笛卡尔积：**A** *×* **B**   A×B = {(x,y)|x∈A∧y∈B}

集合的幂 **A<sup>2</sup> **= **A** *×* **A**

实数集：**R**

正实数集（包括0）：**R<sup>+</sup>**

二维平面有序对：**R<sup>2</sup>**

n维笛卡尔空间中的点：**R<sup>n</sup>**

整数集：**Z**

单位球体上的三维点集（**R<sup>3</sup>**中的点）:**S<sup>2</sup>**

映射符号：*→*

例子：*f* : **R** → **Z**

f(a)被称为a的映像，A的映像则是值域的子集。整个域的映像也被称为函数的范围

#### 2.1.1逆映射

*f* : **A **→ **B** 若逆映射存在，表示为*f* <sup>-1</sup>: **B **→ **A**

即*f*<sup>-1</sup>(b)=a若*f*(a)=b

![image-20220107185748426](C:\Users\Saputello\AppData\Roaming\Typora\typora-user-images\image-20220107185748426.png)

这样的映射称为双射

#### 2.2.2 区间

(0*,* 1)：0到1的区间不包括0和1，开区间

[0,1] :闭区间

[0*,* 1) ：半开半闭

![image-20220107190409263](C:\Users\Saputello\AppData\Roaming\Typora\typora-user-images\image-20220107190409263.png)

[0,1]<sup>3</sup>: 三维空间中的一个立方体

*∩*：交集符号 （3*,* 5)*∩*[4*,* 6] = [4*,* 5)

∪：并集符号 [3*,* 5)∪[4*,* 6] = [3*,* 6]

—：差分运算符，返回运算符左边不在右边区间中的点  [3*,* 5) *−* [4*,* 6] = [3*,* 4)和4*,* 6] *−* [3*,* 5) = [5*,* 6]

![image-20220107191404430](C:\Users\Saputello\AppData\Roaming\Typora\typora-user-images\image-20220107191404430.png)

#### 2.2.3 对数

对数在方程运算中很有用

y = log<sub>a</sub> x ⇔ a<sup>y</sup> = x

a<sup>log<sub>a</sub> (x)</sup> =x

log<sub>a</sub> (a<sup>x</sup>) =x

log<sub>a</sub> (xy) = log<sub>a</sub> x +log<sub>a</sub> y

log<sub>a</sub> (x/y) = log<sub>a</sub> x -log<sub>a</sub> y

log<sub>a</sub> x=log<sub>a</sub> b log<sub>b</sub> x

ln x ≡ log<sub>*e*</sub> x ，ln x 被称为自然对数

≡可看作定义的等价符号

它的导数体现出它为什么自然

![image-20220107192637198](C:\Users\Saputello\AppData\Roaming\Typora\typora-user-images\image-20220107192637198.png)

当a=e，常数因子即为单位1。

### 2.2 计算二次方程

一般形式：*Ax<sup>2</sup> + Bx + c = 0* 

几何意义：抛物线y=Ax<sup>2</sup> + Bx + c与0的交点
$$
x=\frac{-B±\sqrt{B^2-4AC}}{2A}
$$
判别式D ≡ B<sup>2</sup> -4AC , D＞0两个不同的实数解，D = 0,一个双重的实数解，D＜0，无实数解。

![image-20220110172725497](C:\Users\Saputello\AppData\Roaming\Typora\typora-user-images\image-20220110172725497.png)

### 2.3 三角学

#### 2.3.1 角度

角度由它在单位圆上切割的弧段的长度定义，这个弧长的单位是弧度。另一个常见的单位是度，其中圆的周长是360度。一个值为π弧度的角是180度，通常表示为180◦。
$$
角度=\frac{180}{\pi}弧长\\弧长=\frac{\pi}{180}角度
$$
![image-20220110173924320](C:\Users\Saputello\AppData\Roaming\Typora\typora-user-images\image-20220110173924320.png)

#### 2.3.2 三角函数

![image-20220110174643156](C:\Users\Saputello\AppData\Roaming\Typora\typora-user-images\image-20220110174643156.png)

勾股定理（毕达哥拉斯定理）*a*<sup>2</sup> + *o*<sup>2</sup> = *h*<sup>2</sup>*.*

sin *φ* *≡* *o/h*;

csc *φ* *≡* *h/o*;

cos *φ* *≡* *a/h*;

sec *φ* *≡* *h/a*;

tan *φ* *≡* *o/a*;

cot *φ* *≡* *a/o.*

这些定义允许我们建立极坐标体系，其坐标由原点的距离和一个有向角构成，方向一般为逆时针

![image-20220113121058563](C:\Users\Saputello\AppData\Roaming\Typora\typora-user-images\image-20220113121058563.png)

三角函数具有周期性

逆函数通过对值域的范围进行限制定义

asin : [*−*1*,* 1] *→* [*−*π/*2*, π/2];

acos : [*−*1*,* 1] *→* [0*, π*];

atan : *R* *→* [*−*π/*2*, π/2];

atan2 : *R*<sup>2</sup> *→* [*−*π, π]

图形学中，atan2函数极为有用，它通过y和x将笛卡尔坐标转换出极坐标的极角。

![image-20220113122502829](C:\Users\Saputello\AppData\Roaming\Typora\typora-user-images\image-20220113122502829.png)

#### 2.3.3 公式

诱导公式

sin(*−*A) = *−* sin *A*

cos(*−*A) = cos *A*

tan(*−*A) = *−* tan *A*

sin(*π/*2 *−* *A*) = cos *A*

cos(*π/*2 *−* *A*) = sin *A*

tan(*π/*2 *−* *A*) = cot *A* 

毕达哥拉斯公式

sin<sup>2</sup> *A* + cos<sup>2</sup> *A* = 1

sec<sup>2</sup> *A* *−* tan<sup>2</sup> *A* = 1

csc<sup>2</sup> *A* *−* cot<sup>2</sup> *A* = 1

和角公式

sin(*A* + *B*) = sin *A* cos *B* + sin *B* cos *A*

sin(*A* *−* *B*) = sin *A* cos *B* *−* sin *B* cos *A*

sin(2*A*) = 2 sin *A* cos *A*

cos(*A* + *B*) = cos *A* cos *B* *−* sin *A* sin *B*

cos(*A* *−* *B*) = cos *A* cos *B* + sin *A* sin *B*

cos(2*A*) = cos<sup>2</sup> *A* *−* sin<sup>2</sup> *A*
$$
tan(A + B)=\frac{tan A + tan B}{1 − tan A tan B}
$$

$$
tan(A - B)=\frac{tan A - tan B}{1 + tan A tan B}
$$

$$
tan(2A)=\frac{2tan A}{1 − tan^2 A}
$$

半角公式

sin<sup>2</sup>(*A/*2) = (1 *−* cos *A*)*/*2

cos<sup>2</sup>(*A/*2) = (1 + cos *A*)*/*2

和差化积公式

sin *A* sin *B* = *−*(cos(*A* + *B*) *−* cos(*A* *−* *B*))*/*2

sin *A* cos *B* = (sin(*A* + *B*) + sin(*A* *−* *B*))*/*2

cos *A* cos *B* = (cos(*A* + *B*) + cos(*A* *−* *B*))*/*2

![image-20220113124301029](C:\Users\Saputello\AppData\Roaming\Typora\typora-user-images\image-20220113124301029.png)

正弦定理
$$
\frac{sin A}{a}=\frac{sinB}{b}=\frac{sin C}{c}
$$
余弦定理
$$
c^2=a^2+b^2-2abcosC
$$
正切定理
$$
\frac{a+b}{a-b}=\frac{tan(\frac{A+B}{2})}{tan(\frac{A-B}{2})}
$$
海伦公式
$$
三角形面积=\frac{1}{4}\sqrt{(a + b + c)(−a + b + c)(a − b + c)(a + b − c)}
$$

### 2.4 矢量

#### 2.4.1 矢量操作

运算法则：平行四边形法则

**a** + **b** = **b** + **a**

![image-20220113144250122](C:\Users\Saputello\AppData\Roaming\Typora\typora-user-images\image-20220113144250122.png)

**b** *−* **a** ≡ − **a** + **b**

**a** + (**b** *−* **a**) = **b**

![image-20220113144453339](C:\Users\Saputello\AppData\Roaming\Typora\typora-user-images\image-20220113144453339.png)

矢量可以与实数实数直接乘除

#### 2.4.2 矢量的笛卡尔坐标

一个平面矢量可由两个线性无关的非零矢量表示

**c** = *a*<sub>c</sub>**a**+*b*<sub>c</sub>**b**

这两个矢量可以作为整个平面的基底，亦称基矢量。通常使用它们正交，且为单位矢量的情况。

**a** = *x*<sub>a</sub>**x**+*y*<sub>a</sub>**y**

![image-20220113145851257](C:\Users\Saputello\AppData\Roaming\Typora\typora-user-images\image-20220113145851257.png)

矢量的长度用毕达哥拉斯定理计算
$$
\|a\|=\sqrt{x^2_a+y^2_a}
$$
按照惯例，矢量的坐标写为有序对或列矩阵

#### 2.4.3 点乘

矢量之间的点积返回一个标量
$$
\pmb{a}\pmb{·}\pmb{b}=\| \pmb{a}\| \|\pmb{b}\|cos\phi
$$
![image-20220113151449118](C:\Users\Saputello\AppData\Roaming\Typora\typora-user-images\image-20220113151449118.png)

图形学中点乘最常用作计算两个矢量之间夹角的余弦值。

点积也可以用来寻找一个向量到另一个向量上的投影

![image-20220113151708340](C:\Users\Saputello\AppData\Roaming\Typora\typora-user-images\image-20220113151708340.png)

![image-20220113151731726](C:\Users\Saputello\AppData\Roaming\Typora\typora-user-images\image-20220113151731726.png)

**a** *·* **b** = **b** *·* **a** 

**a** *·* (**b** + **c**) = **a** *·* **b** + **a** *·* **c** 

(k**a**) *·* **b** = **a** *·* (k**b**) = k**a** *·* **b**

如果矢量已用笛卡尔坐标系表示

**a** *·* **b** = (*x*<sub>a</sub>**x** + *y*<sub>a</sub>**y**) *·* (*x*<sub>b</sub>**x** + *y*<sub>b</sub>**y**) 

= *x*<sub>a</sub>x<sub>b</sub>(**x** *·* **x**) + *x*<sub>a</sub>y<sub>b</sub>(**x** *·* **y**) + x<sub>b</sub>y<sub>a</sub>(**y** *·* **x**) + y<sub>a</sub>y<sub>b</sub>(**y** *·* **y**) 

= x<sub>a</sub>x<sub>b</sub>+ y<sub>a</sub>y<sub>b</sub>

#### 2.4.4 叉乘

叉乘通常只用于三维矢量

叉乘返回一个垂直于叉乘的两个向量的三维向量，长度与sinφ有关

根据右手定则判断方向

![image-20220113153953919](C:\Users\Saputello\AppData\Roaming\Typora\typora-user-images\image-20220113153953919.png)
$$
\pmb{a}\pmb{×}\pmb{b}=\| \pmb{a}\| \|\pmb{b}\| sin\phi
$$
![image-20220113153256779](C:\Users\Saputello\AppData\Roaming\Typora\typora-user-images\image-20220113153256779.png)

**x** = (1*,* 0*,* 0)*,* 

**y** = (0*,* 1*,* 0)*,* 

**z** = (0*,* 0*,* 1)*,*

**z** = **x** *×* **y**

**x** *×* **y** = +**z** *,* 

**y** *×* **x** = *−* **z** *,* 

**y** *×* **z** = +**x** *,* 

**z** *×* **y** = *−* **x** *,* 

**z** *×* **x** = +**y** *,*

**x** *×* **z** = *−* **y**

叉乘不可交换

**a** *×* (**b** + **c**) = **a** *×* **b** + **a** *×* **c** *,*

**a** *×* (k**b**) =k(**a** *×* **b**),

**a** *×* **b** = *−*(**b** *×* **a**)*.*

**a** × **b** = (x<sub>a</sub>**x** + y<sub>a</sub>**y** +z<sub>a</sub>**z**) × (x<sub>b</sub>**x** + y<sub>b</sub>**y** +z<sub>b</sub>**z**)
          =x<sub>a</sub>x<sub>b</sub> **x** × **x** + x<sub>a</sub>y<sub>b</sub> **x** × **y** +x<sub>a</sub>z<sub>b</sub> **x** × **z**+y<sub>a</sub>x<sub>b</sub> **y** × **x** + y<sub>a</sub>y<sub>b</sub> **y** × **y** +y<sub>a</sub>z<sub>b</sub> **y** × **z** + z<sub>a</sub>x<sub>b</sub> **z** × **x** + z<sub>a</sub>y<sub>b</sub> **z** × **y** +z<sub>a</sub>z<sub>b</sub> **z** × **z**

​		  =(y<sub>a</sub>z<sub>b</sub> - z<sub>a</sub>y<sub>b</sub>)**x** +(z<sub>a</sub>x<sub>b</sub> - x<sub>a</sub>z<sub>b</sub>)**y** +(x<sub>a</sub>y<sub>b</sub> - y<sub>a</sub>x<sub>b</sub>)**z**

**a** × **b** =（y<sub>a</sub>z<sub>b</sub> - z<sub>a</sub>y<sub>b</sub>,z<sub>a</sub>x<sub>b</sub> - x<sub>a</sub>z<sub>b</sub>,x<sub>a</sub>y<sub>b</sub> - y<sub>a</sub>x<sub>b</sub>）

#### 2.4.5 标准正交基和坐标系

$$
\|\pmb{u}\|=\|\pmb{v}\|=\|\pmb{w}\|=1\\
\pmb{u}\cdot\pmb{v}=\pmb{v}\cdot\pmb{w}=\pmb{w}\cdot\pmb{u}==0\\
通过右手定则：\pmb{w}=\pmb{u}\times\pmb{v}
$$

笛卡尔坐标系的特殊之处在于它在程序中隐式存储以及低级表示，而全局坐标系则储存在一个规范坐标系中。

在程序中也会找到参考点建立参考坐标系，这是需要被显式储存的

![image-20220215041936134](C:\Users\Saputello\AppData\Roaming\Typora\typora-user-images\image-20220215041936134.png)

为了得到存储在规范坐标系中的向量b的u-v-w坐标，我们可以使用点积：

*u*<sub>*b*</sub> = **u** *·* **b**; 

*v*<sub>*b*</sub>= **v** *·* **b**; 

*w*<sub>*b*</sub>= **w** *·* **b**

之后会使用矩阵来管理坐标系的变化

#### 2.4.6 从一个向量开始建立基底

首先，让这个向量变为单位向量
$$
\pmb{w}=\frac{\pmb{a}}{\|\pmb{a}\|}
$$
选择任意不与**a**共线的向量**t**，再利用交叉积找到垂直于**w**的单位向量**u**
$$
\pmb{u}=\frac{\pmb{t}\times{\pmb{w}}}{\|\pmb{t}\times{\pmb{w}}\|}
$$
最后
$$
\pmb{v}=\pmb{w}\times\pmb{u}
$$
用到这个方法的例子有曲面着色

#### 2.4.7  从两个向量开始建立基底

完全指定一个框架需要两个向量
$$
\pmb{w}=\frac{\pmb{a}}{\|\pmb{a}\|}
$$

$$
\pmb{u}=\frac{\pmb{b}\times{\pmb{w}}}{\|\pmb{b}\times{\pmb{w}}\|}
$$

$$
\pmb{v}=\pmb{w}\times\pmb{u}
$$

显然**a**和**b**互相垂直会更简单

例子有指定相机位置

#### 2.4.8 修正基底

由于误差或低精度有时基底会出现错误，这时应用现有的向量再次建立坐标系

### 2.5 曲线和表面

#### 2.5.1 二维隐式曲线

隐式曲线的隐函数方程 *f*(x,y)=0

提到的几种圆的表达形式 （x+x<sub>c</sub>）<sup>2</sup>+（y+<sub>c</sub>)<sup>2</sup>=c

​											  (**p** *−* **c**) *·* (**p** *−* **c**) *−* *r*<sup>2</sup>= 0   **c**=(x<sub>c</sub>,y<sub>c</sub>)

​											  ||**p** - **c**||=0

代码中使用矢量很有意义

#### 2.5.2 二维梯度

**梯度矢量**

$$
∇f(x, y) =(\frac{∂f}{∂x},\frac{∂f}{∂y})
$$
梯度垂直于该点的切平面，亦被称为法线

所以平面的梯度导数垂直于该平面。

偏导数

![image-20220221110155913](C:\Users\Saputello\AppData\Roaming\Typora\typora-user-images\image-20220221110155913.png)

*关于梯度坐标为什么偏导数的简单推导*

隐函数

*f*(x,y)=0

沿着切线方向满足
$$
Δf=\frac{∂f}{∂x}Δx+\frac{∂f}{∂y}Δy=0
$$
则法线方向可以取
$$
（\frac{∂f}{∂x}，\frac{∂f}{∂y})
$$
梯度的方向始终指向上坡（uphill）

**二维隐式直线**
$$
Ax + By + C = 0
$$
它的梯度是（A,B），显然垂直于该直线，且所指方向为正，反向为负

任取两点（x<sub>0</sub>,y<sub>0</sub>）,（x<sub>1</sub>,y<sub>1</sub>）

则直线为(*y*<sub>0</sub> *−* *y*<sub>1</sub>)*x* + (*x*<sub>1</sub> *−* *x*<sub>0</sub>)*y* + *x*0*y*1 *−* *x*<sub>1</sub>*y*<sub>0</sub> = 0,这个形式没有数值退化的情况

利用除法
$$
y=\frac{y_1-y_0}{x_1-x_0}x+\frac{x_1y_0-x_0y_1}{x_1-x_0}
$$
点到直线的距离
$$
d=\frac{f(a,b)}{\sqrt{A^2+B^2}}
$$
![image-20220221133553789](C:\Users\Saputello\AppData\Roaming\Typora\typora-user-images\image-20220221133553789.png)

这在三角形栅格化很有用

**隐式二次曲线**
$$
Ax^2 + Bxy + Cy^2 + Dx + Ey + F = 0
$$
包括椭圆，双曲线，抛物线，圆 ，线

#### 2.5.3 三维隐式曲面

$$
f(x, y, z)=0\\
P=(x,y,z)\\
f(P)=0
$$

#### 2.5.4 隐式曲面的曲面法向量

曲面法线是照明计算所必需的

曲面上p点的法线可由隐式函数的梯度给出
$$
\pmb{n}=∇f(\pmb{P})=(\frac{∂f(\pmb{\pmb{P}})}{∂x},\frac{∂f(\pmb{P})}{∂y},\frac{∂f(\pmb{P})}{∂z})
$$

#### 2.5.5 隐式平面

经过**a**且有法向量**n**的无限平面可由(**p** *−* **a**) *·* **n** = 0给出，**p**为该平面上任意位置的点

![image-20220221135429004](C:\Users\Saputello\AppData\Roaming\Typora\typora-user-images\image-20220221135429004.png)

有时平面可由**a**,**b**,**c**三个点给出，法线可由任意叉乘得到

**n** = (**b** *−* **a**) *×* (**c** *−* **a**)

于是，

(**p** *−* **a**) *·* ((**b** *−* **a**) *×* (**c** *−* **a**)) = 0     这个式子用几何好解释，容易产生有效代码

它的几何意义可以理解为由p−a、b−a和c−a定义的平行六面体的体积为零，即它们是共面的。只有当p和a、b、c在同一平面上时，这才可能成立。

用行列式表示
$$
\left|
\begin{array}{cccc}
    x−x_a   & y−y_a   & z−z_a\\
    x_b−x_a & y_b−y_a & z_b−z_a\\
    x_c−x_a & y_c−y_a & z_c−z_a
\end{array}
\right|
=0
$$
这两个方式都比较好用代码实现

**三维二次曲面**

例如球体

*f*(**p**)=(**p** *−* **c**)<sup>2</sup>− r<sup>2</sup> = 0

轴对称椭球体![image-20220221141341931](C:\Users\Saputello\AppData\Roaming\Typora\typora-user-images\image-20220221141341931.png)

**隐式曲面的三维曲线**

一个三维曲线可以由两个联立的隐式方程构造出来

*f*(**p**)=0，*g*(**p**)=0

#### 2.5.6 二维含参曲线

形式
$$
\left[
\begin{array}{ccc}
x\\y
\end{array}
\right]=\left[
\begin{array}{ccc}
g(t)\\f(t)
\end{array}
\right]
$$
经常用向量函数表示含参曲线

**p**=f(t)

这会使代码比较干净

这样的函数上的点可以看作随时间运动，即使它并不在移动

**二维含参直线**

经过**P**<sub>0</sub>=(x<sub>0</sub>,y<sub>0</sub>)和**P**<sub>1</sub>=(x<sub>1</sub>,y<sub>1</sub>)
$$
\left[
\begin{array}{ccc}
x\\y
\end{array}
\right]=\left[
\begin{array}{ccc}
x_0+t(x_1-x_0)\\y_0+t(y_1-y_0)
\end{array}
\right]
$$
向量形式**p**(*t*) = **p**<sub>0</sub> + *t*(**p**<sub>1</sub> *−* **p**<sub>0</sub>)

![image-20220223083849069](C:\Users\Saputello\AppData\Roaming\Typora\typora-user-images\image-20220223083849069.png)

或者**p**(*t*) = **o** + *t*(**d**)

此时，令**d**单位化，t便是线段的长度。

**二维含参圆**

中心（x<sub>c</sub>,y<sub>c</sub>）
$$
\left[
\begin{array}{ccc}
x\\y
\end{array}
\right]=\left[
\begin{array}{ccc}
x_c+r cos φ \\y_c+r sin φ
\end{array}
\right]
$$
椭圆
$$
\left[
\begin{array}{ccc}
x\\y
\end{array}
\right]
=
\left[
\begin{array}{ccc}
x_c+a cos φ \\y_c+b sin φ
\end{array}
\right]
$$

#### 2.5.7 三维含参曲线

*x* = *f*(*t*)*,* *y* = *g*(*t*)*,* *z* = *h*(*t*)*.*

向量形式
$$
\left[
\begin{array}
{ccc}
x\\y\\z
\end{array}
\right]
=
\pmb{p}(t)
$$
**三维含参直线**

向量形式最为简便**p** = **o** + t**d**

#### 2.5.8 三维含参曲面

$$
x = f(u, v), y = g(u, v), z = h(u, v)
$$

或者
$$
\left[
\begin{array}
{ccc}
x\\y\\z
\end{array}
\right]
=
\pmb{p}(u,v)
$$
例如，
$$
x = r cos φ sin θ,
y = r sin φ sin θ,
z = r cos θ
$$
![image-20220223091841631](C:\Users\Saputello\AppData\Roaming\Typora\typora-user-images\image-20220223091841631.png)
$$
θ = acos(\sqrt{x^2 + y^2 + z^2}), φ = atan2(y, x).
$$
过曲面上一点并控制其中一个参数不变，成为该曲面上的等参曲线，并且求导得到曲线的切向量。

通过这个方法，我们可以通过偏导数得到曲面上一点的法线。
$$
n = p_u × p_v
$$
方向朝外。



#### 2.5.9 曲线、曲面综述

隐式曲线、曲面用标量函数定义
$$
S = {p |f(p)=0}.
$$
含参曲线用一元向量函数定义
$$
S = {p(t)|t ∈ D }
$$
含参曲面用二元向量函数定义
$$
S= {p(t)|(u, v) ∈ D }
$$
隐式曲线、曲面法线由梯度给出，

含参曲线、曲面法线由偏导数给出。

### 2.6 线性插值

**p** = (1 *−* *t*)**a** + *t* **b**

常见的线性插值将x轴分为x<sub>1</sub>到x<sub>n</sub>，相对应y<sub>1</sub>到y<sub>n</sub>.
$$
f(x)=y_i+\frac{x-x_i}{x_{i+1}-x_i}(y_i+1-y_i)
$$
将每一段看作(1-t)A+tB,即
$$
t=\frac{x-x_i}{x_{i+1}-x_i}
$$

### 2.7 三角形

#### 2.7.1 平面三角形

坐标a,b,c三点的的三角形面积
$$
\begin{aligned}
s&=\frac{1}{2}
\left|
\begin{array}
{ccc}
x_b-x_a&x_c-x_a\\
y_b-y_a&y_c-y_a
\end{array}
\right|
\\
&=\frac{1}{2}(x_ay_b+x_by_c+x_cy_a-x_ay_c-x_by_a-x_cy_b)
\end{aligned}
$$
a,b,c为逆时针时正，否则为负

![image-20220223192754413](C:\Users\Saputello\AppData\Roaming\Typora\typora-user-images\image-20220223192754413.png)

用重心坐标系给三角形建系（非正交坐标系）

任意点p可写为
$$
p = a + β(b − a) + γ(c − a)\\
即p = (1 − β − γ)a + βb + γc\\
令α ≡ 1 − β − γ\\
p(α, β, γ) = αa + βb + γc,α + β + γ = 1.
$$
其中一个坐标为0时，p位于边缘上；两个为0即为端点。

重心坐标系以相对平滑的方式混合了三个顶点的坐标，这种方式也可以用于其他特性

计算p点重心坐标系坐标的方式
$$
\left[
\begin{array}
{ccc}
x_b-x_a&x_c-x_a\\
y_b-y_a&y_c-y_a
\end{array}
\right]
\left[
\begin{array}
{ccc}
β
\\
γ
\end{array}
\right]
=
\left[
\begin{array}
{ccc}
x_p-x_a\\
y_p-y_a
\end{array}
\right]
$$
重心坐标系可以体现出点到三角形边的比例距离

![image-20220224162221989](C:\Users\Saputello\AppData\Roaming\Typora\typora-user-images\image-20220224162221989.png)

如
$$
β=\frac{f_{ac}(x,y)}{f_{ac}(x_b,y_b)}
$$
同理可得α，γ

先计算经过P<sub>0</sub>、P<sub>1</sub>直线的一种形式，在求出重心坐标系坐标
$$
\begin{align}
&(1)f_{ab}(x, y) ≡ (y_a − y_b)x + (x_b − x_a)y + x_ay_b − x_by_a = 0\\
&(2)γ=\frac{(y_a − y_b)x + (x_b − x_a)y + x_ay_b − x_by_a}{(y_a − y_b)x_c + (x_b − x_a)y_c + x_ay_b − x_by_a}\\
&β=\frac{(y_a − y_c)x + (x_c − x_a)y + x_ay_c − x_cy_a}{(y_a − y_c)x_b + (x_c − x_a)y_b + x_ay_c − x_cy_a}\\
&(3)α = 1 − β − γ.
\end{align}
$$
还有一种方法则通过三个子三角形的面积来计算重心坐标系坐标。

![image-20220227193051112](C:\Users\Saputello\AppData\Roaming\Typora\typora-user-images\image-20220227193051112.png)

![image-20220227193130987](C:\Users\Saputello\AppData\Roaming\Typora\typora-user-images\image-20220227193130987.png)

![image-20220227193208259](C:\Users\Saputello\AppData\Roaming\Typora\typora-user-images\image-20220227193208259.png)

#### 2.7.2 空间三角形

![image-20220227193543627](C:\Users\Saputello\AppData\Roaming\Typora\typora-user-images\image-20220227193543627.png)

法线可以通过叉乘得到

**n** = (**b** *−* **a**) *×* (**c** *−* **a**)

三角形面积
$$
S=\frac{1}{2}\|(\pmb{b}-\pmb{a})×(\pmb{c}-\pmb{a})\|
$$
这个面积是没有符号的，我们需要判断三角形的方向来判定符号

顺时针方向和逆时针方向的三角形法线方向相反。

> 补充有向三角形
>
> 有向三角形是解析几何术语，指规定了三个顶点的顺序的三角形。平面上不共线的三点P<sub>1</sub>，P<sub>2</sub>，P<sub>3</sub>可有两种顺序，若三点按逆时针方向排列，则称△P<sub>1</sub>P<sub>2</sub>P<sub>3</sub>为正向三角形；若三点按顺时针方向排列，则称△P<sub>1</sub>P<sub>2</sub>P<sub>3</sub>为负向三角形。这样规定了方向的三角形称为有向三角形。![image-20220227195919670](C:\Users\Saputello\AppData\Roaming\Typora\typora-user-images\image-20220227195919670.png)
>
> * 摘自百度百科 [有向三角形]([有向三角形_百度百科 (baidu.com)](https://baike.baidu.com/item/有向三角形/18893498))]

