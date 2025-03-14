# xiaogpt

自用，踩坑。

1. 英文阅读。已经修改部分代码，目前空格不会停顿太长，也有连读；
2. 系统建议用苹果或linux，WSL可能可以，但我不想搞；
3. 可以直接用 revChatGPT  `$HOME/.config/revChatGPT/config.json`，而且根据revChatGPT的配置文件，完全可以在同一个会话下聊，应该需要进一步改代码。

Play ChatGPT with Xiaomi AI Speaker

![image](https://user-images.githubusercontent.com/15976103/220028375-c193a859-48a1-4270-95b6-ef540e54a621.png)


## 一点原理

[不用 root 使用小爱同学和 ChatGPT 交互折腾记](https://github.com/yihong0618/gitblog/issues/258)


## 准备

1. ChatGPT id
2. 小爱音响
3. 能正常联网的环境或 proxy
4. python3.8+

## 使用

1. pip install aiohttp # 解决 miserver 依赖
2. pip install -r requirements.txt
3. 参考 [MiService](https://github.com/Yonsm/MiService) 项目 README 并在本地 terminal 跑 `micli list` 拿到你音响的 DID 成功 **别忘了设置 export MI_DID=xxx** 这个 MI_DID 用 
4. 参考 [revChatGPT](https://github.com/acheong08/ChatGPT) 项目 README 配置 chatGPT 的 config
5. run `python xiaogpt.py --hardware ${your_hardware}` hardware 你看小爱屁股上有型号，输入进来
6. 跑起来之后就可以问小爱同学问题了，“帮我"开头的问题，会发送一份给 ChatGPT 然后小爱同学用 tts 回答
7. 因为现在必须指定 conversation_id 和 parent_id 来持续对话，会自动建一个新的 conversation
8. 如果上面不可用，可以尝试用手机抓包，https://userprofile.mina.mi.com/device_profile/v2/conversation 找到 cookie 利用 --cookie '${cookie}' cookie 别忘了用单引号包裹
9. 默认用目前 ubus, 如果你的设备不支持 ubus 可以使用 --use_command 来使用 command 来 tts
10. 使用 --mute_xiaoai 选项，可以让小爱不回答，但会频繁请求，玩一下可以使用，不建议一直用
11. 使用 --account ‘${account}’ --password ‘${password}’ 可以不进行步骤 2
12. 如果有能力可以自行替换唤醒词，也可以去掉唤醒词，源码在 https://github.com/yihong0618/xiaogpt/blob/main/xiaogpt.py#L32
13. 可以使用 gpt-3 的 api 那样可以更流畅的对话，速度快, 请 google 如何用 openai api, 命令 --use_gpt3
14. 可以使用 --use_chatgpt_api 的 api 那样可以更流畅的对话，速度特别快，达到了对话的体验, 请 google 如何用 openai api, 命令 --use_chatgpt_api

e.g.
```shell
python3 xiaogpt.py --hardware LX06;
# or
python3 xiaogpt.py --hardware LX06 --conversation_id="xxxxxxxx";
# or 
python3 xiaogpt.py --hardware LX06 --cookie ${cookie};
# 如果你想直接输入账号密码
python3 xiaogpt.py --hardware LX06 --account ${your_xiaomi_account} --password ${your_password};
# 如果你想 mute 小米的回答
python3 xiaogpt.py --hardware LX06  --mute_xiaoai 
# 如果你想使用 gpt3 ai
export OPENAI_API_KEY=${your_api_key}
python3 xiaogpt.py --hardware LX06  --mute_xiaoai --use_gpt3
# 如果你想用 chatgpt api
export OPENAI_API_KEY=${your_api_key}
python3 xiaogpt.py --hardware LX06 --use_chatgpt_api
```

## config.json
如果想通过单一配置文件启动也是可以的, 可以通过--config参数指定配置文件, config文件必须是合法的JSON格式
参数优先级
- cli>default>config

```shell
python3 xiaogpt.py --config xiaogptconfig.json
```
或者
```shell
cp xiaogptconfig.json.example xiaogptconfig.json
python3 xiaogpt.py 
```

## 注意

1. 请开启小爱同学的蓝牙
2. 如果要更改提示词和 PROMPT 在代码最上面自行更改

## QA

1. 用破解么？不用
2. 连不上 revChatGPT？国情，你得设置 proxy 并且该地区可用的 proxy
3. 你做这玩意也没用啊？确实。。。但是挺好玩的，有用对你来说没用，对我们来说不一定呀
4. 想把它变得更好？PR Issue always welcome.
5. 还有问题？提 Issuse 哈哈

## 视频教程
https://www.youtube.com/watch?v=K4YA8YwzOOA

# 感谢

- [xiaomi](https://www.mi.com/)
- @[Yonsm](https://github.com/Yonsm) 的 [MiService](https://github.com/Yonsm/MiService) 

## 赞赏

谢谢就够了
