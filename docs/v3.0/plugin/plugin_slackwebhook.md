<!-- version-banner -->
!!! info ""
    ゆかコネNEO **v3.0** のドキュメントです。v2.3 をお使いの方は [v2.3 版のこのページ](../../v2.3/plugin/plugin_slackwebhook.md) を、違いを知りたい方は [v2.3 から v3.0 への移行](../../mig/mig_neo_v3.0.md) をご覧ください。

!!! Info "前提条件"
    * Webhook URL登録するためには Slack アカウントが必要です
    * プラグインは v2.0.115から同梱されています

## このプラグインで出来ること

* 音声認識結果をSlackチャットチャネル転送することができます

##　有効化

![slack](images/plugin_slackwebhook_p1.png)

* プラグインを使うチェックをONにしてください。

<!-- wpf-settings-note -->
!!! info "v3.0 で設定画面が新しくなりました"
    見た目がほかのプラグインと揃い、**表示言語に合わせて日本語・英語などで出る**ようになりました。
    各項目には「何を入れる欄なのか」「空のままだとどうなるのか」の説明が付いています。
    Webhook URL を設定します。**URL をどこで作るか**が画面に書かれています。

    設定は**下書き**として持たれます。閉じるときに「適用」「破棄」「続ける」の 3 択が出るので、
    試して気に入らなければ破棄できます。
    新しい画面が開けなかったときは、従来の画面が代わりに開きます。
    → [プラグインの有効化](enabled.md)

## 設定

![slack](images/plugin_slackwebhook_p2.png)

|設定|意味|
|:--|:---|
|Webhook URL|WebHookのアドレスを入れます。|

## 具体的な使い方

* まず、Slackクライアントから管理画面をだします

![slack](images/plugin_slackwebhook_p3.png)

* Slackアプリとして、Incomming Webhookを追加します

![slack](images/plugin_slackwebhook_p4.png)

* 書き込み先ｃｈを設定します

![slack](images/plugin_slackwebhook_p5.png)

* URLが発行されます。このアドレスをゆかコネNEOに設定します。

![slack](images/plugin_slackwebhook_p6.png)

* 認識が終わるごとに、転送されます。

![slack](images/plugin_slackwebhook_p7.png)
