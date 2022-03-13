---
title: 【Python】SMTP发送邮件
tags:
  - Python
categories:
  - Python
toc: true
abbrlink: 52552
date: 2021-07-25 13:54:33
---

SMTP（Simple Mail Transfer Protocol）即简单邮件传输协议,它是一组用于由源地址到目的地址传送邮件的规则，由它来控制信件的中转方式。

python的smtplib提供了一种很方便的途径发送电子邮件。它对smtp协议进行了简单的封装。

Python创建 SMTP 对象语法如下：

<!--more-->

```python
import smtplib

smtpObj = smtplib.SMTP( [host [, port [, local_hostname]]] )
```

参数说明：

- host: SMTP 服务器主机。 你可以指定主机的ip地址或者域名如:runoob.com，这个是可选参数
- port: 如果你提供了 host 参数, 你需要指定 SMTP 服务使用的端口号，一般情况下SMTP端口号为25。
- local_hostname: 如果SMTP在你的本机上，你只需要指定服务器地址为 localhost 即可。

Python SMTP对象使用sendmail方法发送邮件，语法如下：

```python
SMTP.sendmail(from_addr, to_addrs, msg[, mail_options, rcpt_options]
```

参数说明：

- from_addr: 邮件发送者地址。
- to_addrs: 字符串列表，邮件发送地址。
- msg: 发送消息

这里要注意一下第三个参数，msg是字符串，表示邮件。我们知道邮件一般由标题，发信人，收件人，邮件内容，附件等构成，发送邮件的时候，要注意msg的格式。这个格式就是smtp协议中定义的格式。



==实例==

​	*163邮箱发送测试邮件到QQ邮件*

~~~python
import smtplib
from email.mime.text import MIMEText
from email.header import Header

# 发送邮件服务器地址
smtp_server = 'smtp.163.com'

# 发送方账号
sender = 'xxxxxxxxx@163.com'
# 发送方密码（或授权密码）
password = 'xxxxxxxxx'
# 收件方邮箱
receiver = 'xxxxxxx@qq.com'
# 邮件标题
subject = 'Python SMTP 测试邮件'
# 邮件内容
mail_msg = 'Python 测试邮件发送。。。。'

# 三个参数：第一个为文本内容，第二个 plain 设置文本格式，html 设置文本格式为html格式  第三个 utf-8 设置编码
message = MIMEText(mail_msg, 'plain', 'utf-8')  # 发送内容 （文本内容，发送格式，编码格式）
# 发送地址
message['From'] = sender
# 接受地址
message['To'] = receiver
# 邮件标题
message['Subject'] = Header(subject,'utf-8')

try:
    # 创建SMTP对象
    smtp = smtplib.SMTP()

    # 连接服务器
    smtp.connect(smtp_server)

    # 登录邮箱账号
    smtp.login(sender, password)

    # 发送账号信息
    smtp.sendmail(sender, receiver, message.as_string())
    print('success:发送成功')
except smtplib.SMTPException:
    print('error:邮件发送失败')
finally:
    # 关闭
    smtp.quit()
~~~

我们使用三个引号来设置邮件信息，标准邮件需要三个头部信息： **From**, **To**, 和 **Subject** ，每个信息直接使用空行分割。

我们通过实例化 smtplib 模块的 SMTP 对象 *smtpObj* 来连接到 SMTP 访问，并使用 *sendmail* 方法来发送信息。

程序结果：

<img src="https://tva1.sinaimg.cn/large/008eGmZEgy1gmf6hk1uthj30lq06xweu.jpg" alt="image-20210107154721239" style="zoom:50%;" />

> 注意：第一次发送邮件时，如果填写发送方的账号密码可能回出现错误：smtplib.SMTPAuthenticationError: (535, b'Error: authentication failed')
>
> 此时需要去发送方对应的邮箱设置中找到smtp的授权密码：参考（https://jingyan.baidu.com/article/c275f6ba33a95de33d7567d9.html）开启后，填写授权码在密码处，重新发送即可

## 使用Python发送HTML格式的邮件

Python发送HTML格式的邮件与发送纯文本消息的邮件不同之处就是将MIMEText中_subtype设置为html。具体代码如下：

~~~python
import smtplib
from email.mime.text import MIMEText
from email.header import Header

# 发送邮件服务器地址
smtp_server = 'smtp.163.com'

# 发送方账号
sender = 'xxxxxxxxx@163.com'
# 发送方密码（或授权密码）
password = 'xxxxxxxxx'
# 收件方邮箱
receiver = 'xxxxxxx@qq.com'
# 邮件标题
subject = 'Python SMTP 测试邮件'
# 邮件内容
mail_msg =  """
            <p>Python 邮件发送测试...</p>
            <p><a href="http://www.baidu.com">这是一个链接</a></p>
"""

# 三个参数：第一个为文本内容，第二个 plain 设置文本格式，html 设置文本格式为html格式  第三个 utf-8 设置编码
message = MIMEText(mail_msg, 'plain', 'utf-8')  # 发送内容 （文本内容，发送格式，编码格式）
# 发送地址
message['From'] = sender
# 接受地址
message['To'] = receiver
# 邮件标题
message['Subject'] = Header(subject,'utf-8')

try:
    # 创建SMTP对象
    smtp = smtplib.SMTP()

    # 连接服务器
    smtp.connect(smtp_server)

    # 登录邮箱账号
    smtp.login(sender, password)

    # 发送账号信息
    smtp.sendmail(sender, receiver, message.as_string())
    print('success:发送成功')
except smtplib.SMTPException:
    print('error:邮件发送失败')
finally:
    # 关闭
    smtp.quit()
~~~

<img src="https://tva1.sinaimg.cn/large/008eGmZEgy1gmf7mbspynj313w0bu3zj.jpg" alt="image-20210107162702921" style="zoom:50%;" />

## Python 发送带附件的邮件

*发送带附件的邮件，首先要创建MIMEMultipart()实例，然后构造附件，如果有多个附件，可依次构造，最后利用smtplib.smtp发送。*

~~~python
import smtplib
from email.mime.text import MIMEText
from email.mime.multipart import MIMEMultipart
from email.mime.image import MIMEImage
from email.header import Header

# 发送邮件服务器地址
smtp_server = 'smtp.163.com'

# 发送方账号
sender = 'x x x x xxx@163.com'
# 发送方密码（或授权密码）
password = 'xxxxxxx'
# 收件方邮箱
receiver = 'xxxxxxxxx@qq.com'
# 邮件标题
subject = 'Python SMTP 测试邮件'
# 邮件内容
mail_msg =  """
            <p>Python 邮件发送测试...</p>
            <p><a href="http://www.baidu.com">这是一个链接</a></p>
"""

# 创建一个带附件的实例
message = MIMEMultipart()

# 三个参数：第一个为文本内容，第二个 plain 设置文本格式，html 设置文本格式为html格式  第三个 utf-8 设置编码
# message = MIMEText(mail_msg, 'html', 'utf-8')  # 发送内容 （文本内容，发送格式，编码格式）
# 发送地址
message['From'] = sender
# 接受地址
message['To'] = receiver
# 邮件标题
message['Subject'] = Header(subject,'utf-8')


# 添加邮件正文内容
message.attach(MIMEText(mail_msg, 'html', 'utf-8'))

# 构造附件1，传送当前目录下的 809147873.jpeg 文件
att1 = MIMEText(open('809147873.jpeg', 'rb').read(), 'base64', 'utf-8')
# 此处为固定的格式，可以在浏览器中查看到相关信息
att1["Content-Type"] = 'application/octet-stream'
# 这里的 filename 命名任意，即在邮件中显示的名称
att1["Content-Disposition"] = 'attachment; filename="809147873.jpeg"'
message.attach(att1)

# 可以发送多个附件
# # 构造附件2，传送当前目录下的 1543852953700.jpg 文件 由于使用的是图片，采用base64加密方式进行传输
att2 = MIMEText(open('1543852953700.jpg', 'rb').read(), 'base64', 'utf-8')
att2["Content-Type"] = 'application/octet-stream'
att2["Content-Disposition"] = 'attachment; filename="1543852953700.jpg"'
message.attach(att2)

try:
    # 创建SMTP对象
    smtp = smtplib.SMTP()

    # 连接服务器
    smtp.connect(smtp_server)

    # 登录邮箱账号
    smtp.login(sender, password)

    # 发送账号信息
    smtp.sendmail(sender, receiver, message.as_string())
    print('success:发送成功')
except smtplib.SMTPException:
    print('error:邮件发送失败')
finally:
    # 关闭
    smtp.quit()
~~~

实验结果：

<img src="https://tva1.sinaimg.cn/large/008eGmZEgy1gmfa0v1mb4j313u0h677a.jpg" alt="image-20210107175014035" style="zoom:50%;" />

<img src="Users/liuhuanhuan/Library/Application Support/typora-user-images/image-20210107175241392.png" alt="image-20210107175241392" style="zoom:50%;" />

## 在 HTML 文本中添加图片并多人发送

邮件的 HTML 文本中一般邮件服务商添加外链是无效的，正确添加图片的实例如下所示：

~~~python
import smtplib
from email.mime.text import MIMEText
from email.mime.multipart import MIMEMultipart
from email.mime.image import MIMEImage
from email.header import Header

# 发送邮件服务器地址
smtp_server = 'smtp.163.com'

# 发送方账号
sender = 'xxxxxx@163.com'
# 发送方密码（或授权密码）
password = 'xxxxxxxx'
# 收件方邮箱
# 发送多个时可能存在图片不显示的问题
receiver = ['xxxxx@qq.com','xxxxx9@qq.com']
# receiver = 'xxxxx@qq.com'
# 邮件标题
subject = 'Python SMTP 文本新增图片及多人发送'
# 邮件内容
mail_msg =  """
            <p>Python 邮件发送测试...</p>
            <p><a href="http://www.baidu.com">这是一个链接</a></p>
            <p>图片演示：</p>
            <p><img src="cid:img"></p>
"""

# 创建一个带附件的实例

# MIME邮件中除了可以携带各种附件外，还可以将其它内容以内嵌资源的方式存储在邮件中
message = MIMEMultipart('related')

# 发送地址
message['From'] = sender
# 接受地址
message['To'] = ','.join(receiver)
# 邮件标题
message['Subject'] = Header(subject,'utf-8')


# # 构造正文内容
# MIME邮件可以传送超文本内容，但出于兼容性的考虑，一般在发送超文本格式内容的同时会同时发送一个纯文本内容的副本，
# 如果邮件中同时存在纯文本和超文本内容，则邮件需要在Content-Type域中定义multipart/alternative类型，
# 邮件通过其boundary中的分段标识将纯文本、超文本和邮件的其它内容分成不同的段。
body = MIMEMultipart('alternative')
body.attach(MIMEText(mail_msg, 'html', 'utf-8'))

# # 读取需要在邮件正文显示的图片
with open('809147873.jpeg', 'rb') as f:
    msgImage = MIMEImage(f.read())
#
# # 定义图片 ID，在 HTML 文本中引用
msgImage.add_header('Content-ID', '<img>')
message.attach(msgImage)
#
message.attach(body)
#
# 构造附件1，传送当前目录下的 809147873.jpeg 文件
att1 = MIMEText(open('809147873.jpeg', 'rb').read(), 'base64', 'utf-8')
# 此处为固定的格式，可以在浏览器中查看到相关信息
att1["Content-Type"] = 'application/octet-stream'
# 这里的 filename 命名任意，即在邮件中显示的名称
att1["Content-Disposition"] = 'attachment; filename="809147873.jpeg"'
message.attach(att1)

# 可以发送多个附件
# # 构造附件2，传送当前目录下的 1543852953700.jpg 文件 由于使用的是图片，采用base64加密方式进行传输
att2 = MIMEText(open('1543852953700.jpg', 'rb').read(), 'base64', 'utf-8')
att2["Content-Type"] = 'application/octet-stream'
att2["Content-Disposition"] = 'attachment; filename="1543852953700.jpg"'
message.attach(att2)

try:
    # 创建SMTP对象
    smtp = smtplib.SMTP()

    # 连接服务器
    smtp.connect(smtp_server,port=25)

    # 登录邮箱账号
    smtp.login(sender, password)

    # 发送账号信息
    smtp.sendmail(sender, receiver, message.as_string())
    print('success:发送成功')
except smtplib.SMTPException:
    print('error:邮件发送失败')
finally:
    # 关闭
    smtp.quit()
~~~

实验结果：

<img src="https://tva1.sinaimg.cn/large/008eGmZEgy1gmfbd0pl6rj31620qyat0.jpg" alt="image-20210107183619242" style="zoom:50%;" />
