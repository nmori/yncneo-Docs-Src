## 攻略チートシートについて

* このチートシートはテーマを絞ってガイドする「攻略本」的なものです。

## SteamDeckで制御する
!!! Info "前提条件"
    * SteamDeckを導入している
    * 連携のためのツールを入れている


## 1.認識のON/OFFを操作する

* まずは、ゆかりねっとコネクターでURLを確認します。

![Image title](images/cs_colab_deck_p3.png)

|音声認識結果|URL|
|:----------|:--|
|受け取る	 |http://127.0.0.1:15520/api/mute-off|
|受け取らない| http://127.0.0.1:15520/api/mute-on|

!!! Tips "制御用のアドレスについて"
    * パソコンで起動しているアプリが占有しているなどで使えない場合は番号が変わるときがあります。
    * うまく動かないときは、番号を確認してください。

* アドレスをSteamDeckに設定します。

![Image title](images/cs_colab_deck_p1.png)
![Image title](images/cs_colab_deck_p2.png)

!!! Notice "動作確認について"
    * うまく設定できていれば、指示を出したときゆかりねっとコネクターNEO上部のマイクの色が変わります。
