## 将安卓手机投屏到MAC电脑

本文使用的是***scrcpy***
> 这是一个免费的开源软件，支持Linux，Windows，macOS系统，可以实现安卓手机投屏到电脑上的同时使用键鼠操作手机

<br/>

## 安装步骤

#### 1. 进入[scrcpy](https://github.com/Genymobile/scrcpy)的github仓库

#### 2. 在README中找到Get the app，点击[macOS](https://github.com/Genymobile/scrcpy/blob/master/doc/macos.md)跳转到安装界面

<img width="480" height="100" alt="image" src="https://github.com/user-attachments/assets/37809fa8-6269-431c-944e-8a881b8739c4" />
    
#### 3. 推荐使用Homebrew下载，它可以自动配置好相关内容

在终端执行这两条命令，安装scrcpy和安卓平台工具包<br/><br/>

<img width="600" height="175" alt="image" src="https://github.com/user-attachments/assets/59a32daf-3266-4f11-bc99-6d757455aa74" />

> 最后可以在终端输入 adb 检测是否安装完成

<br/>

## 使用教程

### 打开USB调试
`不论有线使用还是无线使用都需要执行`

#### 1. 点开手机设置-关于本机-版本信息
> android版本 ❌\
> 版本信息 ✅

#### 2. 连续多次点击“版本号”，打开开发者模式

#### 3. 在开发者选项中打开“USB调试”<br/><br/>

### 有线使用
#### 1. 连接手机与电脑

> 1. 数据线 ✅ 全连接线 ✅\
>    充电线 ❌ 充电线无法传输数据
> 2. 如果手机弹出相关允许选项，选择允许；\
>    如果不小心选错了，在开发者选项中关闭并重新打开“USB调试”,再重新插拔数据线
> 3. 如果有弹窗询问数据传输类型，选择文件传输或相关选项

#### 2. 启动scrcpy

在终端输入以下命令并按回车

```bash
scrcpy
```
<br/>

### 无线使用
`手机和电脑需要连接同一个网络`

#### 1. 连接手机与电脑
> 同有线连接第一步

#### 2. 在终端中执行命令，查看连接到的设备
```bash
adb devices
```

可以看到类似返回结果：
```bash
List of devices attached
K7SKJ7J799FQ599X	device 
```

#### 3. 运行以下命令，让手机在 5555 端口上监听 Wi-Fi 连接
```
adb tcpip 5555
```

可以看到类似返回结果：
```
restarting in TCP mode port: 5555
```
> 完成后可以拔掉数据线了

#### 4. 查看手机IP地址
设置 - wifi - 点开连接的Wi-Fi - 记下IPv4地址

#### 5.在终端运行命令，将 你的ip地址 改为第四步看到的IPv4地址

```bash
adb connect 你的ip地址:5555  # 例如 adb connect 192.168.1.10:5555
```

可以看到类似提示：
```bash
connected to 192.168.1.10:5555
```

`注意：如果之后手机没有关闭USB调试，并且手机的IP地址没有变化，可以直接从第五步开始，否则得重新开始`<br/><br/>

#### 6. 在终端运行scrcpy
```
scrcpy
```

如果觉得卡顿可以选一条执行：
```
# 降低比特率
# scrcpy默认是 8 Mbps
  scrcpy -b 4M  
  scrcpy -b 2M # 画质会更加模糊

# 降低分辨率
  scrcpy -m 1080 # 限制在1080p级别
  scrcpy -m 720  # 限制在720p级别

# 降低帧率
  scrcpy --max-fps 30 # 将帧率上限限制在30帧/秒

# 组合使用
  scrcpy -b 4M -m 1080
  scrcpy -b 2M -m 1080 --max-fps 30

```
