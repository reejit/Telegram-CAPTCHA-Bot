# Telegram-CAPTCHA-bot

一个用于验证新成员是不是真人的bot。

[![Deploy](https://www.herokucdn.com/deploy/button.svg)](https://heroku.com/deploy?template=https://github.com/reejit/Telegram-CAPTCHA-Bot.git)


![](https://img.shields.io/badge/license-AGPL3.0-%23373737.svg) ![https://python.org](https://img.shields.io/badge/python-3.6%2B-blue.svg) ![https://github.com/pyrogram/pyrogram/](https://img.shields.io/badge/Pyrogram-asyncio-green.svg)

A bot running on Telegram which will send CAPTCHA to verify if the new member is a human.

基于[原始项目](https://github.com/lziad/Telegram-CAPTCHA-bot)重制  

Remaked and forked based on [Original Repository](https://github.com/lziad/Telegram-CAPTCHA-bot)

修改者：Telegram [@Yoshida_Yuuko](https://t.me/Yoshida_Yuuko) Rsplwe

Bot实例: [@toorucaptchabot](https://t.me/toorucaptchabot)
## 原理

本 Bot 通过读取 Telegram API 中返回的入群消息来识别新用户入群，并生成一道随机问题对用户进行验证，非严格模式只要有回答问题就通过；严格模式下回答错误将会被移除或者封禁，这个验证的效果目前无法绕过具有人工操作的广告机器人，但是可以对外语（如阿拉伯语和波斯语）类骚扰用户起到一定的拦截作用。

Telegram Bot API 使用了基于 MTProto 框架的 pyrogram，多线程使用了 asyncio。

## 安装与使用
**由于 Bot 使用了 Python 3.6 的[变量类型标注](https://docs.python.org/zh-cn/3/library/typing.html)支持特性，在低于 Python 3.6 的版本上会出现 SyntaxError，因此源码只能在 Python 3.6+ 上运行!**  
1. 请先向 [@BotFather](https://t.me/botfather) 申请一个 Bot API Token  
> 你申请到的机器人会在你的 Telegram 账号所在数据中心上运行（即申请机器人的账号A位于 DC 5 (新加坡)，则 A 申请到的机器人也将会在 DC5 上运行)
2. 在 [Obtaining Telegram API ID](https://core.telegram.org/api/obtaining_api_id) 申请 API ID 与 API Hash
3. 在服务器上安装 pyrogram 以及 tgcrypto（以 Ubuntu 18.04 LTS 为例）: 
```
# 若未安装pip3，请先安装 python3-pip
apt install python3-pip
pip3 install -U https://github.com/Tooruchan/Telegram-CAPTCHA-bot/raw/master/pyrogram-asyncio.zip
# 由于 pyrogram 经常更新伴随着大改语法，所以在这里直接使用最适合当前版本的 pyrogram 版本，以免部署时发生意外情况。
# pyrogram-asyncio.zip 的校验：
# SHA1: E57BDF355E2B3CA04C6934BB94254ABA7A45A5AF
# CRC32: E4016E8D
pip3 install --upgrade tgcrypto configparser
```
``` 
git clone https://github.com/Tooruchan/Telegram-CAPTCHA-bot 
cd Telegram-CAPTCHA-bot
```

4. 将 auth.ini 里的 token 字段（与等号间存在一个空格）修改为你在 [@BotFather](https://t.me/botfather) 获取到的 API Token，api_hash 和 api_id 修改为你在步骤2中获得的两串内容，其中 API ID 为数字，而 API Hash 为一组字符，你也可以对 config.json 里的内容酌情修改。

有关填写字段说明:

`channel`: Bot 日志记录频道，未填写将会导致无法正常工作（这是一个 bug，等待修复）。

`admin`: 管理用户，不填写则`/leave`和`/reload`指令无效。

5. 使用 `python3 main.py` 直接运行这个 bot,或者在 `/etc/systemd/system/ `下新建一个 .service 文件，使用 systemd 控制这个bot的运行，配置文件示例请参考本项目目录下的 `example.service` 文件进行修改。

6. 将本 bot 加入一个群组，并给予封禁用户的权限，即可开始使用

## 在多个群组（10个以上等）部署本Bot的提示

~~由于一个已知无解的严重 Bug， Bot 在运行一周至13天左右的时间可能会由于线程冲突导致整个 Bot 死掉，如果需要在多个（10个以上）的群组内部署本 Bot 请考虑在crontab等地方设置定期重启。~~

现在的分支加入了一遇到异常就会自动重启的设定，Bot 在正常运行情况下应该是不会卡死了。

## 日志
在安装了 systemd ，且已经在 /etc/systemd/system 下部署了服务的 Linux 操作系统环境下，请使用命令：
```bash
journalctl -u captchabot.service 
# 这里的 captchabot.service 请自行更名为你在服务器上部署的服务名
```

## 项目实例
[@toorucaptchabot](https://t.me/toorucaptchabot)

本项目在 PyPy 3.6 和 pyrogram v0.16.0.asyncio 上测试通过  

[@AffyunWatchCatBot](https://t.me/AffyunWatchCatBot)

(环境为 Python 3.7.3 和 pyrogram v0.12.0.asyncio)

[@JustCaptchaBot](https://t.me/JustCaptchaBot)

(环境为 PyPy 3.6 + pyrogram v0.13.0.asyncio)

## 开源协议
本项目使用 GNU Affero 通用公共许可证 3.0 开源




