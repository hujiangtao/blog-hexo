---
title: 关于acme.sh的摘录
date: 2023-06-06 19:21:43
categories:
- 建站
- 摘录
tags:
- acme.sh
- SSL
---
## 1. 简介
`acme.sh`实现了`acme`协议, 可以从`letsencrypt`等支持SSL验证的服务生成免费的证书。acme.sh的官方位置是Github上[acme.sh](https://github.com/acmesh-official/acme.sh)

## 2. 安装
普通用户和root用户都可以运行`acme.sh`脚本进行安装

```bash
curl https://get.acme.sh | sh -s email=my@example.com
```

`acme.sh`安装实现了
* 把 acme.sh 安装到你的 home 目录下:` ~/.acme.sh/`；并创建 一个 `shell` 的 `alias`, 例如 `.bashrc`，方便你的使用: `alias acme.sh=~/.acme.sh/acme.sh`

* 自动为你创建 cronjob, 每天 0:00 点自动检测所有的证书, 如果快过期了, 需要更新, 则会自动更新证书。

## 3. 生成证书
acme.sh 实现了 acme 协议支持的所有验证协议。 一般有两种方式验证: http验证 和 dns验证。
<!-- more -->
### 3.1. http验证

#### 3.1.1. 通用http验证
通用http验证需要在你的网站根目录下放置一个文件, 来验证你的域名所有权；完成验证后就可以生成证书。

```bash
acme.sh --issue -d mydomain.com -d www.mydomain.com --webroot /home/wwwroot/mydomain.com/
```

#### 3.1.2. Apache服务器验证
在apache服务器中，acme.sh可以从 apache的配置中自动完成验证, 而不需要指定网站根目录。

```bash
acme.sh --issue -d mydomain.com --apache
```

#### 3.1.3. Apache服务器验证
同样在Nginx服务器中，acme.sh也可以从 Nginx配置中自动完成验证, 不需要指定网站根目录。

```bash
acme.sh --issue -d mydomain.com --nginx
```

#### 3.1.4. 80端口没有被占用
如果服务器上的80 端口是空闲的, acme.sh可以虚拟一个webserver, 临时监听80端口完成验证。

```bash
acme.sh --issue -d mydomain.com --standalone
```

**需要注意的是：即使指定了服务器的类型（Apache或Nginx），acme.sh也不会私自修改用户的配置文件，它只会生成证书。必要的SSL配置需要用户来修改相关的配置文件。**

### 3.2. dns验证

#### 3.2.1. 手动`dns`方式
手动`dns`方式是手动在域名上添加一条 txt 解析记录, 验证域名所有权。这种方式的好处是不需要任何服务器, 不需要任何公网 ip, 只需要 dns 的解析记录即可完成验证。坏处是使用这种方式 acme.sh 将无法自动更新证书，每次都需要手动再次重新解析验证域名所有权。

```bash
acme.sh --issue --dns -d mydomain.com \
 --yes-I-know-dns-manual-mode-enough-go-ahead-please
```

执行上面的指令后, acme.sh 会生成相应的解析记录并显示出来, 然后需要手动在域名管理面板中添加这条 txt 记录。
然后执行下面的指令就可以生成证书。

```bash
acme.sh --renew -d mydomain.com \
  --yes-I-know-dns-manual-mode-enough-go-ahead-please
```

#### 3.2.2. 通过api自动`dns`方式
通过域名解析商提供的 api 可以自动添加 txt 记录，并完成验证。acme.sh 目前支持 cloudflare, dnspod, cloudxns, godaddy 以及 ovh 等数十种解析商的自动集成.
以 dnspod 为例, 你需要先登录到 dnspod 账号, 生成你的 api id 和 api key。 然后执行指令:

```bash
export DP_Id="1234"
export DP_Key="sADDsdasdgdsf"
acme.sh --issue --dns dns_dp -d aa.com -d www.aa.com
```

第二次再验证就不需要Id和key了

```bash
acme.sh --issue -d mydomain2.com --dns  dns_dp
```
在Github [acme.sh](https://github.com/acmesh-official/acme.sh)中的dnsapi目录里，是常用域名解析商的api。在各个`.sh`脚本中又相关的例子。