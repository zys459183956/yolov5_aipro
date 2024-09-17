# OrangePi AIPro 华为昇腾芯片高性能测试+AI 应用部署视频目标检测

## 一. OrangePi AIPro [开发板](https://so.csdn.net/so/search?q=开发板&spm=1001.2101.3001.7020)简介

### 1.1 简介

香橙派 AIpro 开发板是一款高性价比的边缘计算设备，搭载昇腾 AI 处理器，提供 8TOPS INT8 的计算能力，能够运行 Ubuntu 22.04 操作系统，为部署复杂的深度学习算法提供了坚实的硬件基础。香橙派 AIpro 开发板由香橙派和华为联合打造，搭载强大的昇腾处理器，提供 8TOPS INT8 的计算能力，适用于复杂的计算任务。开发板拥有丰富的接口，包括双 4K HDMI 输出、Type-C 电源接口、GPIO 接口、支持 SATA/NVMe SSD 2280 的 M.2 插槽、TF 插槽、千兆网口等，可广泛应用于 AI 边缘计算、深度视觉学习、视频图像分析、智能安防等领域，满足大多数 AI 算法原型验证和推理应用开发的需求。

#### 昇腾AI在线资料

在线课程
https://www.hiascend.com/edu/courses

在线文档
https://www.hiascend.com/document

### 1.2 主要参数

| 模块           | 规格                                                         |
| -------------- | ------------------------------------------------------------ |
| 昇腾 AI 处理器 | 4 核 64 位 Arm 处理器 <br /> AI 处理器                       |
| 内存           | LPDDR4X 类型 <br />容量8GB 或 16GB                           |
| Wi-Fi+蓝牙     | 支持 2.4G 和 5G 双频 WIFI                                    |
| USB            | 2 个 USB3.0 Host 接口 <br />1 个 Type-C 接口（只支持 USB3.0， 不支持 USB2.0） |
| 摄像头         | 2 个 MIPI CSI 2 Lane 接口                                    |
| 显示           | 2 个 HDMI 接口 <br />1 个 MIPI DSI 2 Lane 接口               |
| 音频           | 1 个 3.5mm 耳机孔， 支持音频输入输出<br /> 2 个 HDMI 音频输出 |
| 电源           | 支持 Type-C 供电， 20V PD-65W 适配器                         |
| 风扇接口       | 4pin， 0.8mm 间距， 用于接 12V 风扇， 支持 PWM 控制          |
| 调试串口       | Micro USB 接口的调试串口                                     |
| 支持的操作系统 | Ubuntu 22.04 和 openEuler 22.03                              |
| 规格           | 产品尺寸：107*68mm<br />重量：82g                            |

## 二、开箱展示

### 2.1开箱



<img src="file:///F:\下载\用户下载\文档\Tencent Files\459183956\Image\C2C\A7[CT`L}VC@%4UBDXZZMQWV.png" alt="img" style="zoom:50%;" />



![img](file:///F:\下载\用户下载\文档\Tencent Files\459183956\Image\C2C\f4da7120615dee51c5a269de0b3c24ff.jpg)

​                                                                                            图1 香橙派AIpro开发套件

### 2.2 开发板的接口详情图    

![image-20240718192540303](C:\Users\ZYS\AppData\Roaming\Typora\typora-user-images\image-20240718192540303.png)

​                                                                                                           正面视图

![image-20240718192632384](C:\Users\ZYS\AppData\Roaming\Typora\typora-user-images\image-20240718192632384.png)

​                                                                                                           背面视图

## 三、详细开发前准备步骤

### 3.1 下载OrangePi AIPro 开发板的镜像和相关的资料  

镜像有desktop版本和minimal版本，desktop版本有完整的桌面环境。minimal没有桌面环境，只能用命令行操作。根据需求进行选择，对linux不熟练推荐使用desktop带桌面环境的系统。

开发板资料下载页面的链接如下所示：  

```
http://www.orangepi.cn/html/hardWare/computerAndMicrocontrollers/service-and-support/Orange-Pi-AIpro.html
```

![image-20240718194407605](C:\Users\ZYS\AppData\Roaming\Typora\typora-user-images\image-20240718194407605.png)

![image-20240720131913994](C:\Users\ZYS\AppData\Roaming\Typora\typora-user-images\image-20240720131913994.png)

### 3.2 下载系统烧写工具

#### 3.2.1. 基于 Windows PC 将 Linux 镜像烧写到 TF 卡的方法  

下载用于烧录 Linux 镜像的软件——balenaEtcher，下载完记得用管理员身份打开，下载地址为：https://www.balena.io/etcher/  

首先准备一张 32GB 或更大容量的 TF 卡（ 推荐使用 64GB 或以上容量的 TF卡） ， TF 卡的传输速度必须为 class10 级或 class10 级以上， 建议使用闪迪等品牌的 TF 卡。  然后把 TF 卡插入读卡器， 再把读卡器插入电脑  .

![image-20240720131655571](C:\Users\ZYS\AppData\Roaming\Typora\typora-user-images\image-20240720131655571.png)

上面的烧录有时会出错，推荐另一个好用的烧录工具，下载完记得用管理员身份打开：
https://ascend-repo.obs.cn-east-2.myhuaweicloud.com/Atlas%20200I%20DK%20A2/DevKit/tools/latest/Ascend-devkit-imager_latest_win-x86_64.exe

![image-20240718200249602](C:\Users\ZYS\AppData\Roaming\Typora\typora-user-images\image-20240718200249602.png)





#### 3.2.2 其他方法烧录镜像方法

烧录方式详见手册用户手册中的《2.5. 烧写 Linux 镜像到 eMMC 中的方法  》、《2.6. 烧写 Linux 镜像到 NVMe SSD 中的方法  》、《2.7. 烧写 Linux 镜像到 SATA SSD 中的方法  》。

### 3.3 开发板启动模式

Orange Pi AI Pro 开发板 支持从 TF 卡、 eMMC 和 SSD（支持 NVMe SSD 和 SATA SSD） 启动。具体从哪个设备启动是由开发板背面的两个拨码（BOOT1 和 BOOT2） 开关来控制的。  BOOT1 和 BOOT2 两个拨码开关都支持左右两种设置状态， 所以总共有 4 种设置状态，开发板目前只使用了其中的三种。 不同的设置状态对应的启动设备如下表所示：  

![image-20240718194014323](C:\Users\ZYS\AppData\Roaming\Typora\typora-user-images\image-20240718194014323.png)

注意， SATA SSD和NVMe SSD的启动方式对应的拨码开关的设置状态是一样的。这两种启动方式是通过M2_TYPE引脚的电平来自动区分的。  另外切换拨码开关后必须重新拔插电源上下电才能让新的启动设备选项生效。 通过开发板的复位按键来复位系统是不会让拨码开关新设置的配置生效的。  

将烧录好镜像的 TF 卡或者 eMMC 模块或者 SSD 插入开发板对应的插槽中。  

开发板有两个 HDMI 接口（ 目前只有 HDMI0 支持显示 Linux 系统的桌面，HDMI1 显示 Linux 系统桌面的功能还需等软件更新） ， 如果想显示 Linux 系统的桌面， 可以将开发板的 HDMI0 接口连接到 HDMI 显示器。  

![image-20240718201059966](C:\Users\ZYS\AppData\Roaming\Typora\typora-user-images\image-20240718201059966.png)、

开发板有 USB 接口， 可以接上 USB 鼠标和键盘， 来控制开发板。  开发板有千兆以太网口， 可以插入网线用来上网。  

然后需要连接一个 20V PD-65W 的 Type C 接口的电源， 电源接口的位置如下图所示：  

![image-20240718201119667](C:\Users\ZYS\AppData\Roaming\Typora\typora-user-images\image-20240718201119667.png)



然后打开电源适配器的开关， 如果一切正常， 等待一段时间后， HDMI 显示器就能看到 Linux 系统的登录界面了。  

![image-20240720133801602](C:\Users\ZYS\AppData\Roaming\Typora\typora-user-images\image-20240720133801602.png)

输入密码即可成功登录，账号HwHiAiUser，密码Mind@123

![image-20240720133936229](C:\Users\ZYS\AppData\Roaming\Typora\typora-user-images\image-20240720133936229.png)

### 3.4 连接测试

#### 3.4.1  串口连接

首先需要安装如下USB转串口驱动：
https://obs-9be7.obs.cn-east-2.myhuaweicloud.com/OrangePi/private/CH343SER.EXE

只需要一根 Micro USB 接口的数据线将开发板连接到电脑的 USB 接口就可以开始使用开发板的调试串口功能了， 无需购买 USB 转 TTL 模块 。

![image-20240718202828596](C:\Users\ZYS\AppData\Roaming\Typora\typora-user-images\image-20240718202828596.png)

#### 3.4.2  SSH连接

除了用串口连接，也可以用ssh连接。将开发板和电脑连接同一wifi，确保两者在统一网段，可以ping通。MobaXterm里的SSH连接功能，填写好IP地址后，默认22端口即可。

连接wifi:

![image-20240720134356235](C:\Users\ZYS\AppData\Roaming\Typora\typora-user-images\image-20240720134356235.png)



查看电脑ip:

![image-20240720134950185](C:\Users\ZYS\AppData\Roaming\Typora\typora-user-images\image-20240720134950185.png)



查看OrangePi板子的IP地址，打开控制面板，输入ifconfig,

![image-20240720161351230](C:\Users\ZYS\AppData\Roaming\Typora\typora-user-images\image-20240720161351230.png)



ping，可以ping通Orange Pi AI Pro 开发板 ,

![image-20240720133146614](C:\Users\ZYS\AppData\Roaming\Typora\typora-user-images\image-20240720133146614.png)

连接SSH：用mobaxter连接开发板，mobaxterm下载地址[MobaXterm free Xserver and tabbed SSH client for Windows (mobatek.net)](https://mobaxterm.mobatek.net/)

![image-20240720133339649](C:\Users\ZYS\AppData\Roaming\Typora\typora-user-images\image-20240720133339649.png)

![image-20240720133428987](C:\Users\ZYS\AppData\Roaming\Typora\typora-user-images\image-20240720133428987.png)

ssh连接成功，可以看到是Ubuntu 22.04.3 LTS版本。

## 四、AI功能体验

### 4.1 测试项目YOLOv5

香橙派自带的conda的base安装的python环境是3.9.2，我们这里就使用这个环境来测试，可以使用下面的命令更换环境

```
conda create -n name python=version
```

使用pip安装requirements.txt中列出的依赖，速度比较慢，建议先下载压缩包，在通过mobaxterm传输到开发板即可。yolov5下载地址https://github.com/ultralytics/yolov5

![image-20240720135846782](C:\Users\ZYS\AppData\Roaming\Typora\typora-user-images\image-20240720135846782.png)





上传到开发板，并解压得到yolov5-master,

![image-20240720140130442](C:\Users\ZYS\AppData\Roaming\Typora\typora-user-images\image-20240720140130442.png)

进入yolo5-master,安装对应库

```
cd yolo5-master
pip3 install -r requirements.txt -i https://pypi.tuna.tsinghua.edu.cn/simple/
```

识别单张图片 ： 这个里面的yolov5m-seg.pt如果不存在，会自动到github上去下载，但是速度极慢，建议是下载好，然后指定对应路径的pt文件.

测试YOLOv5模型的效果，我们将使用预训练模型识别一些图片。可以先下载一些图片，通过mobaxterm将pc端的图片拖拉上传到开发板目录就行，如下：

![image-20240720141101255](C:\Users\ZYS\AppData\Roaming\Typora\typora-user-images\image-20240720141101255.png)



运行以下命令：

```
	python segment/predict.py --weights ~/Documents/yolov5m-seg.pt --data data/images/huawei.jpg
	python segment/predict.py --weights ~/Documents/yolov5m-seg.pt --data data/images/bus.jpg
	python segment/predict.py --weights ~/Documents/yolov5m-seg.pt --data data/images/dog.jpg

```

执行命令后，可以对应目录下找到结果：

![image-20240720141955728](C:\Users\ZYS\AppData\Roaming\Typora\typora-user-images\image-20240720141955728.png)

测试结果：

![image-20240720142145040](C:\Users\ZYS\AppData\Roaming\Typora\typora-user-images\image-20240720142145040.png)

![image-20240720142439065](C:\Users\ZYS\AppData\Roaming\Typora\typora-user-images\image-20240720142439065.png)



![image-20240720142322877](C:\Users\ZYS\AppData\Roaming\Typora\typora-user-images\image-20240720142322877.png)

### 4.2 实时识别视频

 使用yolo对视频进行实时监测，实现将需要识别的视频上传到开发板目录，如下：

![image-20240720142825516](C:\Users\ZYS\AppData\Roaming\Typora\typora-user-images\image-20240720142825516.png)



修改源码detect.py的361行：

```
parser = argparse.ArgumentParser()
    parser.add_argument("--weights", nargs="+", type=str, default=ROOT / "yolov5s.pt", help="model path or triton URL")
    # parser.add_argument("--source", type=str, default=ROOT / "data/images", help="file/dir/URL/glob/screen/0(webcam)")
    parser.add_argument("--source", type=str, default=ROOT / "data/video", help="file/dir/URL/glob/screen/0(webcam)")
    parser.add_argument("--data", type=str, default=ROOT / "data/coco128.yaml", help="(optional) dataset.yaml path")
    parser.add_argument("--imgsz", "--img", "--img-size", nargs="+", type=int, default=[640], help="inference size h,w")
    parser.add_argument("--conf-thres", type=float, default=0.25, help="confidence threshold")
    parser.add_argument("--iou-thres", type=float, default=0.45, help="NMS IoU threshold")
    parser.add_argument("--max-det", type=int, default=1000, help="maximum detections per image")
    parser.add_argument("--device", default="", help="cuda device, i.e. 0 or 0,1,2,3 or cpu")
    parser.add_argument("--view-img", action="store_true", help="show results")
    parser.add_argument("--save-txt", action="store_true", help="save results to *.txt")
    parser.add_argument("--save-csv", action="store_true", help="save results in CSV format")
    parser.add_argument("--save-conf", action="store_true", help="save confidences in --save-txt labels")
    parser.add_argument("--save-crop", action="store_true", help="save cropped prediction boxes")
    parser.add_argument("--nosave", action="store_true", help="do not save images/videos")
    parser.add_argument("--classes", nargs="+", type=int, help="filter by class: --classes 0, or --classes 0 2 3")
    parser.add_argument("--agnostic-nms", action="store_true", help="class-agnostic NMS")
    parser.add_argument("--augment", action="store_true", help="augmented inference")
    parser.add_argument("--visualize", action="store_true", help="visualize features")
    parser.add_argument("--update", action="store_true", help="update all models")
    parser.add_argument("--project", default=ROOT / "runs/detect", help="save results to project/name")
    parser.add_argument("--name", default="exp", help="save results to project/name")
    parser.add_argument("--exist-ok", action="store_true", help="existing project/name ok, do not increment")
    parser.add_argument("--line-thickness", default=3, type=int, help="bounding box thickness (pixels)")
    parser.add_argument("--hide-labels", default=False, action="store_true", help="hide labels")
    parser.add_argument("--hide-conf", default=False, action="store_true", help="hide confidences")
    parser.add_argument("--half", action="store_true", help="use FP16 half-precision inference")
    parser.add_argument("--dnn", action="store_true", help="use OpenCV DNN for ONNX inference")
    parser.add_argument("--vid-stride", type=int, default=1, help="video frame-rate stride")
    opt = parser.parse_args()
    opt.imgsz *= 2 if len(opt.imgsz) == 1 else 1  # expand
    print_args(vars(opt))
    return opt
```

执行下面的命令：等待完成

```
python segment/predict.py --weights ~/Documents/yolov5m-seg.pt --source ~/Documents/video1.mp4
python segment/predict.py --weights ~/Documents/yolov5m-seg.pt --source ~/Documents/video2.mp4
```

找到对应的结果：

![image-20240720143117925](C:\Users\ZYS\AppData\Roaming\Typora\typora-user-images\image-20240720143117925.png)

测试效果如下：

<iframe src="//player.bilibili.com/player.html?isOutside=true&aid=112859241515312&bvid=BV1QZv7eSENe&cid=500001629566821&p=1" scrolling="no" border="0" frameborder="no" framespacing="0" allowfullscreen="true"></iframe>

### 4.3  案例测试

1、首先登录 Linux 系统桌面， 然后打开终端， 再切换到保存 MindSpore AI 应用样例的目录下，

2、在当前目录下有 8 个文件夹和 1 个 shell 文件， 分别对应 8 个 AI 应用样例和Jupyter Lab 启动脚本 start_notebook.sh ，

3、然后执行 start_notebook.sh 脚本启动 Jupyter Lab。 ，

4、在执行该脚本后， 终端会出现如下打印信息， 在打印信息中会有登录 Jupyter Lab 的网址链接  ，

5、然后打开火狐浏览器  ，在浏览器中输入上面看到的网址链接， 就可以登录 Jupyter Lab 软件  

```
依次运行如下命令：
cd samples
ls
./start_notebook.sh
```

![image-20240720160059698](C:\Users\ZYS\AppData\Roaming\Typora\typora-user-images\image-20240720160059698.png)



![image-20240720160125280](C:\Users\ZYS\AppData\Roaming\Typora\typora-user-images\image-20240720160125280.png)





案例测试:

1、首先在 Jupyter Lab 界面双击下图所示的 03-ResNet50， 进入到该样例的目录中  

2、在该目录下有运行该示例的所有资源， 其中 main_resnet50.ipynb 是在 Jupyter Lab 中运行该样例的文件， 双击打开 main_resnet50.ipynb， 在右侧窗口中会显示此文件中的内容， 如下图所示  

3、运行即可

![image-20240720160207611](C:\Users\ZYS\AppData\Roaming\Typora\typora-user-images\image-20240720160207611.png)

![image-20240720160226890](C:\Users\ZYS\AppData\Roaming\Typora\typora-user-images\image-20240720160226890.png)

其他案例可查看OrangePi AIPro 用户手册  。

### 4.4  OrangePi AIPro 高性能测试与体验

#### 4.4.1单线程cpu测试

我们将运行单线程的 sysbench CPU 测试，评估香橙派 Kunpeng Pro 的整数计算性能。使用以下命令开始测试

```
sysbench cpu --cpu-max-prime=20000 run
```

![image-20240720152619320](C:\Users\ZYS\AppData\Roaming\Typora\typora-user-images\image-20240720152619320.png)



#### 4.4.2 多线程cpu测试

运行多线程的 sysbench CPU 测试，评估多核处理能力。使用以下命令进行测试：

```
sysbench cpu --threads=4 --cpu-max-prime=20000 run
```

![image-20240720152736813](C:\Users\ZYS\AppData\Roaming\Typora\typora-user-images\image-20240720152736813.png)

#### 4.4.3 内存性能测试

4G 内存压力测试：

```
stress-ng --vm 2 --vm-bytes 4G --vm-method all --verify -t 60s
```

5G 内存压力测试：

```
stress-ng --vm 2 --vm-bytes 5G --vm-method all --verify -t 60s
```

6G 内存压力测试：

```
stress-ng --vm 2 --vm-bytes 6G --vm-method all --verify -t 60s
```

![image-20240720153516830](C:\Users\ZYS\AppData\Roaming\Typora\typora-user-images\image-20240720153516830.png)



| 测试项目             | 总执行时间（秒） | 每秒事件数 | 测试结果   |
| -------------------- | ---------------- | ---------- | ---------- |
| 单线程 CPU 测试      | 10.0011          | 816.62     | 正常       |
| 多线程 CPU 测试      | 10.0012          | 2434.15    | 正常       |
| 高负载内存测试（4G） | 65.50            |            | successful |
| 高负载内存测试（5G） | 60.06            |            | successful |
| 高负载内存测试（6G） | 61.51            |            | successful |

## 使用感受

香橙派 AIpro 是一款功能强大且易于使用的 AI 开发板。其性能和功能设计不仅适合初学者学习和探索 AI 技术，也满足专业开发者在边缘计算和 AI 应用部署方面的需求。以下是总结的主要优点和特点：

### 性能与配置
1. **高性能 AI 处理器**：配备高达 8TOPS 的 AI 处理能力，适合人脸识别、物体识别、分类和追踪等场景。
2. **大内存支持**：提供 8GB 或 16GB LPDDR4X 内存选项，能够高效处理复杂的 AI 算法和数据分析。
3. **丰富的存储选项**：支持 TF 卡、eMMC 和 M.2 2280 SSD（NVMe 和 SATA 协议），提供灵活的存储解决方案。
4. **良好的散热性能**：自带静音风扇，智能控制转速，确保高性能计算时的散热效果。

### 接口与扩展性
1. **丰富的外设接口**：包括两个 HDMI 输出、GPIO 接口、Type-C 电源接口、千兆网口、USB 接口等，满足多种开发需求。
2. **电池管理与快充支持**：支持电池供电及快充功能，为便携和移动应用提供便利。
3. **高集成度设计**：集成固态接口、串口转 USB、电池管理等功能，减少外接模块的需求。

### 操作系统与开发体验
1. **多系统支持**：兼容 Ubuntu、openEuler 等操作系统，方便用户根据需求进行开发和部署。
2. **开箱即用**：系统烧录后预装 SSH 和 AI 框架，减少重复性配置工作，提升开发效率。
3. **优质的用户手册**：详细的官方资料和用户手册，使得上手非常简单，适合初学者和专业开发者。

### 实际应用与体验
1. **公共卫生管理**：在健康监测解决方案中，利用香橙派 AIpro 实现高效的人脸识别与非接触式体温测量，提升疾病早期预警和控制能力。
2. **高负载下稳定运行**：经过长时间高负载运行，香橙派 AIpro 依然保持稳定，且风扇噪音低，系统静音效果佳。
3. **创新与国产化推进**：集成了多款国产芯片，为 AI 边缘计算的发展和国产化进程作出贡献。

### 结论
香橙派 AIpro 开发板凭借其强大的 AI 处理能力、丰富的接口和存储选项、优良的散热性能以及良好的用户体验，成为一款非常优秀的 AI 开发板。在各种应用场景中，如边缘计算、物联网、多媒体处理和教育科研等方面都表现出色。如果你正在寻找一款功能强大的 AI 开发板，香橙派 AIpro 无疑是一个不错的选择。