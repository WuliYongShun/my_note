# ubuntu使用root登录
1, 打开配置文件
`sudo gedit /usr/share/lightdm/lightdm.conf.d/50-ubuntu.conf`

2, 修改配置文件
在此文件中追加
`greeter-show-manual-login=true`
保存
3, 为root设置密码
`sudo passwd root`

4, 将非root账户目录中的.profile复制到/root/：
例如：`cp /home/username/.profile /root/`
(如果不做此步骤， 启动时会报错：`读取/root/.profile时发现错误：mesg:ttyname failed:对设备不适当的ioctl操作 作为结果，会话不会被正确配置`)

5, 重启即可

## Ubuntu1804之后的特殊问题
在Ubuntu1804后, 使用了GDM3人机交互登录界面, 上述方法需要切换到lightdm方法才能够生效
安装lightdm:
`apt install lightdm`
在安装过程中的提示中, 选择使用lightdm. 再按照上述步骤操作即可

