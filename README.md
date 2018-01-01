![计算](http://upload-images.jianshu.io/upload_images/576195-fd957e0c51330db5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



调试时，修改 debug 为 True，真实运行时，设置为 False。停顿时间设置为 1s，如果电脑运算速度太快，保险起见可以设置为 2s。

第一版使用垂直投影图的方案进行目标查找，结果不是太准备；

第二版改为直接去除背景，以达到二值化。

第二版去除背影的方式，太慢了，第三版不再去除背景，直接找极点，非常迅速！

目前以 距离 x 1.5 作为长按时长，基本能跳到目标中心位置。

原理：
0. adb 截图
1. 找到小人臀部坐标（hsv 色相紫黑色）
2. 将背景（取高度在1/3处点的色相为基准）替换为黑色，其余替换为白色，进行二值化处理。
3. 找到下一桥墩的顶点坐标
4. 找到下一桥墩的极左/极右点坐标
5. 计算出下一桥墩的中心点坐标
6. 从小人臀部到下一桥墩中心点计算出跳远距离
7. 将距离换算为长按时长
8. 使用 adb 跳

视频：

http://v.youku.com/v_show/id_XMzI3NjY5NjI5Mg==.html?spm=a2h3j.8428770.3416059.1


## 开发环境搭建


### 系统环境

笔者环境：

    $ uname -a
    Darwin rmbp-finn.lan 17.3.0 Darwin Kernel Version 17.3.0: Thu Nov  9 18:09:22 PST 2017; root:xnu-4570.31.3~1/RELEASE_X86_64 x86_64

    $ python --version
    Python 2.7.10

### 安装 Python 2.7

略。

### (可选安装) virtualenv, virtualenvwrapper

略。

### 安装 adb

略。

### 工程搭建


先 fork 一份到自己账户。然后：

    $ mkvirtualenv wechat_micro_jump_game_hero
    $ cdvitualenv
    $ git clone ...
    $ cd wechat_micro_jump_game_hero
    $ echo `pwd` > ../.project
    $ pip install pipenv
    $ pipenv install

手机连上电脑，打开跳一跳小游戏，并点击开始，之后：

    $ python main.py
