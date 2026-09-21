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

## 設定

プラグイン一覧で、このプラグインの名前の右にある **「設定」** を押すと開きます。

!!! info "閉じるときの 3 択"
    設定は**下書き**として持たれ、「OK」か「適用」を押すまで動いているプラグインには効きません。
    変更したまま閉じようとすると「変更が保存されていません」と聞かれ、**［はい］保存して閉じる／［いいえ］破棄して閉じる／［キャンセル］閉じるのをやめる** から選べます。

Slack のチャンネルへ字幕を流します。

![Slack 連携の設定 - Slack](images/v30/slackwebhook_1.png)

| 項目 | 説明 |
|:--|:--|
| Webhook URL | Slack アプリの設定で作った Incoming Webhook の URL を貼り付けます。空のままだと何も送りません。 |

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
