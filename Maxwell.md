# Maxwell

---

[toc]

---

## 1 仿真流程

### 1.1 ANSYS Maxwell 电磁场有限元仿真的一般流程

<img src="F:\NOTE\Maxwell.assets\image-20230921152645757.png" alt="image-20230921152645757" style="zoom:80%;" />

### 1.2 ANSYS Workbench 多物理场耦合仿真的一般流程

![image-20230921153044306](F:\NOTE\Maxwell.assets\image-20230921153044306.png)

---

## 2 几何建模

###　2.1 坐标系简介

* 全局坐标系
* 相对坐标系
* 表面坐标系
* 实体坐标系

![image-20230921153945040](F:\NOTE\Maxwell.assets\image-20230921153945040.png)

<img src="F:\NOTE\Maxwell.assets\image-20230921153955336.png" alt="image-20230921153955336" style="zoom:150%;" />

### 2.2 基本模型绘制方法

* 点、线、面、体的绘制

* 螺旋线的绘制

* 参数方程曲线的绘制

  <img src="F:\NOTE\Maxwell.assets\image-20230921154059341.png" alt="image-20230921154059341" style="zoom:150%;" />

### 2.3 几何操作方法

* 布尔运算    unite加法  subtract减法  intersect取交集  split分割  imprint印记

<img src="F:\NOTE\Maxwell.assets\image-20230921154401060.png" alt="image-20230921154401060" style="zoom:150%;" />

* 等比例放大、缩小和拉伸、扫描

<img src="F:\NOTE\Maxwell.assets\image-20230921154821859.png" alt="image-20230921154821859" style="zoom:80%;" />

<img src="F:\NOTE\Maxwell.assets\image-20230921154856347.png" alt="image-20230921154856347" style="zoom:150%;" />

* 位置变换和复制

<img src="F:\NOTE\Maxwell.assets\image-20230921155025724.png" alt="image-20230921155025724" style="zoom:150%;" />

* 圆角和倒角

<img src="F:\NOTE\Maxwell.assets\image-20230921155151583.png" alt="image-20230921155151583" style="zoom:150%;" />

>注意**设置选择模式**
>
>![image-20230921155445462](F:\NOTE\Maxwell.assets\image-20230921155445462.png)

### 2.4 UDP快速建模

<img src="F:\NOTE\Maxwell.assets\image-20230921160604145.png" alt="image-20230921160604145" style="zoom:90%;" />

* 双击CreateUserDefinePart可弹出参数设置对话框
* 其中每个参数的意义可去help文档查找

<img src="F:\NOTE\Maxwell.assets\image-20230921160153292.png" alt="image-20230921160153292" style="zoom:120%;" />

<img src="F:\NOTE\Maxwell.assets\image-20230921160207425.png" alt="image-20230921160207425" style="zoom:90%;" />

### 2.5 参数化方法在建模中的应用

* 直接在value框中填入自定义变量名

<img src="F:\NOTE\Maxwell.assets\image-20230921161452518.png" alt="image-20230921161452518" style="zoom:90%;" />

* 在项目的properties属性栏中可查看和更改所有的参数化变量

![image-20230921161516867](F:\NOTE\Maxwell.assets\image-20230921161516867.png)

### 2.6 外部几何模型导入

![image-20230921161815611](F:\NOTE\Maxwell.assets\image-20230921161815611.png)

### 2.7 RMxprt快速建模

#### 2.7.1 步骤

##### 1 模型选择

![image-20230921164631721](F:\NOTE\Maxwell.assets\image-20230921164631721.png)

![image-20230921164746604](F:\NOTE\Maxwell.assets\image-20230921164746604.png)<img src="F:\NOTE\Maxwell.assets\image-20230922160124489.png" alt="image-20230922160124489" style="zoom:70%;" />

* maxwell model wizard属于利用RMxprt工具包建立maxwell有限元模型，并不能进行快速性能分析，所以一般选择generate RMxprt solutions
* machine type如果选择general，则属于普通通用旋转电机建模方法，一般在电机类型选择库中没有需要的电机类型的话可以选择这个
* 如果属于常见电机，可以选择standard

##### 2 设置电机默认选项 machine

![image-20230921165053074](F:\NOTE\Maxwell.assets\image-20230921165053074.png)

##### 3 设置定子参数 stator

* **slot** 槽型
* **winding**绕组

![image-20230921165219450](F:\NOTE\Maxwell.assets\image-20230921165219450.png)

##### 4 设置转子参数 rotor

![image-20230921165625807](F:\NOTE\Maxwell.assets\image-20230921165625807.png)

##### 5 设置转轴属性 shaft

![image-20230921165748090](F:\NOTE\Maxwell.assets\image-20230921165748090.png)

##### 6 求解设定

​	一般将额定工作状态设定为分析对象

![image-20230921165907034](F:\NOTE\Maxwell.assets\image-20230921165907034.png)

##### 7 模型检测

![image-20230922073412636](F:\NOTE\Maxwell.assets\image-20230922073412636.png)

##### 8 仿真计算

![image-20230922073451843](F:\NOTE\Maxwell.assets\image-20230922073451843.png)

##### 9 计算结果及特性曲线查看

![image-20230922162028339](F:\NOTE\Maxwell.assets\image-20230922162028339.png)

* RMxprt Report：主要是查看相关的特性曲线及3D曲面

* Solution Data：[参考](# 1 查看求解数据)

##### 10 模型生成导出

1. RMxprt的**design setting**

   ![image-20230922163829845](F:\NOTE\Maxwell.assets\image-20230922163829845.png)     ![image-20230922163518422](F:\NOTE\Maxwell.assets\image-20230922163518422.png)

   * Enable 不勾选：导出模型为默认最优的周期几何模型，即导出1/k模型  k为槽数和极数的最大公约数
   * Enable 勾选：在空白栏中输入 “Fractions”+“空格”+“数字”
     * 输入1，导出完整模型
     * 输入4，导出全模型的1/4
     * 数字必须满足 未勾选enable 时的导出原则，即为公约数  例如4极42槽，若Fractions设为4，模型也只能导出1/2
   * 项目模型属性中可查看修改Fractions

   <img src="F:\NOTE\Maxwell.assets\image-20230923081937459.png" alt="image-20230923081937459" style="zoom:80%;" />

2. **create maxwell design**

   **需要先analyze**

   ![image-20230922073722381](F:\NOTE\Maxwell.assets\image-20230922073722381.png)

#### 2.7.2 修改模型参数

>* ***RMxprt导出的模型不需要再进行额外设置即可直接执行计算程序**
>* 若需要 ，可参考本节
>* P146

##### 1 模型参数修改

导出的2D模型中，系统还自动生成了一些求解域：运动域（band）、内部域（interRegion）、外部域（outRegion）、轴（shaft），并将气材料设置为真空（vacuum）

![image-20230923075104739](F:\NOTE\Maxwell.assets\image-20230923075104739.png)

##### 2 边界条件、激励设置、网格划分等前处理修改

##### 3 电感及二维斜槽求解设定

##### 4 求解设置

#### 2.7.3 RMxprt自定义槽型

![image-20230922073958573](F:\NOTE\Maxwell.assets\image-20230922073958573.png)

![image-20230922074038114](F:\NOTE\Maxwell.assets\image-20230922074038114.png)

---

## 3 前处理

### 3.1 建立模型

![image-20230922080556996](F:\NOTE\Maxwell.assets\image-20230922080556996.png)

### 3.2 设定求解类型   Solution Type

> **7-specifying the solver type 指定求解器类型**

![image-20230922081746328](F:\NOTE\Maxwell.assets\image-20230922081746328.png)

![image-20230922081819589](F:\NOTE\Maxwell.assets\image-20230922081819589.png)![image-20230922082526691](F:\NOTE\Maxwell.assets\image-20230922082526691.png)

* Geometry Mode
  * Cartesian，XY：笛卡尔坐标系
  * Cylindrical about Z：圆柱坐标系
* 磁场
  * Magnetostatic：静磁场
  * Eddy Current：涡流场
  * Transient：瞬态场
* 电场
  * Electrostatic：静电场
  * AC Conduction：交流传导
  * DC Conduction：直流传导
  * Electric Transient：瞬态电场



### 3.3 材料库设置

#### 1 基础

![image-20230922083239240](F:\NOTE\Maxwell.assets\image-20230922083239240.png)

![image-20230922083359008](F:\NOTE\Maxwell.assets\image-20230922083359008.png)

* 右下角 **Export to Library**是将选中的材料导入到个人材料库

* 导入后，还需右上角三点那边加入

  ![image-20230922083623224](F:\NOTE\Maxwell.assets\image-20230922083623224.png)

#### 2 铁磁材料的添加

#### 3 永磁材料的属性设置

#### 4 导体材料的属性设置

#### 5 考虑温度修正的材料参数化设置

### 3.4 设定运动区域



### 3.5网格的类型及划分策略

#### 1 网格划分默认设置

​	**施加指定的剖分规则**

![image-20230922084852337](F:\NOTE\Maxwell.assets\image-20230922084852337.png)

* On Selection：对物体边界指定剖分规则
* Inside Selection：对物体内部指定剖分规则
* Surface Approximation：对曲面/线边界指定剖分规则
* Clone Mesh：柱面网格克隆部分规则



​	**指定初始网格剖分规则**

![image-20230922085524931](F:\NOTE\Maxwell.assets\image-20230922085524931.png)

​	**网格划分一般步骤**

1. 对模型各部件进行相应的网格划分设置

2. 右键setup求解器，选择generate mesh选项，使用求解器进行网格划分

   ![image-20230922092436705](F:\NOTE\Maxwell.assets\image-20230922092436705.png)

3. 右键模型，选择plot mesh即可得到模型剖分示意图

   ![image-20230922092548831](F:\NOTE\Maxwell.assets\image-20230922092548831.png)

4. 修改网格划分设置后，需先revert to initial mesh ，然后在generate mesh

![image-20230922100945427](F:\NOTE\Maxwell.assets\image-20230922100945427.png)

#### 2 基于表面/内部网格划分

##### （1）On Selection 剖分规则

![image-20230922092909113](F:\NOTE\Maxwell.assets\image-20230922092909113.png)



##### （2）Inside Selection剖分设置

![image-20230922101828399](F:\NOTE\Maxwell.assets\image-20230922101828399.png)

#### 3 曲线及曲面网格划分  Surface Approximation

​	对边界为曲线类的物体进行进一步的细致剖分，主要设定物体曲面或曲线边界的剖分网格分段数

![image-20230922102443054](F:\NOTE\Maxwell.assets\image-20230922102443054.png)

#### 4 网格克隆

​	针对具有较高的几何对称性的模型，通过网格克隆，使其相同几何结构的网格划分完全相同

##### （1）TAU 2D 网格克隆

​	[需先进行length based refinement设置](# （1）On Selection 剖分规则)

![image-20230922103154867](F:\NOTE\Maxwell.assets\image-20230922103154867.png)



#####　（2）3D 网格克隆

​	需要先cylindrical gap treatment 柱面气隙处理，才能进行3D 网格克隆

![image-20230922104713607](F:\NOTE\Maxwell.assets\image-20230922104713607.png)

### 3.6 激励源设置

#### 1 电流激励

![image-20230922145251067](F:\NOTE\Maxwell.assets\image-20230922145251067.png)

#### 2 电压激励

#### 3 外电路激励

#### 4 绕组激励面

​	选中对象，利用section生成激励面

![image-20230922155001072](F:\NOTE\Maxwell.assets\image-20230922155001072.png)

### 3.7 边界条件设定

![image-20230922110300713](F:\NOTE\Maxwell.assets\image-20230922110300713.png)

![image-20230922110354613](F:\NOTE\Maxwell.assets\image-20230922110354613.png)

![image-20230922110410294](F:\NOTE\Maxwell.assets\image-20230922110410294.png)

### 3.8 自定义监测参数设定

#### 1 电感参数

#### 2 非直接求解模型受力/转矩参数

​	选中需要分析的受力对象，右键打开菜单，选择assign parameters->force/torque，可分析受力/转矩

![image-20230922150137975](F:\NOTE\Maxwell.assets\image-20230922150137975.png)

​	待计算完毕，可查看该对象的受力分布   也可在 [solution data](# 1 查看求解数据)查看力的数值

![image-20230922151025817](F:\NOTE\Maxwell.assets\image-20230922151025817.png)

---

## 4 求解及后处理

### 4.1 求解参数设置

#### 1 稳态求解器

1. 静电场、静磁场、直流传导电场

2. 激励源均为非时变的恒定值

3. 建立求解器     求解器可添加多个，彼此相互独立，可用于求解不同工况

   ![image-20230922125507850](F:\NOTE\Maxwell.assets\image-20230922125507850.png)

#### 2  频域求解器

1. 涡流场、交流传导电场
2. 激励源均为随频率变化的正弦量

![image-20230922132410937](F:\NOTE\Maxwell.assets\image-20230922132410937.png)

#### 3 瞬态求解器

1. 瞬态磁场、瞬态电场
2. 激励源一般为时变的激励源

### 4.2 结果后处理

#### 1 查看求解数据

![image-20230922133039716](F:\NOTE\Maxwell.assets\image-20230922133039716.png)

* performance：计算结果
* design sheet：将performance中所有计算结果以报告形式呈现
* curves：查看相关的特性曲线图

![image-20230922162507398](F:\NOTE\Maxwell.assets\image-20230922162507398.png)

#### 2 生成结果报表

![image-20230922133426009](F:\NOTE\Maxwell.assets\image-20230922133426009.png)

![image-20230922133447291](F:\NOTE\Maxwell.assets\image-20230922133447291.png)

#### 3 绘制场量图

![image-20230922134445606](F:\NOTE\Maxwell.assets\image-20230922134445606.png)

#### 4 场图动画生成及不同参数下结果查看

#### 5 场计算器后处理



---

## 附1  Motor-CAD  电磁、热分析

---

## 附2 ANSYS optiSLang 优化设计

---

## 附3 Maxwell-Fluent 电磁-热耦合

---

## 附4 基于 workbench 振动噪声特性多物理场耦合仿真

---

## 附5 simplorer联合仿真 

---

## END
