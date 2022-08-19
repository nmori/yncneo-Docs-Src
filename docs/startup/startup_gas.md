!!! Info "前提条件"
    * GASを使った翻訳は Version 1.9592 から対応しています
    * Googleアカウントが必要です

!!! info "謝辞"
    * [@satto_sann(株式会社ZOZO) 様](https://qiita.com/satto_sann)の技術記事を参照しています。ありがとうございます。


## GASとは

* Googleの機能で、自作プログラムを動かすことができる機能です。
* 翻訳結果を加工するなど、個人で機能を拡張することができます。

## GASをつかった翻訳とは

* 個人のGoogleアカウントに紐づく機能を使うことで自前APIでの翻訳を実現します。
* 個人での作業が発生します。

## 設定の仕方

### 1. GASの設定をする

* [こちらの資料](https://qiita.com/satto_sann/items/be4177360a0bc3691fdf)を参考にGASの設定をしてください。

### 2. アドレスの設定をする

![GASオプション](images/plugin_gas_p1.png)

* ゆかりねっとコネクターNEOのオプション枠にあるURL欄にURLをいれます。
* 入れるURLは /exec の手前まで。<br>
例）``https://script.google.com/macros/s/aAaaaaaaaaaaaaaaaa`` 


### 3. 翻訳を使う設定

![翻訳オプション](images/plugin_gas_p2.png)

* 選択でGASを選んでください。

!!! info "仕様について"
    * 入力される言語は母国語を想定しています。
    * 言語推定をGoogle側に一任しているので、翻訳が失敗することもあります。
    * 翻訳は一定数使うとGAS側で制約がかかります。
    * GASの仕様は変わることがあります。かかるコストなどは個人で調査しご利用ください。