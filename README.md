# cockroachai-web

## 更新了新的账户系统更加方便，指路[cockroachai-oauth](https://github.com/lyy0709/cockroachai-oauth)
此为增加了管理后台的cockroachai版本，写的比较匆忙部分功能未实现，如refreshcookie的实时显示，未实现refreshcookie的热加载（蟑螂本身不支持）导致此功能只有在refreshcookie过期时可用，未添加审计接口，未做安全防范，请不要暴露你的ip以及其他信息，项目打包好已开源，开源地址[cockroachai-web-code](https://github.com/lyy0709/cockroachai-web-code)

交流群: https://t.me/xyhelper

## 重要提示

- 请在使用时将./config/condig.yaml文件夹中需要的功能解除注释，即变为启用状态，并固定一个管理员密码，本项目会清除注释项，仅支持ip:端口登录，反代时注释掉websocket，反代后跳转账号登录失效，手动在后面加上/getsession，其他错误概不负责，上传refreshcookie只确保能上传不确保能否使用

## 更新功能

- 更新刷新cockroachai的登录，输入cockroachai的容器名，未更改应该为cockroachai_cockroachai_1或cockroachai-cockroachai-1，可实现删除后启动容器实现对usertokens的刷新（防止token过期后依然白嫖）
- 容器名可在运行后的输出中查看，如下

[![pF1ATd1.jpg](https://s11.ax1x.com/2024/02/06/pF1ATd1.jpg)](https://imgse.com/i/pF1ATd1)
- 重要！需将cockroachai文件夹放在/home文件夹下，即/home/cockroachai，防止白嫖功能才能生效

## 更新方法

1. 拉取我的项目或者单独复制docker-compose.yml里的内容（建议以及配置好cockroachai的选择单独复制docker-compose.yml里的内容，但注意设置固定管理员密码），建议放置于/home文件夹下

- 拉取指令
```bash
git clone https://github.com/lyy0709/cockroachai-web.git cockroachai
```

2. 执行`./deploy.sh` 完成更新
- 执行指令
```bash
cd cockroachai && ./deploy.sh
```

## 功能

- 主要功能同cockroachai

- 后台管理userTokens（实时生效）

- 后台管理refreshcookie（不实时生效，只添加一个可上传的接口）

- 跳转到账号登录

- 实现token刷新

## 配置要求

同cockroachai

## 使用方法

1.后台地址

- 后台地址为你的服务器公网IP:8999（端口可自行修改）

2.登录密码

- 登录密码为cockroachai的管理员密码，请在配置cockroachai时设置一个固定的密码

## 安装方法（Docker）

- 同cockroachai，将cockroachai中的docker-compose.yml文件替换未本项目的即可，或手动替换为以下

```bash
version: '3'
services:
  cockroachai:
    image: xyhelper/cockroachai:latest
    restart: always
    ports:
      - "9000:9000" #左侧端口暴露在外,可根据需求更改
    volumes:
      - ./config:/app/config
        # - ./resource:/app/resource
    environment:
      ASSET_PREFIX: https://oaistatic-cdn.closeai.biz
  cockroachai-web:
    image: lyy0709/cockroachai-web:latest
    restart: always
    ports:
      - "8999:8999" #左侧端口暴露在外,可根据需求更改
    volumes:
      - ./config:/usr/src/app/config
      - /var/run/docker.sock:/var/run/docker.sock
  
```
## 运行图片

[![pF1AoZR.jpg](https://s11.ax1x.com/2024/02/06/pF1AoZR.jpg)](https://imgse.com/i/pF1AoZR)
[![pF1A7Ix.jpg](https://s11.ax1x.com/2024/02/06/pF1A7Ix.jpg)](https://imgse.com/i/pF1A7Ix)


