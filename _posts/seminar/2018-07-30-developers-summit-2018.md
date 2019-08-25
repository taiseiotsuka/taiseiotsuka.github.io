---
categories: [seminar]
layout: default
title: developers summit 2018 summer - Neural Networkについて
description: DevelopersSummit2018
tags: [DevelopersSummit2018]
image: /images/seminar/developers-summit-2018-tmb.png
lang: ja_JP
---

# はじめに

7月27日 [developers summit 2018 summerでSONYが開催していたセミナー](https://event.shoeisha.jp/devsumi/20180727/session/1756/)に参加してきました。  
![スクリーンショット 2018-07-30 11.28.11.png](/images/seminar/developers-summit-2018-1.png)


せっかくなので

- 行きたかったけど行けなかった人
- Neural Networkって具体的にどういうものか知りたい人

へ向けて記事を書こうと思います。

# 当日行われた流れ

1. 成平 拓也さん自己紹介
2. なぜDeep Learningなのか
3. 導入事例紹介
4. プログラムを用いたデモンストレーション
5. SONY「Neural Network Console」最新情報
6. まとめ

上記からいくつかの重要な点だけ抜粋して記述します。

# なぜDeep Learningなのか

![スクリーンショット 2018-07-30 11.16.01.png](/images/seminar/developers-summit-2018-2.png)

もっとわかり易く、ディープラーニング(深層学習)はその他の機械学習手法とどう違うのか
https://products.sint.co.jp/aisia/blog/vol1-5

# SONYの提供する「Neural Network Console」と「Neural Network Libraries」について
- Neural Network Console
  - https://dl.sony.com/ja/
- Neural Network Libraries
  - https://github.com/sony/nnabla

「Neural Network Console」は
研究や、商用レベルの技術開発に対応したDeep Learningツール。  
GUIによるビジュアルな操作。

- 主なターゲット
  - 特に開発効率を重視される方
  - 初めてディープラーニングにふれる方

「Neural Network Libraries」は  
Deep Learning研究開発者向けオープンソースフレームワーク。  
コーディングを通じて利用。

- 主なターゲット
  - じっくりと研究・開発に取り組まれる方
  - プログラミング可能な研究、開発者

# デモンストレーション 1
画像認識機能によるデモンストレーション  
![スクリーンショット 2018-07-30 14.30.40.png](/images/seminar/developers-summit-2018-3.png)

上記のような画像と正解の数字の２つのデータを用意しNeural Network Consoleにて学習させます。  
そしてそこで学習し終えたモデルをNeural Network Librariesで作成した画像認識システムにて使用します。

画像認識システムは手書きで書いた数字をなんの数字であるかを判別していました。

# デモンストレーション 2
距離空間学習 ~Siamese Network~
![CameraSoft](/images/seminar/developers-summit-2018-4.jpg)
![CameraSoft](/images/seminar/developers-summit-2018-5.jpg)

手書きの画像を二次元に飛ばし数字と数字の間の距離を求め最も類似する文字列は何かを判定するというデモンストレーションを行っていました。  
...どう距離計算してるのか全くわからん（；＾ω＾）

# 感想
セミナーを聞いてて一番のミソだなあと思った所なんですがDeep Learningの開発者が不足していてその育成にConsoleとLibrariesが使われればとおっしゃっていました。

もちろん儲けベースで利用者が増えればという側面もあるかと思いますが、私のような機械学習初心者も引き込んでくれそうな可能性を感じたため画像認識システム作って見ようと思いました。  
SONYさんの使うかわかんないけどw