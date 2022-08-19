!!! Info "前提条件"
    * 棒読みちゃんの通信ポートがひらいていること
    * 棒読みちゃんが起動していること

## このプラグインで出来ること

* 棒読みちゃんをつかって音声認識結果を読み上げできます。

##　有効化

![棒読み](images/plugin_bouyomi_p1.png)

* プラグインを使うチェックをONにしてください。

## 設定

![棒読み](images/plugin_bouyomi_p2.png)

|設定|意味|
|:--|:---|
|読み上げる内容|何を読み上げさせるか指示します|
|通信方式|HTTPかTCPを選べます。HTTPのほうが安定している報告が多いです|
|ポート|棒読みちゃんの通信ポートを指定します|
|音声ID|使う声の種類を指定します|
|音量|音量を指定します。-1を指定すると棒読みちゃんの設定を優先します|
|話速|速さを指定します。-1を指定すると棒読みちゃんの設定を優先します|
|トーン|トーンを指定します。-1を指定すると棒読みちゃんの設定を優先します|
|ディレイ|どれぐらい遅らせて話始めるかを指定します|
|ひらがなベースで読み上げ|・IME辞書をつかって漢字をすべてひらがなに変換して渡します。<br>・UDトーク併用時は認識時のひらがなに直します|

## 使うとき

1. 棒読みちゃんを立ち上げます。
1. ゆかりねっとコネクターNEOで音声認識をしましょう。
1. 文章が確定すると同時に棒読みちゃんで読み上げが行われます。