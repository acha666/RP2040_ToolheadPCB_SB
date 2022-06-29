# Stealthburner_Toolhead_PCB
**尚未完工，敬请期待**
## 简介
适用于Voron StealthBurner的3D打印工具板，基于RP2040控制器
* RP2040 控制器，使用USB连接上位机
* TMC2209 挤出机电机驱动
* MAX31865 铂电阻传感器
* SHT20 温湿度传感器
* ADXL345 加速度计
* 两个5pin风扇接口，支持2/3/4线，12/24V
* 一个3pin探头接口
* 一个普通NTC接口
* 一个2pin的x轴限位接口
* 一个3pin的5V WS2812 LED接口
* 一个24V发热棒接口

## [配置文件参考](klipper_config.conf)

## 细节
### 控制器
STM32价格疯了，RP2040只要8块钱
RP2040支持UART和USB，考虑到抗干扰选择了USB连接，不支持CANbus

### MAX31865
板载MAX31865传感器，支持2/3/4线，PT100/1000铂电阻。请自行选择参考电阻(430R/4.3K)和电容(100nF/1uF)，根据需要设置跳线并进行短接，请参考[Datasheet](https://datasheets.maximintegrated.com/en/ds/MAX31865.pdf)，详细设置见[此处](Document/max31865_cn.md)

### SHT20
用于测量箱温，SHT20目前NRND，可是klipper目前仅支持SHT20，DS18B20只能直接连接到上位机，用不了。如果使用了铂电阻测温可以利用空闲的NTC测量箱温

### ADXL345
共振测量，其实只会用到那么一两次，ADXL343和ADXL345都能用

### 风扇
支持传统2线制，3线制（方波转速检测输出）和4线制（PWM输入和转速检测），12/24V电压选择通过跳线设置

### 加热棒
选型时注意，需要N沟道耐压30V，并且在4.5V栅极电压有较低导通电阻的

### DC-DC
支持多种有相同pinout的选择，请见原理图

| Options |
| --- |
| BL9342(便宜) |
| LMR54410(未测试) |
| LMR14006(未测试) |
