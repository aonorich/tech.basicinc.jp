---
layout: post
category : WordPress
title: Wordpressのリビジョン（revision）管理について
tagline: 自動バックアップのやつ 
author : kobayashi
tags : [Wordpress]
---
{% include JB/setup %}
Wordpressにはリビジョン管理機能がデフォルトでついてます。投稿の編集画面をずっと開いているときに、自動的に保存をしてくれるあれです。

「ちょっと間違えてしまったので、前の状態に戻したい！」

なんてときは保存されているリビジョンのバージョンに戻すことで解決します。


## 編集前の状態に戻す方法
＜戻し方＞

記事個別の投稿の編集画面を開きます。

↓

左上の表示オプションをクリック
![](/assets/img/2013-05-27-wp.png)

↓

表示する項目で「リビジョン」を選択

すると、リビジョンの項目が表示されるので、そこでもとに戻したいバージョンの記事を選択すればOK！

それぞれのバージョンの中身もちゃんとみれます。


とっても便利なこの機能。ただし、ちょっと問題が、、、



## リビジョン管理をするとデータが増え過ぎる？
このリビジョン管理は大変便利なんですが、デフォルトではリビジョンの管理に制限がなくどんどん作成されてしまうので、データを圧迫してしまう可能性があります。


さらに記事ごとにpost\_idが付与されるのですが、このpost\_idがリビジョンが作成されるたびにも増えていってしまうので実際の記事に付与されるIDがとびとびになります。（なんか気持ち悪いぐらいで動作上はなんにも問題はないです）


どのくらいリビジョンが作成されているかを確認するには「post\_type」をrevisionで絞り込めばいけます。

	select count(*) from wp_posts WHERE post_type = 'revision';
	

もちろん、投稿画面を開いてそこまで時間をかけなければ、それほど作成されないので気にする程でもないです。

気になるかたはリビジョンの設定を変更しましょう。


## リビジョン管理の設定を変更する
wp-config.phpに必要に応じて下記の設定を追加しましょう。


### リビジョン管理を無効にする
	define(WP_POST_REVISION, false);

### リビジョン管理数を制限する
	define(WP_POST_REVISION, <リビジョン数>);

### 自動保存の間隔を変更する
	define(AUTOSAVE_INTERVAL, <秒数>);
※デフォルトで60秒が設定されてます。


## プラグインでリビジョン管理
プラグインでも設定ができます。

#### ■[Bettar Delete Revision](http://wordpress.org/plugins/better-delete-revision/)

これはリビジョンデータを削除することができます。
どのくらいリビジョンが存在するのかも確認できるので、気になる人は見てみるといいかも。



#### ■[Revision Control](http://wordpress.org/plugins/revision-control/)

リビジョンの最大保存数を設定できます。

