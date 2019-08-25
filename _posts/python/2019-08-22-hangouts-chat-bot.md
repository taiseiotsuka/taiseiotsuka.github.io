---
categories: [python]
layout: default
title: google hangouts chat botってやつを作ってみた
description: Django GitHub Python
tags: [Django, GitHub, Python]
image: /images/python/hangouts-chat-bot-tmb.png
lang: ja_JP
---

# はじめに 

今日イチ笑えた動画です。  
[【史上最恐】｢なんでもあり｣のカードを使って罰ゲームを回避せよ！](https://youtu.be/DHelYnbQ458)  
今あなたが業務中でないならこの記事を閉じてこっちを見ることをオススメする。

# はじめに 2

無駄話失礼しました。  
とりあえず、タイトルのとおりです。

- 使用技術
- bot作成方法
- google hangouts chat apiの仕様

この３つを完結に書きます。  
<b>本件で使用したプログラムはgithubにアップしています</b>ので興味のある方はどうぞ。  
[github:example_google_chatbot](https://github.com/taiseiotsuka/example_google_chatbot)

# 使用技術
- python 3系
- Django 2系
- google cloud platform

# bot作成方法
1. Webhook用エンドポイントのプログラムを作成します。
2. gcpのコンソールを開きます。
3. APIタブのダッシュボードに移ります。
4. google hangouts chatと検索します。
5. google hangouts chat apiを有効化します。
6. hangouts chat apiの設定画面を開きWebhook用のエンドポイントを登録します。
7. hangouts chat apiの設定画面でbot名を入力します。
8. hangouts chatを開いて7で設定したbot名を検索します。
9. なんでもいいのでbotに話しかけてみましょう。

# google hangouts chat apiの仕様
作成方法の項目1がミソなので、どういう仕様でWebhook用のエンドポイント作ればいいか解説します。

botにメッセージ送った際にエンドポイントにjsonのpostリクエストが飛びます。  
エンドポイントではそれを受け取り、処理しresponceします。  
※日本語の記事で見なかったのが、何をresponceするかの部分です。

下記が実際に作成して動作確認済みのコードです。

> views.py

``` python
from django.http.response import JsonResponse
from django.views.decorators.csrf import csrf_exempt
from django.views.decorators.http import require_http_methods
import json

@require_http_methods(["POST"])
@csrf_exempt
def message(request):
	event = json.loads(request.body)
	if event["type"] == "MESSAGE":
		return JsonResponse({"text": event["message"]["argumentText"]})
```

``` python
return JsonResponse({"text"
```
となっているようにtextというkeyのあるjsonをレスポンスすれば、自動的にbotがその内容を返してくれます。

# まとめ
今回は応答型のbotを作りましたが全体に対して任意のタイミングにメッセージを送るタイプのapiもあるので、  
興味ある方はgoogle hangouts chat apiのドキュメントを見てもらえればと思います。

以上！！