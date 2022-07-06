## 题目介绍

[附件](/CTF_ATTACHMENTS/2022/ACTF-myclient.zip)

```
A cute mysql here, try to exploit it!
http://124.71.205.170:10047

The /tmp of the remote environment is fixed and does not require sql injection
The directory is cleaned every five minutes
It is recommended to test locally first

远程的环境的/tmp是固定的，不需要sql注入
/tmp目录每五分钟清理一次
建议先测试本地
```

考点：
- mysql选项
- 恶意认证Server

## Writeup

官方WP： https://github.com/team-s2/ACTF-2022

