# Ubuntu下安装TIM等软件

## 1. 安装wine环境

1. 参考https://github.com/wszqkzqk/deepin-wine-ubuntu 中的本地安装方法，clone仓库后执行`./install.sh`.

2. 从https://packages.deepin.com/deepin/pool/non-free/d/ 中获取deepin.com.qq.office的deb包，下载以后通过dpkg安装.

## 2. 安装字体

deb包中可能并不带有中文字体，因此需要将字体安装到`~/.deepinwine/Deepin-TIM/driver_c/windows/Fronts`中。通常安装`simhei.ttf`和`simsun.ttc`就够了。

## 3. 更新exe程序

因为TIM的程序在不断升级，deepin官方的包已经无法正常登陆（提示版本过低），因此需要手动更新，以TIM为例 (ref: https://blog.csdn.net/Hesye/article/details/113430274).

   ```bash
   mkdir /tmp/tim
   cd /tmp/tim
   wget wget https://dldir1.qq.com/qqfile/qq/PCTIM/TIM3.3.5/TIM3.3.5.22018.exe
   env WINEPREFIX=~/.deepinwine/Deepin-TIM deepin-wine TIM3.3.5.22018.exe
   ```

   然后像在Windows一样完成安装即可。

## 4. 安装插件使用状态栏图标

```bash
sudo apt-get install gnome-shell-extension-top-icons-plus gnome-tweaks
```



## 可能遇到的问题

若通过.desktop图标运行无法正常启动，可以使用`/opt/deepinwine/apps/Deepin-TIM/run.sh`来运行并查看报错信息。

### GLX相关错误

```
X Error of failed request:  GLXBadContext
  Major opcode of failed request:  155 (GLX)
  Minor opcode of failed request:  6 (X_GLXIsDirect)
  Serial number of failed request:  32
  Current serial number in output stream:  31
```

或

```
X Error of failed request:  BadValue (integer parameter out of range for operation)
  Major opcode of failed request:  154 (GLX)
  Minor opcode of failed request:  24 (X_GLXCreateNewContext)
  Value in failed request:  0x0
  Serial number of failed request:  29
  Current serial number in output stream:  30
```



下载.run格式的驱动程序，重新安装nvidia显卡驱动，并使用参数`--no-opengl-files`.

### 图片和头像无法显示

禁用ipv6，但对日后脱离ipv4使用是否会有影响尚不明确。

```bash
sudo sysctl -w net.ipv6.conf.all.disable_ipv6=1
sudo sysctl -w net.ipv6.conf.default.disable_ipv6=1
sudo sysctl -w net.ipv6.conf.lo.disable_ipv6=1
```

