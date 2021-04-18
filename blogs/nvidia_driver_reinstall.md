# 重新安装nVidia显卡驱动

1. 前往官网下载.run格式的驱动
2. 为.run格式文件加上可执行权限`chmod +x NVIDIA-Linux-x86_64*.run `
3. 使用Ctrl+Alt+F3切换到非图形终端
4. `sudo systemctl isolate multi-user.target`
5. `sudo modprobe -r nvidia_drm`
6. `sudo modprobe -r nvidia_modeset`
7. `sudo ./NVIDIA-Linux-x86_64*.run --no-opengl-files`
8. `sudo systemctl start graphical.target`