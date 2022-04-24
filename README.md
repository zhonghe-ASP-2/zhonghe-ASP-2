# zhonghe-ASP-2



## 组织结构

0. 说明文档：

[zhonghe-ASP-2](https://github.com/zhonghe-ASP-2/zhonghe-ASP-2)



1. 征兆离散化：

[TimeSeriesMaker](https://github.com/zhonghe-ASP-2/TimeSeriesMaker)： 用于时序数据的生成和测试

[modbus2IoTDB](https://github.com/zhonghe-ASP-2/modbus2IoTDB)：用于模拟机生成的时序数据，并且导入到IoTDB之中

[feature_judge_template](https://github.com/zhonghe-ASP-2/feature_judge_template)：18种征兆判断的具体算法实现

[zhonghe_massive_EDA](https://github.com/zhonghe-ASP-2/zhonghe_massive_EDA)：用于算法的expoloresive data analysis的若干方法，目前使用过一些动态阈值和FFT的检测方法。



2. 规则预警：

[alarm_style](https://github.com/zhonghe-ASP-2/alarm_style)：预警样式

[evidence_reasoning_test](https://github.com/zhonghe-ASP-2/evidence_reasoning_test)： 规则推理覆盖性测试



3. 整体架构：

[zhonghe_reimplementation](https://github.com/zhonghe-ASP-2/zhonghe_reimplementation)：在DWF中运行的整体逻辑和运行环境

[streaming_process](https://github.com/zhonghe-ASP-2/streaming_process)：流式计算的框架，分为IoTDB的trigger处理，producer和consumer



备注：

+ pytest的覆盖性测试贯穿在征兆离散化，规则推理和整体流程之中。



## 具体模块说明

###  征兆离散化

周老师负责，具体可见word说明文档和相关的判断流程



### 规则预警

郭老师负责



### 与DWF开发相关



#### 在DWF中整体运行思路

当运行一个检测方案的时候，需要按照下面的步骤对相关的参数进行设置：

1. 标准测点的准备：1RCP604MP, 1RCP606SD, 1RCV036MD, 1RCP609MT, 1RCP610MT,     1RCP606MT, 1RCP607MT
2. FEG树的准备，包括零件-功能-FMECA-征兆（选择关联的中性测点）-规则的顺序进行创建。 征兆上自定义的一些参数( 能否添加一键展开的功能，否则每次逐层的点开比较的繁琐)
3. 实例测点准备，并且创建的时候，选择关联的标准测点。实例测点上自定义的参数606SD测点没有，仅有604配置了测点参数，其余的仅有时序数据路径，但是没有配置时序数据处理参数。

4. 创建实例设备，选择相关的中性零件。实例设备上关联实例测点。（目前都是中性的征兆公用，实例化；若以后有针对性地参数设置，需要在第一步的时候就创建实例的征兆，并且在后续的分析任务的时候，自动判断是否有实例化的征兆，从而选择是中性的征兆进行判断还是实例的征召进行判断）

5. 创建分析算法，上传主函数和配置文件。

6. 创建分析方案，选择相关的实例设备，并且自动化的关联相关的FMECA。

7. 以上步骤全部完成，现在需要调整python的运行流程以及debug，最后产生相关的结果。







