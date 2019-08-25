---
categories: [infra]
layout: default
title: IP制限がかかっているAPIをsshポートフォワーディングしてコールする
description: SSH portforward dns
tags: [SSH, portforward, dns]
image: /images/infra/ssh-port-forwarding-tmb.jpg
lang: ja_JP
---

> 投稿内容は私個人の意見であり、所属企業・部門見解を代表するものではありません。

# はじめに

IP制限が掛かっているAPIやサイトに特定サーバからだとアクセスできるけど  
localのマシンからだとIP制限でアクセスできない、ってことありますよね。  
先日、その悩みを解消したので備忘録として残します。

# 解決方法1　VPN(今回は使いません)

![Richbourg_VPN2.png](/images/infra/ssh-port-forwarding-1.png)

エンジニアが使いそうなVPNだと以下があります。

- [google cloud](https://cloud.google.com/vpn/pricing?hl=ja)
- [aws](https://aws.amazon.com/jp/vpn/)
- [azure](https://azure.microsoft.com/ja-jp/services/vpn-gateway/)

基本従量課金なんで今回は使わなかったです。

# 解決方法2　sshポートフォワーディング


本記事では[sshポートフォワーディングについての説明](http://www.koikikukan.com/archives/2016/09/15-000300.php)はせずに粛々とhow toだけ書いていきます。

例として、ssh接続先のvps.jp経由で、APIのエンドポイント（[https://httpbin.org/ip](https://httpbin.org/ip)）にアクセスできるようにしていきます。  
※[https://httpbin.org/ip](https://httpbin.org/ip)はIPが確認できるサイトです。

vps.jpのssh接続設定

> config

``` txt
host vps
  user hoge
  hostname vps.jp
  Identityfile /hoge/.ssh/hoge
  port 22
```

```ssh vps```で接続できることを確認した上で下記を追記します。

> config

``` txt
host tunnel-vps
  user hoge
  hostname vps.jp
  Identityfile /hoge/.ssh/hoge
  LocalForward 8000 httpbin.org:443
  port 22
```
追記が終わったら、```ssh tunnel-vps```でsshができることを確認して下さい。

ssh接続をしたままの状態で  
localhost:8000へアクセスするとア〜ラ不思議☆  
<b>httpbin.orgにはアクセスできません</b>

# なんで？
僕はずっと  
サーバ側(ssh)がDNS解決出来てないんだなってサーバ側の```/etc/hosts```を書き換えるってアホなことやってたんですが、永井大先生(身内ネタすいません)がご教授くれたんでなぜ駄目だったかと解決方法を書きます。

##### まず、なぜ駄目だったかの理由から
至極かんたんな理由でしてhttpbin.orgのサーバへlocalhostというドメインでアクセスしていた為、サーバ側のvirtual hostがどこへ振り分けていいかわからないという状況となっていました。

##### 解決方法
localマシン(MAC)の/etc/hostsに下記を追記します。

```
127.0.0.1	httpbin.org
```
超初歩的。

この状態で[https://httpbin.org:8000/ip](https://httpbin.org:8000/ip)へアクセスするとア〜ラ不思議☆  
<b>ssh接続先のglobal IPがちゃんと返ってきます!</b>

スバラ！！！