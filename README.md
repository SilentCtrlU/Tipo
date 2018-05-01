# Tipo
Quick markdown of every-day powerup
Stay awhile and listen.....

## STM32 MCU Firmware Development
Part 0: Keil MDK Development Environment.

  推荐下载STM32_StdPeripheral_Lib，根据工程模板Template直接开始，在设定Group选项时，关注Include路径，预编译选项和仿真器设定.
  
Part 1: Peripheral I2C use.

  STM32F10xx系列的硬件I2C存在著名的Bug：[Racede](https://racede.me/talk_about_stm32_i2c_peripheral.html) 从寄存器原理和时序的角度给出了Bug的原因和建议规避方法，这一I2C bug使得STM系列的MCU在面对I2C外设处理时通常选用GPIO模拟的方法，完整模仿I2C的完整时序。基础的GPIO模拟I2C的程序比较简单，关键在于ACK逻辑的处理，在完成读写单字节数据后，应当根据芯片参考手册编写多字节读写数据的函数.
  
  另一方面，STM针对其硬件I2C的Bug也做出了许多努力，如[STM8L I2C程序第二次数据通信失败的问题分析](https://www.stmcu.com.cn/Designresource/design_resource_detail?file_name=STM8L+I2C%E7%A8%8B%E5%BA%8F%E7%AC%AC%E4%BA%8C%E6%AC%A1%E6%95%B0%E6%8D%AE%E9%80%9A%E4%BF%A1%E5%A4%B1%E8%B4%A5%E7%9A%84%E9%97%AE%E9%A2%98%E5%88%86%E6%9E%90&lang=EN&ver=1)，[一个判断I2C总线通信异常的原因](https://www.stmcu.com.cn/Designresource/design_resource_detail?file_name=%E4%B8%80%E4%B8%AA%E5%88%A4%E6%96%ADI2C%E6%80%BB%E7%BA%BF%E9%80%9A%E4%BF%A1%E5%BC%82%E5%B8%B8%E5%8E%9F%E5%9B%A0%E7%9A%84%E6%96%B9%E6%B3%95&lang=EN&ver=1)
  
  在F10xx系列上，官方推荐的方法是采用DMA+中断处理的方式处理多字节读写，更进一步，推荐使用HAL库和Cube直接配置I2C外设.
  
  在F0xx系列上，官方有两例I2C例程（EEPROM，板载温湿度，主从通信）使用了CPAL库进行I2C的操作，如果一定要使用官方库的I2C，请配置好时钟和GPIO速率.
