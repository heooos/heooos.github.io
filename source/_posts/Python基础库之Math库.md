---
title: Python基础库之Math库
date: 2017-11-30 00:30:07
tags: [python,基础库,math库]
categories: Python
---

Python中提供了Math库，用于进行数学计算。

使用时，只需在文件开始导入即可**``import math``**

常用的函数及其功能如下表：

| 函数名                 | 函数功能                                     | 说明/示例                                    |
| ------------------- | :--------------------------------------- | :--------------------------------------- |
| math.acos(x)        | 返回 x 的反余弦                                |                                          |
| math.acosh(x)       | 返回 x 的反双曲余弦                              |                                          |
| math.asin(x)        | 返回 x 的反正弦                                |                                          |
| math.asinh(x)       | 返回 x 的反双曲正弦                              |                                          |
| math.atan(x)        | 返回 x 的反正切                                |                                          |
| math.atan2(y,x)     | 返回 y/x 的反正切                              |                                          |
| math.atanh(x)       | 返回 x 的反双曲正切                              |                                          |
| **math.ceil(x)**    | 返回≧ x 的最小整数                              | math.ceil(3.4)  結果 4.0                   |
| math.copysign(x,y)  | 返回与 y 同号的 x 值                            | math.copysign(-1.9, 2.9)     返回1.9       |
| math.cos(x)         | 返回 x 的余弦                                 |                                          |
| math.cosh(x)        | 返回 x 的双曲余弦                               |                                          |
| **math.degrees(x)** | 將 x (弧长) 转成角度，与 radians 为反函数             |                                          |
| **math.e**          | 常数   e = 2.7128...                       |                                          |
| math.exp(x)         | 返回 e<sup>x</sup>也就是 math.e**x            |                                          |
| **math.fabs(x)**    | 返回 x 的绝对值                                |                                          |
| math.factorial(x)   | 返回 x!                                    |                                          |
| **math.floor(x)**   | 返回 ≦ x 的最大整数                             | math.floor(3.4) 結果 3.0                   |
| math.fmod(x,y)      | 返回 x对y取模的余数fmod 类似 %，但产生的结果可能与%不同，因为前者以y来决定余数的符号，后者以x来决定余数的符号。 | print(-2%3,math.fmod(-2,3))返回 (1, -2.0)  |
| math.frexp(x)       | Return the mantissa and exponent of x, as pair (m, e).                                                        m is a float and e is an int, such that x = m * 2.**e.                                                                  If x is 0, m and e are both 0.  Else 0.5 <= abs(m) < 1.0. | math.frexp(1.625)               返回(0.8125,1) |
| math.fsum(x)        | 返回 x 阵列值的各項和（ 无损精度的和）                    | 0.1+0.2+0.3                          返回0.6000000000000001   math.fsum([0.1, 0.2,0.3])   返回0.6 |
| math.hypot(x,y)     | 返回 &radic;x<sup>2</sup>+y<sup>2</sup>  （以x和y为直角边的斜边长） | math.hypot(3,4)                  返回5.0   |
| math.isinf(x)       | 若x不是数字，返回True；否则，返回False                 | math.isnan(1.2e3)              返回False   |
| math.isnan(x)       | 如果 x = Non (not a number)返回 True         |                                          |
| math.ldexp(m,n)     | 返回 m×2n与 frexp 是反函数                      |                                          |
| math.log(x,a)       | 返回log<sub>a</sub>x 若不写a 默认为e             |                                          |
| math.log10(x)       | 返回log<sub>10</sub>x                      |                                          |
| math.modf(x)        | 返回 x 的小数部份与整数部份                          | math.modf(2.123)             返回 (0.1231230000000001, 2.0) |
| **math.pi**         | 常数  π (3.14159...)                       |                                          |
| **math.pow(x,y)**   | 返回 x<sup>y</sup>                         |                                          |
| math.radians(d)     | 将 x(角度) 转成弧长，与 degrees 为反函数              |                                          |
| math.sin(x)         | 返回 x 的正弦                                 |                                          |
| math.sinh(x)        | 返回 x 的双曲正弦                               |                                          |
| **math.sqrt(x)**    | 返回&radic;x                               |                                          |
| math.sqrt(x)        | 返回 x 的正切                                 |                                          |
| math.tanh(x)        | 返回 x 的双曲正切                               |                                          |
| math.trunc(x)       | 返回 x 的整数部份，等同 int                        |                                          |

