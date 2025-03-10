# ハンズオン: 「開発者ポータル」の作成

■開発者ポータルの設定

- 画面左メニューの「ポータルの概要」をクリック
- 画面上部の「開発者ポータル」をクリック

![](images/ss-2022-04-08-08-48-45.png)

Webブラウザーで新しいタブが開く

![](images/ss-2022-04-08-08-49-18.png)

ページが表示されるまで1分ほど待つ

「開発者ポータル」のデザイン画面が表示される。

![](images/ss-2022-04-08-08-50-34.png)

ページ内の要素を編集できる。

![](images/ss-2022-04-08-08-56-20.png)

![](images/ss-2022-04-08-08-56-38.png)

編集後は保存する。

![](images/ss-2022-04-08-08-58-59.png)

参考: https://www.google.com/search?q=%E3%83%95%E3%83%AD%E3%83%83%E3%83%94%E3%83%BC+%E4%BF%9D%E5%AD%98%E3%83%9C%E3%82%BF%E3%83%B3


「開発者ポータル」のデザイン画面のタブを閉じる。

![](images/ss-2022-04-08-09-00-02.png)


Azure portalのページを、F5（再読み込み）でリロードする。「公開」ボタンが押せるようになる。

![](images/ss-2022-04-08-09-02-23.png)

 
  - 「公開」をクリック
  - 「はい」をクリック

![](images/ss-2022-04-08-09-02-44.png)

  - 「CORSを有効にする」をクリック

![](images/ss-2022-04-08-09-03-10.png)

  - 「はい」をクリック

![](images/ss-2022-04-08-09-03-31.png)

■製品の設定

Azure portal＞API Management＞（作成したリソース）

- 画面左メニューの「製品」をクリック

![](images/ss-2022-04-08-09-07-20.png)

- Starterをクリック

![](images/ss-2022-04-08-09-07-38.png)

- 画面左メニューの「設定」をクリック
- 「サブスクリプションを要求する」のチェックを外す
- 画面上部の「保存」をクリック

![](images/ss-2022-04-08-09-08-17.png)

■開発者ポータルの利用


「製品」の「Starter」のページから、「API Management」のインスタンスのトップページへ戻る。

![](images/ss-2022-04-08-09-09-02.png)

- 画面左メニューの「概要」(一番上)をクリック
- 「開発者ポータルのURL」をクリップボードにコピー

![](images/ss-2022-04-08-09-10-33.png)

- Webブラウザーで、Ctrl + Shift + Nを押して、InPrivateウィンドウ（シークレットウィンドウ）を開く。
- コピーしたURL（開発者ポータル）にアクセスする

![](images/ss-2022-04-08-09-11-59.png)

- Explore APIsをクリック

![](images/ss-2022-04-08-09-12-07.png)

- tenki-v1をクリック

![](images/ss-2022-04-08-09-12-30.png)

- Try itをクリック

![](images/ss-2022-04-08-09-12-55.png)

- （画面下部にスクロールして）Sendをクリック

![](images/ss-2022-04-08-09-13-23.png)

- 東京の天気予報の情報が表示される

![](images/ss-2022-04-08-09-13-47.png)