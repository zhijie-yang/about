# 为WSL启用图形界面

## Windows端设置

在Windows上安装VcXsrv, 使用配置文件wsl.xlaunch (display_numer为1):

```xml
<?xml version="1.0" encoding="UTF-8"?>
<XLaunch WindowMode="MultiWindow" ClientMode="NoClient" LocalClient="False" Display="1" LocalProgram="xcalc" RemoteProgram="xterm" RemotePassword="" PrivateKey="" RemoteHost="" RemoteUser="" XDMCPHost="" XDMCPBroadcast="False" XDMCPIndirect="False" Clipboard="True" ClipboardPrimary="True" ExtraParams="" Wgl="False" DisableAC="True" XDMCPTerminate="False"/>

```

若使用XLaunch图形界面配置，首先Multiple windows, 并且指定Display number, 记为\<display_number\>. 

下一步，选择Start no client，

下一步，取消勾选Native opengl，勾选Disable access control

下一步，保存当前配置文件，之后可以直接双击配置文件启动XServer

## WSL端设置(Ubuntu)

向`~/.bashrc`中添加

```bash
export DISPLAY="`cat /etc/resolv.conf|grep nameserver|awk '{print $2}'`:<display_number>.0"
```

例：当\<display_number\>设置为1时则

```bash
export DISPLAY="`cat /etc/resolv.conf|grep nameserver|awk '{print $2}'`:1.0"
```

对于某些使用Qt的程序可能需要手动安装Qt5、PyQt等包才可正常运行。