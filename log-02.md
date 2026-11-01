# GitHub 学习日志：第一次让网站出现浏览器小锁（HTTPS）

## 学习目标

今天的目标是让自己部署的网站从 **HTTP** 升级到 **HTTPS**，让浏览器地址栏出现安全锁（🔒）。

之前一直不知道 HTTPS 是怎么来的，以为只要买服务器就会自动有。实践之后才知道，中间其实涉及服务器、域名、Nginx 和 SSL 证书几个部分。

---

## 我的环境

- 云服务器：腾讯云 Ubuntu
- 本地电脑：Windows
- SSH 登录方式：`.pem` 密钥
- Web 服务器：Nginx
- 域名：已解析到服务器公网 IP

---

## 第一步：连接服务器

第一次真正使用 SSH 登录 Linux 服务器。

学习了：

- 什么是 SSH
- `.pem` 密钥有什么作用
- Windows 如何打开终端
- 如何使用 SSH 登录远程服务器

例如：

```bash
ssh -i xxx.pem ubuntu@服务器公网IP
```

第一次看到 Ubuntu 的命令行界面，说明已经成功连接服务器。

---

## 第二步：安装 Nginx

安装了 Nginx：

```bash
sudo apt update
sudo apt install nginx
```

然后启动服务：

```bash
sudo systemctl start nginx
sudo systemctl enable nginx
```

浏览器输入服务器 IP 后，看到了 Nginx 欢迎页面。

这一刻说明：

> 浏览器 → Internet → 腾讯云服务器 → Nginx

整个流程已经打通。

---

## 第三步：理解为什么没有小锁

虽然网站已经可以访问，但浏览器提示：

> Not Secure

原因是：

网站仍然使用的是 **HTTP（80端口）**。

HTTP 的内容都是明文传输，因此浏览器不会显示安全锁。

---

## 第四步：学习 HTTPS 是什么

了解到：

HTTPS = HTTP + SSL/TLS 证书

SSL 证书主要负责：

- 身份认证
- 数据加密
- 防止中间人攻击

浏览器只有验证证书合法后，才会显示：

🔒 Secure

---

## 第五步：申请 SSL 证书

使用 Let's Encrypt 免费证书。

安装 Certbot：

```bash
sudo apt install certbot python3-certbot-nginx
```

随后运行：

```bash
sudo certbot --nginx
```

Certbot 自动完成：

- 申请证书
- 配置 Nginx
- 自动开启 HTTPS
- 设置 HTTP 自动跳转 HTTPS

整个过程比想象中简单很多。

---

## 第六步：浏览器终于出现小锁

重新打开网站：

```
https://pancyspace.com
```

浏览器地址栏终于出现了：

🔒

这一刻真正理解了：

浏览器的小锁不是浏览器自己生成的，而是：

浏览器验证了服务器提供的 SSL 证书，并确认连接已经加密，因此才显示安全锁。

---

## 今天最大的收获

以前一直觉得：

> 网站上线 = 买服务器 + 上传代码。

现在知道实际上还有很多基础知识：

- Linux
- SSH
- Nginx
- 域名解析
- HTTP
- HTTPS
- SSL/TLS
- Let's Encrypt
- Certbot

这些共同组成了一个真正可以安全访问的网站。

---

## 遇到的问题

今天也踩了不少坑，例如：

- 不知道 `.pem` 文件应该放在哪里
- Windows 文件路径不会写
- SSH 登录命令格式容易输错
- 一开始分不清 HTTP 和 HTTPS 的区别
- 不理解浏览器为什么有时候有锁、有时候没有锁

但通过一步一步排查，最终成功完成了 HTTPS 配置。

---

## 总结

今天不仅完成了网站 HTTPS 配置，更重要的是理解了整个过程背后的原理。

第一次真正知道：

浏览器那个小小的🔒，背后其实涉及服务器配置、证书申请、网络协议和加密技术。

虽然只是一个小锁，但也是我第一次独立完成网站安全部署的重要里程碑。
