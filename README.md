# STorM32_Gimbal项目简介

<table>
  <tr>
    <td width="50%">
      <img src="https://github.com/user-attachments/assets/0c473fa2-4649-4ee6-bf2f-c77e58dbf4f5" width="100%" />
    </td>
    <td width="50%">
      <img src="https://github.com/user-attachments/assets/4dfc6341-fdcd-4deb-a17a-ca13e4600e9a" width="100%" />
    </td>
  </tr>
</table>

手持三轴云台项目基于storm32开发，重新设计电路部分删除冗余部分，结构采用钣金折弯设计，作为DIY大幅降低可玩性成本。<br>
修改结构可作为吊舱三轴云台挂载无人机使用，电路固件通用。

**版本说明**
* 硬件版本参考主板V3.3i、驱动器编码器版V42EC-g4和陀螺仪V42-g4。主控采用STM32F103RCT6，其余模块主控采用是STM32G431KBU3。
* 当前硬件使用版本：主控板V1.1、电控板V1.1、IMU板V1.0。
* 固件采用官方最新的即可，注意要选择Nt带有编码器的版本。
* 虽然V42EC-g4的电机驱动带有电流检测，但是目前版本固件还未支持。所以电控板也可以选择DRV8313版本的。

## Gimbal主控板V1.1
只保留了主控电源另增加电位器摇杆用于控制YAW轴和Pitch轴的移动，需要在o323BGCTool中Rc Inputs设置为POT0和POT1通道。

## 首次使用
| 指令 | 解释 |
| --- | --- |
| setmodeltle5012b; | 设置编码器类型 |
| r2setrange 45; | 设置来回旋转角度 |
| r2sppofs +11; | 设置电机方向和极对数 |

使用这3条命令就能完成电机零点和极对数的设置，更详细的指令可以参考NT Module CLI。

可以选择组装完校准和未组装前校准，区别在于未组装前校准电机能够进行360度旋转，校准数据准确些，但实际测试区别并不明显，为了方便我都是组装完成后再进行校准操作。

* 根据IMU板的安装位置设置Z轴和X轴的方位；
* 设置完位置将云台放置水平运行1-Point Acc Calibration；
* 使用CLI Tool设置编码器类型和极对数；
* 逐次打开各个电机设置电机方向；
* 将云台放置水平获取当前编码器位置；
* 调整PID参数。

## 外部控制

支持多种外部控制模式，推荐两种比较简单易用的一种手持使用电位器摇杆进行控制移动，一种无人机吊舱串口控制发送角度。


原作者可参考：https://www.olliw.eu/storm32bgc-v2-wiki/Main_Page<br>
GitHub：https://github.com/olliw42/storm32bgc<br>
论坛：https://www.rcgroups.com/forums/showthread.php?2838548-T-STorM32-The-best-STorM32-ever-%21
