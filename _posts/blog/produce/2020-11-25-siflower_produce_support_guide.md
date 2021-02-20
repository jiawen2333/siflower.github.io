---
layout: post
title: 方案以及生产支持说明手册
categories: PRODUCE
description: 介绍siflower方案及生产支持
keywords: produce 
mermaid: true
---


# siflower方案及生产支持手册

**目录**

* TOC
{:toc}

## 1 介绍

本文主要介绍siflower方案产品落地生产需要具备的条件和矽昌提供的相关的支持，

### 1.1 适用人员

需要了解siflower方案的人员、siflower方案产品开发人员

## 2 相关引用

[快速入门手册](https://siflower.github.io/2020/08/05/quick_start/)

[新的版型引入指南](https://siflower.github.io/2020/09/08/newBoardImportGuide/)

[Siflower软件服务介绍](https://siflower.github.io/2020/07/31/siwifi_software_guide/)

[PCBA工具使用说明]()

[PCBA板端说明]()

## 3 方案支持说明

```mermaid
graph LR
A[项目立项]-->B[获取SDK/HDK]-->C[硬件设计/软件开发]-->D[各项测试]-->E[软件release]-->F[产测准备]-->G[生产支持]-->H[后续维护]

```

### 3.1 软硬件设计

- 硬件设计
  
  客户确定立项后，由我们提供硬件HDK，客户进行客制化设计，我们提供相关支持。

- 软件设计

  SDK获取参考[快速入门手册](https://siflower.github.io/2020/08/05/quick_start/)，获取SDK后，客户进行软件客制化修改，我们提供相关技术支持。

### 3.2 硬件调试、软件调试

- 硬件调试

    前期设计好硬件后，我们提供相关原理图设计以及layout检查支持，便于有问题及时修改

- 软件开发

    软件方面，siflower相关软件服务可以参考[Siflower软件服务介绍](https://siflower.github.io/2020/07/31/siwifi_software_guide/)，目前提供的SDK集成了siwifi的以太网以及wifi驱动，已对接好的openwrt版本，可以满足客户开发需求，开发过程中出现任何问题可以向FAE窗口反馈。

- 性能测试
  
    在软件开发过程中我们也提供wifi/以太网测试说明，便于开发过程中调试，参考[以太网测试介绍](https://siflower.github.io/2020/09/08/ethernetTestGuide/)和[wifi测试手册]()

- 测试报告模板
  
  测试报告模板，可以点击[测试报告]()下载，这里提供的是没有数据的测试报告模板，需要用户自行按照里面的方法进行测试
  如果需要有测试数据的报告，请联系FAE，此类报告仅对签订立项或者签署了NDA的客户提供

  |测试类型|介绍|
  |--|--|
  |wifi射频测试测试报告|主要是射频部分测试|
  |wifi性能测试报告|使用Ixcharoit/iperf进行吞吐量测试|
  |以太网性能测试报告|主要以太网收发测试|
  |功能测试报告|提供详细的测试用例，针对每一项软件功能做测试|
  |压力测试报告|主要是利用脚本对DDR/flash读写，以太网断连，wifi压力测试|
  |老化测试报告|在高温箱环境对产品进行测试|

### 3.3 软件release

在所有硬件软件调试以及各项测试完成之后，可以对硬件进行定板，对应软件也可以发布生产版本。  
在调试时生成镜像可以通过make指令直接编译，软件release版本则是在确定了所有配置后，通过脚本编译带版型名称以及版本号的最终镜像，作为第一版镜像，并且制作FLASH生产烧录镜像

### 3.4 产测镜像/产测工具

- 产测镜像
  
    uboot + openwrt + pcba镜像

    简称带PCBA的镜像。该镜像主要用于工厂生产，需要与PC端的测试工具配合使用，与openwrt相比，pcba启动更快，便于批量测试，能够提升工厂的测试效率。使用该镜像将进入pcba镜像，进行WiFi的校准测试以及其他测试，全部完成后将由PC端软件发送命令结束pcba模式，这样下次上电后将启动openwrt系统，且带有WIFI校准参数，WiFi性能最优。
    
    需要将最后定版的openwrt镜像与uboot/pcba镜像打包在一起，生成完整的flash镜像，提供给产线做烧录  
    产测镜像说明参考[PCBA板端说明]()

- 产测工具
  
    我们同时也提供完整的产测工具对方案进行支持，产测工具需要结合产测镜像才能使用，该工具主要是用于产线wifi校准，pcba板硬件测试，以及mac地址等相关产品信息写入  
    产测工具说明参考[PCBA工具使用说明]()
    **注：如果需要对产测工具进行修改，请联系矽昌**

### 3.5 生产支持

客户在大批量生产之前需要到产线试产，在条件允许的情况下我们可以派专业的FAE在试产的时候到产线做支持，对注意事项进行说明以及对试产出现的问题做分析，尽最大可能规避大批量生产时候的风险。

### 3.6 后续维护

- 硬件维护
  
    在生产完成之后的一段时间，如果有机器出现硬件问题，而客户解决有困难，我们会在一段有限时间内进行支持，并且指导客户如何去解决，后续则交由客户处理

- 软件维护
  
    主要是针对机器出厂后，需要对机器进行升级维护  
    siflower软件有一个OTA升级的功能，可以对出厂的设备进行OTA升级更新，但是仅限于使用siflower管理网页的方案，其它方案则需要客户自行开发  
    siflower OTA软件升级说明参考[OTA升级开发手册](https://siflower.github.io/2020/07/31/ota_upgrade_guide/)
