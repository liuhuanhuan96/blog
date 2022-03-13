---
title: 【Python实战案例】基于WebSocket的简易聊天室
tags:
  - Python
categories:
  - Python
toc: false
abbrlink: 55562
date: 2021-11-01 19:34:30
---



话不多说直接上代码：

<!--more-->

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <title>聊天室</title>
</head>
<body>
    <div id="contents" style="height:500px;overflow:auto;"></div>
    <div>
        <textarea id="msg"></textarea>
        <a href="javascript:;" onclick="sendMsg()">发送</a>
    </div>

<!-- jQuery -->
<script src="https://cdn.staticfile.org/jquery/3.3.1/jquery.min.js"></script>
<script type="text/javascript">
    var ws = new WebSocket("ws://127.0.0.1:2222/chat");
    ws.onmessage = function(e) {
        $("#contents").append("<p>" + e.data + "</p>");
    };
    function sendMsg() {
        var msg = $("#msg").val();
        ws.send(msg);
        $("#msg").val("");
    }
</script>
</body>
</html>

```

```python
# encoding=utf-8

from __future__ import unicode_literals, print_function
from datetime import datetime
import os

import tornado
from tornado.options import define, options
from tornado.web import RequestHandler
from tornado.websocket import WebSocketHandler

# 设置服务器端口
define("port", default=2222, type=int)


class IndexHandler(RequestHandler):
    def get(self):
        self.render("chat-client.html")


class ChatHandler(WebSocketHandler):
    users = set()  # 用来存放在线用户的容器

    def open(self):
        # 建立连接后添加用户到容器中
        self.users.add(self)

        # 向已在线用户发送消息??
        for user in self.users:
            remote_ip, port = self.request.connection.context.address
            now = datetime.now().strftime("%H:%M:%S")
            user.write_message("[{}][{}:{}]-进入聊天室".format(now, remote_ip, port))

    def on_message(self, message):
        # 向在线用户广播消息
        now = datetime.now().strftime("%H:%M:%S")
        remote_ip, port = self.request.connection.context.address
        for user in self.users:
            user.write_message("[{}][{}:{}] {}".format(now, remote_ip, port, message))

    def on_close(self):
        # 用户关闭连接后从容器中移除用户
        now = datetime.now().strftime("%H:%M:%S")
        remote_ip, port = self.request.connection.context.address
        self.users.remove(self)
        for user in self.users:
            user.write_message("[{}][{}:{}]-离开聊天室".format(now, remote_ip, port))

    def check_origin(self, origin):
        return True  # 允许WebSocket的跨域请求


if __name__ == '__main__':
    tornado.options.parse_command_line()

    app = tornado.web.Application([
        (r"/", IndexHandler),
        (r"/chat", ChatHandler),
    ],
        static_path=os.path.join(os.path.dirname(__file__), "static"),
        template_path=os.path.join(os.path.dirname(__file__), "template"),
        debug=True
    )

    http_server = tornado.httpserver.HTTPServer(app)
    http_server.listen(options.port)
    tornado.ioloop.IOLoop.current().start()


```

源码地址：https://gitee.com/liuhuanhuan963019/WebSocket_Chat_Python.git

欢迎关注！！！

