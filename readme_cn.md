# Stealthburner_Toolhead_PCB

## 简介

适用于Voron StealthBurner的3D打印工具板，基于RP2040控制器

![](/Document/pic/v1.1t.png)

![](/Document/pic/v1.1b.png)

* RP2040 控制器，使用USB连接上位机
* TMC2209 挤出机电机驱动
* MAX31865 铂电阻传感器
* Si7021 温湿度传感器
* ADXL345 加速度计
* 两个5pin风扇接口，支持2/3/4线，12/24V
* 一个3pin探头接口
* 一个普通NTC接口
* 一个2pin的x轴限位接口
* 一个3pin的5V WS2812 LED接口
* 一个24V发热棒接口

## [配置文件参考](klipper_config.cfg)

## [Programming Guide](Document/programming_cn.md)

## 细节
### 控制器
STM32价格疯了，RP2040只要8块钱

RP2040支持UART和USB，考虑到抗干扰选择了USB连接，不支持CANbus

### MAX31865
板载MAX31865传感器，支持2/3/4线，PT100/1000铂电阻。请自行选择参考电阻(430R/4.3K)和电容(100nF/1uF)，根据需要设置跳线并进行短接，请参考[Datasheet](https://datasheets.maximintegrated.com/en/ds/MAX31865.pdf)，详细设置见[此处](Document/max31865_cn.md)

### Si7021
用于测量箱温，价格昂贵且供货不稳定，不推荐焊接。DS18B20只能直接连接到上位机，用不了。如果使用了铂电阻测温可以利用空闲的NTC测量箱温

### ADXL345
共振测量，其实只会用到那么一两次，ADXL343和ADXL345都能用

### 风扇
支持传统2线制，3线制（方波转速检测输出）和4线制（PWM输入和转速检测），12/24V电压选择通过跳线设置
注意若使用12V电压，需注意风扇所需电流不可超过DC-DC最大电流

### 加热棒
选型时注意，需要N沟道耐压30V，并且在4.5V栅极电压有较低导通电阻的

### Neopixel LED
需注意板上5V是LDO输出，能力有限，不可串联过多灯珠

### DC-DC
支持多种有相同pinout的选择，请见原理图

电感使用4x4mm封装，厚度需要尽量低，2mm以内为佳

**电感参考选型**
* FHD4012 (长江微电)
* SLW4010 (Sunltech韩国顺磁)
* WPN4012H (Sunlord顺络)
* SPH4012S PH4018 (Sunlord顺络)
* SWPA4010 SWPA4018 SWPA4020 (Sunlord顺络)

**DC-DC参考选型**
* LMR14006
* LMR14010
* LMR54410(未测试) 
* MP2451(未测试)
* ~~BL9342(不推荐)~~
