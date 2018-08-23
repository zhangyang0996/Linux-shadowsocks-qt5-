

## 一、安装 shadowsocks-qt5

前提你要有这个SS服务端，咱们现在搭建的是Ubuntu客户端

服务端可以使用第三方的，速度比较快1080p视频没问题：http://91tianlu.win/aff.php?aff=1993

shadowsocks-qt5 需要通过PPA源安装，仅支持Ubuntu 14.04或更高版本。
 1、设置 PPA 源并安装 shadowsocks-qt5

```shell
$ sudo add-apt-repository ppa:hzwhuang/ss-qt5
$ sudo apt-get update
$ sudo apt-get install shadowsocks-qt5
```

2、安装过程遇到 libappindicator1 依赖问题（dependency problems），而 libappindicator1 又遇到 libindicator7 依赖的解决办法。一并安装 libappindicator1 libindicator7 依赖，再重新安装 shadowsocks-qt5。

```shell
$ sudo apt-get -f install libappindicator1 libindicator7
```

3、完成后就可以打开 shadowsocks-qt5 啦



## 二、设置系统全局代理

window和mac下的ss都有PAC功能，但linux下的GUI程序ss-qt5却没有pac功能，作者说没有时间做，当然也没有人去帮忙更新。
 所以使用ss-qt5时，使用系统的代理功能（设置-->网络-->代理设置），然后在浏览器用proxy插件来设置规则。
 使用系统的全局代理功能（即选择手动）在使用国外的代理地址代理过后访问国内的很慢，在浏览器中使用插件很麻烦，而且这样只对浏览器生效。
 所以最佳方法当然是使用系统的自动代理功能，这个功能要求输入一个URL，这个URL就是代理规则的文件，怎么来呢，用pac规则自动生成工具就行了，或者自己编写O(∩_∩)O哈哈~，下面用自动生成工具制作工具（直接使用现成的PAC文件见文章末尾）

**shadowsockets-qt5安装**



 **生成PAC文件有以下两个工具：**
 [Genpac](https://link.jianshu.com?t=https%3A%2F%2Fgithub.com%2FJinnLynn%2Fgenpac)
 [gfwlist2pac](https://link.jianshu.com?t=https%3A%2F%2Fgithub.com%2Fclowwindy%2Fgfwlist2pac)

这里使用第一个

**使用genpac生成PAC文件步骤**

- 安装genpac
- 命令行生成pac文件，需要使用一个被墙地址列表：`https://raw.githubusercontent.com/gfwlist/gfwlist/master/gfwlist.txt` 

```
genpac --proxy="SOCKS5 127.0.0.1:1080" --gfwlist-proxy="SOCKS5 127.0.0.1:1080" -o autoproxy.pac --gfwlist-url="https://raw.githubusercontent.com/gfwlist/gfwlist/master/gfwlist.txt"
```

- 设置系统自动代理，在设置-->网络设置-->代理设置中选择自动代理，URL填写生成的PAC文件地址，file://文件路径/文件名(可以直接把文件拖到URL栏)
- ![1535019223724](./Linux shadowsocks-qt5 教程.assets/1535019223724.png)

**如果懒得自己生成的话，用我已经生成了的**(这里是重点)

- [下载PAC文件](https://link.jianshu.com?t=https%3A%2F%2Fraw.githubusercontent.com%2FNeutree%2Fnote%2Fmaster%2Ftool%2Fshadowsocks%2Fautoproxy.pac)（）

- 本仓库中就有此文件直接下载后放到指定路径，然后将此文件拖到浏览器中查看url地址

  ![1535019548795](./Linux shadowsocks-qt5 教程.assets/1535019548795.png)

- 把该地址复制到`配置 URL`框中，点击`应用到系统全局`按钮

- 设置系统自动代理，在设置-->网络设置-->代理设置中选择自动代理，URL填写生成的PAC文件地址，file://文件路径/文件名(可以直接把文件拖到URL栏)，可能某些系统是`file:///..../....pac`，可以把文件拖到浏览器看地址



**相关文章**

[搭建ss](https://www.jianshu.com/p/ee6dd0a96d08)
 [ss+kcp加速](https://www.jianshu.com/p/71f130ebfd7b)
 [git clone 加速](https://www.jianshu.com/p/90081496f100)

**参考文档**

[参考文档](https://link.jianshu.com?t=http%3A%2F%2Fwww.linuxdiyf.com%2Flinux%2F18265.html)

[ubuntu 16.04 安装 shadowsocks-qt5 并配置 pac 全局代理](https://www.jianshu.com/p/2f038ff61d25)

[linux PAC 自动代理 规则设置](https://www.jianshu.com/p/f85b8b5cd647)



 

 

 

 

 