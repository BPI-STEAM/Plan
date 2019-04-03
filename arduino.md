# Arduino

## Arduino IDE 
<img src="/Image/Arduino-logo.jpg" width="150px" />

### 安装Arduino IDE 

下载Arduino IDE：
[Arduino.cc官方网站下载地址](https://www.arduino.cc/en/main/software)
[Arduino中文社区下载地址](https://www.arduino.cn/thread-5838-1-1.html)

### Arduino IDE连接板子以及导入开发扩展包
#### 1. 有线连接板子

- 将板子通过 MicroUSB 线连接到你的电脑里，以下以 Windows10 为例。

 ![连接板子](./Image/home08.png)

#### 2. 查看驱动

- 进入 **设备管理器** 确认串口驱动（Serial）是否安装，进入方法如下。
  - （右键）此电脑 -> 属性 -> **设备管理器**
  - 开始菜单 -> （输入）**设备管理器**
  - 控制面板 -> （搜索）**设备管理器**

 ![查看驱动](./Image/home07.png)

- 可以看到 设备显示 **USB2.0-Serial** ，说明**未安装驱动**，若此前已安装驱动，可以跳至步骤 5 。


#### 3. 安装驱动

- [点此获取 Serial CH341](http://www.wch.cn/downloads/file/5.html) 驱动，并按如下说明操作安装驱动

- 打开下载的 **CH341SER.ZIP** 压缩包，进入 **CH341SER** 文件夹，打开 **SETUP.EXE**，即可看到如下图。

 ![安装驱动](./Image/home06.png)

- 点击 **INSTALL** （安装），等待片刻即可完成安装。


#### 4. 确认串口

- 核对板子是否连接成功

 ![连接成功](./Image/home01.png)

- 可以看到原来的 **USB2.0-Serial** 消失了，取而代之的是 **USB-SERIAL CH340(COM3)**，这意味着你已经成功安装驱动，并且得到板子串口名称为（**COM3**），你可以通过各种串口工具来查看串口名（COM3）的板子传出的信息。

#### 5. 开发扩展包

- [arduino-esp32 开发工具包](https://github.com/espressif/arduino-esp32/archive/master.zip)，点击前边连接获取开发工具包
> - 源自乐鑫(espressif) github 开源项目 [arduino-esp32](https://github.com/espressif/arduino-esp32),后续开发工具包更新推荐使用[GitHub-DeskTop](https://desktop.github.com) 工具随时同步更新套件。


#### 6-1. Windows安装说明

1. 下载并安装最新版本的Arduino IDE， ```Windows Installer``` from [arduino.cc](https://www.arduino.cc/en/Main/Software)
2. 从 [espressif/arduino-esp32](https://github.com/espressif/arduino-esp32)开源项目下载Arduino开发扩展包

    ![Step 1](./Image/win-1.png)

3. 解压Arduino开发扩展包  ```[ARDUINO_SKETCHBOOK_DIR]/hardware/espressif/esp32```
    
    - ARDUINO_SKETCHBOOK_DIR: 一般情况下是 ```C:/Users/[YOUR_USER_NAME]/Documents/Arduino``` 并列在Arduino首选项中的“Sketchbook位置”下方。
        
        ![Step 2](./Image/win-2.png)

    - 依次打开目录 ```[ARDUINO_SKETCHBOOK_DIR]/hardware/espressif/esp32/tools``` 并且双击运行 ```get.exe```
        
        ![Step 3](./Image/win-3.png)

    - 当 ```get.exe``` 运行结束, 您应该在目录中看到以下文件

        ![Step 4](./Image/win-4.png)

4. 插入BPI：BIT板并等待驱动程序安装（或手动安装） [Serial CH341](http://www.wch.cn/downloads/file/5.html) 
5. 运行 `Arduino IDE`
6. 选择您的版型(BPI-BIT) ```Tools > Board``` menu

    ![Step 5](./Image/win-5.png)

7. 选择BIT板所连接的COM端口，例如`COMx`
8. 编译并上传您的工程代码 (BIT板设计有自动烧录电路，直接点击上传即可)

    ![Arduino IDE Example](./Image/arduino-ide.png)

#### 6-2. Debian / Ubuntu OS安装说明

- 从 [arduino.cc](https://www.arduino.cc/en/Main/Software)网站获取并安装最新版本的 Arduino IDE
- 打开终端并执行以下命令 (copy-> paste并点击回车):

  ```bash
  sudo usermod -a -G dialout $USER && \
  sudo apt-get install git && \
  wget https://bootstrap.pypa.io/get-pip.py && \
  sudo python get-pip.py && \
  sudo pip install pyserial && \
  mkdir -p ~/Arduino/hardware/espressif && \
  cd ~/Arduino/hardware/espressif && \
  git clone https://github.com/espressif/arduino-esp32.git esp32 && \
  cd esp32 && \
  git submodule update --init --recursive && \
  cd tools && \
  python2 get.py
  ```
- 重新运行 Arduino IDE

- 如果您已经安装arduino至`~/`目录，请执行以下代码, 如果没有, 那么请从 `mkdir -p ~/Arduino/hardware`开始:

  ```bash
  cd ~/Arduino/hardware
  mkdir -p espressif && \
  cd espressif && \
  git clone https://github.com/espressif/arduino-esp32.git esp32 && \
  cd esp32 && \
  git submodule update --init --recursive && \
  cd tools && \
  python2 get.py
  ```

#### 6-3. Mac OS安装说明

- 从 [arduino.cc](https://www.arduino.cc/en/Main/Software)网站获取并安装最新版本的 Arduino IDE
- 打开终端并执行以下命令 (copy-> paste并点击回车):

  ```bash
  mkdir -p ~/Documents/Arduino/hardware/espressif && \
  cd ~/Documents/Arduino/hardware/espressif && \
  git clone https://github.com/espressif/arduino-esp32.git esp32 && \
  cd esp32 && \
  git submodule update --init --recursive && \
  cd tools && \
  python get.py 
  ```
  其中 `~/Documents/Arduino` 目录与"Arduino" > "首选项" > "Sketchbook location" (在软件启动后)应该保持一致。 如果有需要的话，或许需要更改上面的命令！
  
- 如果您收到以下错误。 使用xcode-select --install安装命令行开发工具并再次尝试上面的命令：

  ```xcrun: error: invalid active developer path (/Library/Developer/CommandLineTools), missing xcrun at: /Library/Developer/CommandLineTools/usr/bin/xcrun```
  
  ```xcode-select --install```
  
- 在运行 `python get.py`的时候，收到错误提示: `IOError: [Errno socket error] [SSL: TLSV1_ALERT_PROTOCOL_VERSION] tlsv1 alert protocol version (_ssl.c:590)` ，您可以尝试使用 `python3` 代替 `python` 

- 重启 Arduino IDE


### Arduino IDE扩展库安装
以下方法以Windows 10系统为例，其他系统的安装方法于此类似。

#### 0. Arduino IDE 安装库方法1(通过Arduino IDE`管理库`工具)

依次点开`项目`>`加载库`>`管理库`(默认快捷键`Ctrl+Shift+I`)

![step a-1](./Image/Install_Lib_1.png)

打开`库管理器`之后，等待下方的进度条加载完成，然后可以在上方的过滤框添加过滤关键字，点选需要安装的库后，在条目右下角点击安装即可。

![step a-2](./Image/Install_Lib_2.png)

## 1. Arduino IDE 安装库方法2(通过Arduino IDE安装ZIP库)

依次点开`项目`>`加载库`>`添加.ZIP库`

![step b-1](./Image/Install_Lib_3.png)

选择已经下载好的库文件的ZIP压缩包，然后点击打开。

![step b-2](./Image/Install_Lib_4.png)

#### 2. Arduino IDE 安装库方法3(直接复制库文件夹至`libraries`目录)

`libraries`目录存放地址一般为：`C:\Users\yelv1\Documents\Arduino`，可以在Arduino IDE里查看，依次打开`文件`>`首选项`

![step c-1](./Image/Install_Lib_5.png)

在首选项对话框内

![step c-2](./Image/Install_Lib_6.png)

将整个库的github上托管的仓库目录复制进去即可

![step c-3](./Image/Install_Lib_7.png)


#### PlatformIO IDE
<img src="/Image/PlatformIO-logo.png" width="150px" />

**PlatformIO is an open source ecosystem for IoT development**
*Cross-platform IDE and unified debugger. Remote unit testing and firmware updates*
### 安装PlatformIO

[Install PlatformIO IDE](https://platformio.org/platformio-ide) 你需要配合Visual Studio Code(推荐，或者使用Atom也可以)来使用它。

### 硬件连接：
#### 1. 有线连接板子

- 将板子通过 MicroUSB 线连接到你的电脑里，以下以 Windows10 为例。

 ![连接板子](./Image/home08.png)

#### 2. 查看驱动

- 进入 **设备管理器** 确认串口驱动（Serial）是否安装，进入方法如下。
  - （右键）此电脑 -> 属性 -> **设备管理器**
  - 开始菜单 -> （输入）**设备管理器**
  - 控制面板 -> （搜索）**设备管理器**

 ![查看驱动](./Image/home07.png)

- 可以看到 设备显示 **USB2.0-Serial** ，说明**未安装驱动**，若此前已安装驱动，可以跳至步骤 5 。


#### 3. 安装驱动

- [点此获取 Serial CH341](http://www.wch.cn/downloads/file/5.html) 驱动，并按如下说明操作安装驱动

- 打开下载的 **CH341SER.ZIP** 压缩包，进入 **CH341SER** 文件夹，打开 **SETUP.EXE**，即可看到如下图。

 ![安装驱动](./Image/home06.png)

- 点击 **INSTALL** （安装），等待片刻即可完成安装。


#### 4. 确认串口

- 核对板子是否连接成功

 ![连接成功](./Image/home01.png)

- 可以看到原来的 **USB2.0-Serial** 消失了，取而代之的是 **USB-SERIAL CH340(COM3)**，这意味着你已经成功安装驱动，并且得到板子串口名称为（**COM3**），你可以通过各种串口工具来查看串口名（COM3）的板子传出的信息。


### 添加Espressif 32开发扩展包到PlatformIO IDE:

- Open PlatformIO(PIO) Home Page:
    1. `Platforms`>`Embedded`>`ESP32`
    2. Click `Espressif 32`
    3. Click `Install`
    4. Waiting...

![Step 1](/Image/pio-15.png)

![Step 2](/Image/pio-16.png)

#### PlatformIO中为BPI-Bit新建一个工程:

![Step 3](/Image/pio-17.png)

1. Click `Home` window.
2. Click `New Project` create a new project.

![Step 4](/Image/pio-18.png)

1. `Name`是工程名称
2. `Board`栏选择`BPI-Bit(BPI Tech)`
3. `Framework`选择`Arduino`
4. 你可以自定义选择工程存放的位置(这不是必须的)
5. 点击`Finish`完成创建

#### PlatformIO安装一个扩展库

![step 1](/Image/Install_Lib_8.png)

打开PlatformIO IDE的`Home`页面，然后在左侧边栏的`Libraries`后，在搜索栏搜索需要安装的库的名称

![step 2](/Image/Install_Lib_9.png)

根据搜索的结果选择自己需要的库，然后点击库名称，进入到库的详细信息页面后，点击`Install`即可

![step 3](/Image/Install_Lib_10.png)