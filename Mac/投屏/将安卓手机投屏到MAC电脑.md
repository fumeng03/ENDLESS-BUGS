## 将安卓手机投屏到MAC电脑

我使用的是scrcpy这个工具，它是一个免费的开源软件，支持Linux，Win，macOS系统，可以实现安卓手机投屏到电脑上并用键鼠操作手机

### 安装步骤

1) 点开[scrcpy的github网址](https://github.com/Genymobile/scrcpy)

2) 在README中找到Get the app，点击macOS跳转到Install界面

><img width="480" height="100" alt="image" src="https://github.com/user-attachments/assets/37809fa8-6269-431c-944e-8a881b8739c4" />

3) 推荐用Homebrew下载，它可以自动配置好相关内容

>在终端运行这两条命令，安装scrcpy和安卓平台工具包
>
><img width="600" height="175" alt="image" src="https://github.com/user-attachments/assets/59a32daf-3266-4f11-bc99-6d757455aa74" />
>
>`最后可以在终端输入 adb 检测是否安装完成`

### 使用教程

#### 1. 打开USB调试
`不论有线使用还是无线使用都需要执行`

1）点开手机设置-关于本机-版本信息\
` 注意：版本信息✅ android版本❌ `

2）连续多次点击“版本号”，打开开发者模式

3）在开发者选项中打开“USB调试”

#### 2. 有线使用
1）将数据线连接手机与电脑\
` 注意：1.数据线 ✅ 全连接线 ✅ 充电线 ❌ 充电线无法传输数据`\
`      2.如果手机弹出相关“允许...？”，选择允许；如果不小心选错了，在开发者选项中关闭并重新打开“USB调试”并重新插拔数据线`\
`      3.如果跳出弹窗询问数据传输类型，选择文件传输或相关选项`

2）启动scrcpy

在终端输入以下命令并按回车

```
scrcpy
```

#### 3. 无线使用
`必须保证手机和电脑连接同一个wifi ！`

1）同有线使用第一步

2）在终端中执行命令，可以看到类似返回

```
  adb devices
```
\
<img width="240" height="30" alt="image" src="https://github.com/user-attachments/assets/cf925111-6687-4140-bc21-f403e50b6c80" />

\
3）运行以下命令，让手机在 5555 端口上监听 Wi-Fi 连接

```
adb tcpip 5555
```


```
# 看到如下提示后，就可以拔掉USB数据线了

  restarting in TCP mode port: 5555
```
\
4）查看手机IP地址(手机要和电脑连同一个Wi-Fi！)

```
# 设置 - wifi - 点开连接的Wi-Fi - 记下IPv4地址
```
\
5）在终端运行命令，连接电脑和手机

```
  adb connect 你的ip地址:5555

# 例如 adb connect 192.168.1.10:5555
```
\
可以看到如下提示
```
  connected to 你的ip地址:5555

# 例如 connected to 192.168.1.10:5555

```

```
# 此时在终端输入 adb devices 可以看到自己设备

# 例如 List of devices attached
      192.168.1.10:5555	device
```

`注意：如果之后手机没有关闭USB调试，并且手机的IP地址没有变化，可以直接从第五步开始，否则得重新开始`

6）在终端运行scrcpy
```
  scrcpy
```
```
# 如果觉得卡顿可以尝试

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



### 其他
>在README界面中有更加具体的各种操作指南（点击Translations）
><img width="444" height="175" alt="image" src="https://github.com/user-attachments/assets/3af8e86b-2348-4862-80b8-c5abfcbfaa4f" />\
>
>``但是只有README和FAQ界面有翻译，其他内容依然还是英文``
