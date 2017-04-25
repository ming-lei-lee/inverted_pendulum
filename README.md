# inverted_pendulum

电子科技大学2017电子设计竞赛校队控制组第一次训练，KZ-3组

小组成员：章程，韦仕才，徐瑶

采用ebox库，vs2015开发环境。[模板和使用说明](https://github.com/pidan1231239/ebox_stm32f103RCT6_VS#ebox_stm32f103rct6_vs)参考队长[章程](https://github.com/pidan1231239)的ebox_stm32f103RCT6_VS

- # 机械部分说明
    ## 材料选取及用途：
    > 3mm厚碳板和铜柱作为快装板和电机支撑，碳方管作为横梁，碳圆管作为摆杆，铝棒作为转轴，底部用三脚架支撑，连接处用法兰联轴器以及五转六的电机联轴以及绑扎带固定，采用导电滑环防止绕线。

- # 软件部分说明
  ## 重新编写编码器驱动```encoder_timer```

     可用引脚：
    > 高级定时器和通用定时器可以将ch1和ch2配置成正交编码器AB相输入

    TIM1~TIM4可用io口如下：
     > TIM1:PA8 PA9

     > TIM2:PA0 PA1

     > TIM3:PA6 PA7

     > TIM4:PB6 PB7

    本次倒立摆设计采用TIM1和TIM3配置正交编码器。用TIM2配置PWM控制电机

  ## 编写电机驱动```encoder_motor.h```

    > 设置速度和位置模式以及PID初始化


  ## 将光编码器作为绝对编码器使用
    > 计算摆杆的角加速度和角速度，以弧度制为单位


  ## 采用四级PID控制

    > 对摆杆角度、摆杆角速度、横梁角度、横梁角速度进行PID算法控制


  ## 采用状态机和四个独立键盘对倒立摆进行模式切换

    > 选择io如下：PB12 PB13 PB14 PB15

    > 对应模式：```Swing SwingInvert Invert Round```

    
  ## 用freertos设置进程
    > 实现多任务并行处理


- # 电路部分说明
  电路组成：
    > LM2596S-5.0作为降压模块

    >tb6612作为电机驱动

    > stm32f103c8t6最小系统作为主控

    > 四个独立按键

  电路设计：
    > 电机驱动模块插座

    >c8t6最小系统板插座

    > 降压模块插座

    >4pin xh2.56光编码器接口

    > 6pin xh2.56电机接口

    > 4pin xh2.56延长线

    > 12v电池插头