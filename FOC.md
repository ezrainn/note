# FOC

---

>以袁雷的**《现代永磁同步电机控制原理及MATLAB仿真》**为主，本文档做辅助用

---

## 1 数学建模

### 1.1 坐标变换

#### 1.1.1 Clark

1. 从自然坐标系ABC变换到静止坐标系α-β的变换 **Clark变换**
   1. 等幅值系数：**$\frac{2}{3}$**
   2. 等功率系数：**$\sqrt {\frac{2}{3}} $**

$$
{\left[ {\begin{array}{*{20}{c}}
  {{f_\alpha }}&{{f_\beta }}&{{f_0}} 
\end{array}} \right]^T} = {T_{3s/2s}}{\left[ {\begin{array}{*{20}{c}}
  {{f_A}}&{{f_B}}&{{f_C}} 
\end{array}} \right]^T}
$$


$$
{T_{3s/2s}} = \frac{2}{3}\left[ {\begin{array}{*{20}{c}}
  1&{ - \frac{1}{2}}&{ - \frac{1}{2}} \\ 
  0&{\frac{{\sqrt 3 }}{2}}&{ - \frac{{\sqrt 3 }}{2}} \\ 
  {\frac{{\sqrt 2 }}{2}}&{\frac{{\sqrt 2 }}{2}}&{\frac{{\sqrt 2 }}{2}} 
\end{array}} \right]
$$

2. 从静止坐标系α-β变换到自然坐标系ABC的变换 **反Clark变换**

$$
{\left[ {\begin{array}{*{20}{c}}
  {{f_A}}&{{f_B}}&{{f_C}} 
\end{array}} \right]^T} = {T_{2s/3s}}{\left[ {\begin{array}{*{20}{c}}
  {{f_\alpha }}&{{f_\beta }}&{{f_0}} 
\end{array}} \right]^T}
$$

$$
{T_{2s/3s}}{\text{ = }}T_{3{\text{s}}/2s}^{ - 1} = \left[ {\begin{array}{*{20}{c}}
  1&0&{\frac{{\sqrt 2 }}{2}} \\ 
  { - \frac{1}{2}}&{\frac{{\sqrt 3 }}{2}}&{\frac{{\sqrt 2 }}{2}} \\ 
  { - \frac{1}{2}}&{ - \frac{{\sqrt 3 }}{2}}&{\frac{{\sqrt 2 }}{2}} 
\end{array}} \right]
$$

| 正转 | <img src="F:\NOTE\FOC.assets\image-20230926083138934.png" alt="image-20230926083138934" style="zoom:67%;" /> | α超前β |
| ---- | ------------------------------------------------------------ | ------ |
| 反转 | <img src="F:\NOTE\FOC.assets\image-20230926083223162.png" alt="image-20230926083223162" style="zoom:67%;" /> | β超前α |

#### 1.1.2 Park

1. 从静止坐标系α-β变换到同步旋转坐标系d-q的变换  **park变换**
   $$
   {\left[ {\begin{array}{*{20}{c}}
     {{f_d}}&{{f_q}} 
   \end{array}} \right]^T} = {T_{2s/2r}}{\left[ {\begin{array}{*{20}{c}}
     {{f_\alpha }}&{{f_\beta }} 
   \end{array}} \right]^T}
   $$

   $$
   {T_{2s/2r}} = \left[ {\begin{array}{*{20}{c}}
     {\cos {\theta _e}}&{\sin {\theta _e}} \\ 
     { - \sin {\theta _e}}&{\cos {\theta _e}} 
   \end{array}} \right]
   $$

2. 从同步旋转坐标系d-q变换到静止坐标系α-β的变换  **反park变换**
   $$
   {\left[ {\begin{array}{*{20}{c}}
     {{f_\alpha }}&{{f_\beta }} 
   \end{array}} \right]^T} = {T_{2r/2s}}{\left[ {\begin{array}{*{20}{c}}
     {{f_d}}&{{f_q}} 
   \end{array}} \right]^T}
   $$

   $$
   {T_{2r/2s}}{\text{ = }}T_{_{2s/2r}}^{ - 1} = \left[ {\begin{array}{*{20}{c}}
     {\cos {\theta _e}}&{ - \sin {\theta _e}} \\ 
     {\sin {\theta _e}}&{\cos {\theta _e}} 
   \end{array}} \right]
   $$

3. d-q轴

   1. 控制d轴：控制磁场强弱（不需要） d轴与永磁体磁链方向相同
   2. 控制q轴：控制转矩大小（需要）

###  1.2 两种常用坐标系

| <img src="F:\NOTE\FOC.assets\image-20230925135836564.png" alt="image-20230925135836564" style="zoom:60%;" /> | 书本使用       | aligned with phase a axis      |
| ------------------------------------------------------------ | -------------- | ------------------------------ |
| <img src="F:\NOTE\FOC.assets\image-20230925140157065.png" alt="image-20230925140157065" style="zoom:55%;" /> | MATLAB自身使用 | 90 degrees behind phase a axis |

### 1.3 PMSM模块

#### 1.3.1 三类PMSM模块

<img src="F:\NOTE\FOC.assets\image-20230918152058813.png" alt="image-20230918152058813" style="zoom:80%;" />

#### 1.3.2 configuration 配置

![image-20230925163639633](F:\NOTE\FOC.assets\image-20230925163639633.png)

1. number of phases（相数）
2. back EMF wavefrom（反电动势波形）
   1. sinusoidal：**正弦波**激励
   2. trapezoidal：**梯形波**激励
3. rotor type（转子类型）
   1. salient-pole：凸极型  **内置式**
   2. round：圆柱型  **表贴式**
4. mechanical input（机械输入方式）
   1. torque Tm：**负载转矩**
   2. speed w：**机械角速度**
5. preset model（电机的类型）
   1. 选择no就可以修改电机参数
   2. 或者选择各种功率等级的电机

#### 1.3.3 parameters 参数

![image-20230925164551264](F:\NOTE\FOC.assets\image-20230925164551264.png)

1. Rs（定子相电阻）

2. Ls（定子相电感）

3. Ld Lq（d-q轴电感）

4. armature inductance（电枢电感）

5. Machine constant（电机常量值）

   1. Flux（永磁体磁链）Wb
   2. Voltage（线反电动势系数）V/krpm      ${v_{peak}} = \sqrt 2 {v_{rms}}$
   3. Torque（扭矩常数）N·m

6. Inertia（转动惯量）、viscous damping（阻尼系数）、pole pairs（极对数）和static friction（静摩擦力）

   viscous damping通常设置为0

7. Initial conditions[wm（rad/s）thetam（deg）ia，ib（A）]（电机的初始状态）：可以设置包括机械角速度、转子位置、相电流ia和ib在内的数值大小

#### 1.3.4 注意

1. 在[parameters](# 1.3.3 parameters 参数)参数设置中，最后一项rotor flux position when theta=0，注意选择[坐标系](# 1.2 两种常用坐标系)

2. 角度的换算

   1. 计算过程用的是电角度${\theta _e}$

   2. 电机输出的角度是机械角速度${\theta _m}$

   3. 需要将${\theta _m}$转换为${\theta _e}$       

      ${P_n}$为电机的极对数
      $$
      {\theta _e} = {P_n}{\theta _m}
      $$

   4. 当选择90 degrees behind phase a axis时，且其余坐标变换选择第一个坐标系（d-q在上），则需要$  - \frac{\pi }{2}$
      $$
      {\theta _e} = {P_n}{\theta _m} - \frac{\pi }{2}
      $$

#### 1.3.5 常用方法

![20200312135655314](F:\NOTE\FOC.assets\20200312135655314.png)

---

## 2 SVPWM

### 2.1 三相电量的空间矢量表示

​	外接圆半径为$\frac{2}{3}{U_{{\text{dc}}}}$   表示    合成的参考矢量幅值不超过$\frac{{\sqrt 3 }}{3}{U_{{\text{dc}}}}$，可保证输出电压不失真

![image-20230925213209896](F:\NOTE\FOC.assets\image-20230925213209896.png)

### 2.2 SVPWM 算法的实现

#### 2.2.1 参考电压的扇区判断

![image-20230926083558530](F:\NOTE\FOC.assets\image-20230926083558530.png)

#### 2.2.2 非零矢量和零矢量作用时间的计算

![image-20230926083628524](F:\NOTE\FOC.assets\image-20230926083628524.png)

* T~4~可以认为是第一个非零矢量的作用时间T~first~
* T~6~可以认为是第二个非零矢量的作用时间T~second~

#### 2.2.3 扇区矢量切换点的确定

![image-20230925214845081](F:\NOTE\FOC.assets\image-20230925214845081.png)

![image-20230925214853190](F:\NOTE\FOC.assets\image-20230925214853190.png)

​	输出的是马鞍波

#### 2.2.4 与三角载波比较

​	三角载波减去马鞍波，若大于0则该相导通

1. 三角载波底（周期）是PWM开关周期，即T~PWM~（T~S~）
2. 幅值是底的一半
3. 例如T~PWM~=0.0002，则三角载波的幅值为0.0001，周期为0.0002

<img src="F:\NOTE\FOC.assets\v2-bf22a358cd1f1a96a7eb5b737c4ba65d_r.jpg" alt="v2-bf22a358cd1f1a96a7eb5b737c4ba65d_r" style="zoom:80%;" />

---

## 3 SPWM

---



![速度-电流](F:\NOTE\FOC.assets\速度-电流.jpg)

![位置-速度-电流](F:\NOTE\FOC.assets\位置-速度-电流.jpg)


---







## MATLAB

### 数据字典

1. 建立数据字典



<img src="F:\NOTE\FOC.assets\image-20230918155944053.png" alt="image-20230918155944053" style="zoom: 80%;" />

2. 创建变量

![image-20230918161330072](F:\NOTE\FOC.assets\image-20230918161330072.png)

3. 修改变量名和变量参数

![image-20230918161423116](F:\NOTE\FOC.assets\image-20230918161423116.png)

​	需手动保存更改

![image-20230918161500539](F:\NOTE\FOC.assets\image-20230918161500539.png)

4. 将模型链接到数据字典

![image-20230918161617083](F:\NOTE\FOC.assets\image-20230918161617083.png)



![image-20230918161816222](F:\NOTE\FOC.assets\image-20230918161816222.png)

### 系统辨识 调节PID参数

### simulink 代码生成

1. 设置**离散的定步长算法**，并设置步长，大部分控制步长都设备为10ms（1e-5）
2. 选取代码生成的系统目标文件为ert.tlc

---

## STM32

### PWM

1. 定时器

   基本定时器、通用定时器、高级定时器

2. CNT 计数器当前值

   ARR 自动重装载值

   CCRx 捕获/比较寄存器值

   ![](F:\NOTE\FOC.assets\微信图片_20230918111901.jpg)

3. 定时器的定时时间（周期）
   $$
   T = \frac{{(psc + 1) \times (arr + 1)}}{{{T_{clk}}}}
   $$
   psc为预分频数

   arr为自动重装载值，在cubemx中为counter period

   T~clk~为定时器的输入时钟，例如72mHZ

4. 定时器的定时频率
   $$
   f = \frac{1}{T} = \frac{{{T_{clk}}}}{{(psc + 1) \times (arr + 1)}}
   $$

5. HAL库PWM控制函数

   ```c
   HAL_TIM_PWM_Start(&htim3,TIM_CHANNEL_2);//PWM启动函数
   HAL_TIM_PWM_Stop//PWM停止函数
   _HAL_TIM_SET_COMPARE//占空比
   _HAL_TIM_SET_AUTORELOAD//周期
   ```

   

6. 占空比

   在cubemx中设置pulse，占空比=pulse/arr

   ```c
   TIM3->CCR2 = NUM;
   //等同于
   _HAL_TIM_SET_COMPARE(&htim3,TIM_CHANNEL_2,num);
   //num为范围0~arr内的数字
   //占空比=num/arr
   ```

7. 死区

---

## 补充

### 欧拉公式

$$
e^{i\pi} + 1 = 0
$$

$$
{e^{i\theta }} = \cos \theta  + i\sin \theta
$$

### 均方根 RMS

1. 均方根值常用于测量数据集中的数值的离散程度或振幅

   在信号处理和电工领域中，均方根值也常用于表示信号的强度或振幅

2. 信号的均方根值是指一个信号在一定时间内的平方值的均值，然后再开平方根 **先平方、再平均、然后开方**

   这用于描述信号的有效振幅

3. 真实均方根值：这是一种精确计算均方根值的方法，可以适用于任何类型的波形，包括非正弦波。这种方法可以准确地反映信号的真实振幅

4. 基本均方根值：这种均方根值通常用于正弦波形的计算。对于正弦波，其均方根值可以通过幅值（振幅）除以来$\sqrt 2 $估算。这是因为正弦波的均方根值等于其振幅除以$\sqrt 2 $。这种估算方法对于纯正弦波形是准确的，但对于其他类型的信号可能不适用

$$
RMS(f(t)) = \sqrt {\frac{1}{T}\int\limits_{t - T}^t {f{{(t)}^2}dt} }
$$

---





