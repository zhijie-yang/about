# 为WSL命令行添加V2Ray代理

向`~/.bashrc`中添加如下别名

```bash
alias proxy_v2ray="export HTTPS_PROXY=http://`cat /etc/resolv.conf|grep nameserver|awk '{print $2}'`:1082; export HTTP_PROXY=http://`cat /etc/resolv.conf|grep nameserver|awk '{print $2}'`:1082"
alias proxy_off="unset HTTPS_PROXY; unset HTTP_PROXY"
```

根据实际情况修改命令中的端口号。