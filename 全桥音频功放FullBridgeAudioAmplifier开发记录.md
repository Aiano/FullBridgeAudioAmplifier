# 全桥音频功放FullBridgeAudioAmplifier开发记录

## 指标要求

> 要求：
>
> [盟升杯高年级组A题题目指标相关Q&A (qq.com)](https://docs.qq.com/doc/DRkJyb095dlBBeEtx)
>
> [2024年盟升杯高年级组-电源题(A题)](2024年盟升杯高年级组-电源题(A题).pdf)

| 项目              | 参数                                | 单位 | 备注                                                         |
| ----------------- | ----------------------------------- | ---- | ------------------------------------------------------------ |
| 供电电压          | 24±1（DC）                          | V    |                                                              |
| 输入信号频率范围  | 80~3.4k                             | Hz   | 人耳听觉范围20~20k，但大多数人听不到这个范围                 |
| 输出电压          | 0~16±0.1                            | V    | 自动增益控制                                                 |
| 增益波动          | <3                                  | dB   | 80Hz, 1000Hz, 3400Hz三个频点，输入信号20mV（或其他相同幅值）正弦波 |
| 输出电流          | 2                                   | A    |                                                              |
| 输出频率误差      | <0.2                                | Hz   |                                                              |
| 总谐波失真（THD） | <2                                  | %    |                                                              |
| 效率@2A           | >95                                 | %    |                                                              |
| 负载              | 5                                   | Ω    |                                                              |
| 拓扑              | 单相全桥逆变电路                    |      |                                                              |
| 调制方式          | 单极倍频调制                        |      |                                                              |
| 工作模式          | 固定输出16V/400Hz正弦波 或 音频功放 |      | 软件切换                                                     |
| 重量              | <200                                | g    |                                                              |
| 输入接口          | 3.5mm麦克风接口                     |      |                                                              |
| 输出接口          |                                     |      |                                                              |
| 保护功能          | 过流保护、防自激                    |      |                                                              |

## 硬件仿真

### 全桥逆变器Simulink仿真

> [单相全桥逆变原理及仿真实验-CSDN博客](https://blog.csdn.net/lwb450921/article/details/128514857)

- 基波频率$f_c=3.6\text{kHz}$
- LC滤波器截至频率$f_r=40\text{kHz}$
- 载波频率$f_s=500\text{kHz}$

三者之间满足：
$$
10f_c<f_r<\frac{1}{10}f_s
$$
滤波器截至频率：
$$
f_r=\frac{1}{2\pi\sqrt{LC}}
$$
经过计算，LC乘积为：
$$
LC=99.5\times10^{-12}
$$
故选择：

- $L=10\mu H$
- $C=10\mu F$

仿真模型：

![image-20241016232615486](D:\Projects\FullBridgeAudioAmplifier\全桥音频功放FullBridgeAudioAmplifier开发记录\image-20241016232615486.png)

仿真波形：

![image-20241016232754339](D:\Projects\FullBridgeAudioAmplifier\全桥音频功放FullBridgeAudioAmplifier开发记录\image-20241016232754339.png)

![image-20241016232805000](D:\Projects\FullBridgeAudioAmplifier\全桥音频功放FullBridgeAudioAmplifier开发记录\image-20241016232805000.png)

提高三角波电压幅值，输出正弦波幅值减小：

![image-20241016234721998](D:\Projects\FullBridgeAudioAmplifier\全桥音频功放FullBridgeAudioAmplifier开发记录\image-20241016234721998.png)

![image-20241016234732224](D:\Projects\FullBridgeAudioAmplifier\全桥音频功放FullBridgeAudioAmplifier开发记录\image-20241016234732224.png)