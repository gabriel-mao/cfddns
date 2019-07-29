# koolshare-cfddns

## 简介 

> 这是一个适用于梅林固件(koolshare) 的 Cloudflare DDNS 插件，开发参考了 [gdddns](https://github.com/mritd/koolshare-gdddns) 

## 插件使用

- DNS托管在Cloudflare
- 在 Cloudflare管理面板获取API KEY，Zone ID。
- 在软件中心使用离线安装本插件，填入对应用户注册Email，API KEY ，Zone ID，并设置解析域名等相关参数即可

### 本插件目录结构规范

本插件目录结构如下

``` sh
├── LICENSE                        授权声明
├── README.md                      说明文档
├── build.sh                       编译脚本，一般为打包脚本，感觉也可以写点从源码编译的动作
├── cfddns                         插件主目录
│   ├── install.sh                 安装脚本
│   ├── res                        资源目录
│   │   └── icon-cfddns.png        插件图标
│   ├── scripts                    插件辅助执行脚本
│   │   ├── cfddns_config.sh       插件配置脚本
│   │   ├── cfddns_update.sh       本插件的主要执行脚本
│   │   └── uninstall_cfddns.sh    卸载脚本
│   └── webs                       页面资源文件
│       └── Module_cfddns.asp      插件设置页面
└── cfddns.tar.gz                  插件打包文件
```

**约定优于配置: 默认的安装卸载脚本文件名(install.sh、uninstall_xxxx.sh) 请不要乱更改，否则可能不会执行；尤其是插件的文件名约定，
最好参考已有插件命名，不要乱造；否则这些脚本可能不会被执行，点击卸载时也只是做了 DBUS 反注册信息而已，实际文件并未被删除**


### 插件中心目录结构规

**插件在打包成 tar.gz 文件后，安装时将插件各个目录中的内容释放到 `/koolshare` 目录，以下是 `/koolshare` 目录结构**


``` sh
koolshare
├── bin            二进制文件
├── configs        配置目录
├── init.d         初始化脚本
├── perp           预处理脚本
├── res            资源文件目录
├── scripts        脚本目录
└── webs           页面资源文件
```

**从上面 koolshare 目录结构可以看出，实际上插件内的目录结构应该是与其一致的，一般是能少不能多，因为在安装后插件内各个目录中的文件
都会被释放到 `/koolshare` 目录下的相应目录中(安装脚本控制)，除非特殊情情况，比如 shadowsocks 文件很多所以单独创建了文件件(在 `/koolshare`
下差创建了一个 ss 的目录)；**

### 插件更新推送机制
- 插件git地址需要先被 [modules.json](https://github.com/koolshare/koolshare.github.io/blob/acelan_softcenter_ui/softcenter/modules.json) 收录；
- 插件作者提交插件相关更新后，更改config.json.js内的版本号；
- 插件作者运行 python build.py，会自动生成插件安装包，插件备份
- koolshare插件中心服务器会每隔5分钟检查一次该项目config.json.js内的版本号，如果有更新，则会拉取一份到中转服务
- 同时会将config.json.js的内容插入[app.json.js](https://koolshare.ngrok.wang/softcenter/app.json.js)
- 用户访问软件中心请求[app.json.js](https://koolshare.ngrok.wang/softcenter/app.json.js)，即可知道插件的状态


















