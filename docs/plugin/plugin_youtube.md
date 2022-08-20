!!! Info "前提条件"
    * Google アカウントが必要です。

## このプラグインで出来ること

* YouTube Live配信に字幕を送付できます

!!! Warning "字幕送付について"
    * Google社から開示されている資料に基づいて作成してはいますが、不安定です
    * 特に、配信遅延などをつけている場合にうまく表示されないことがあります
    * [OBS連携](plugin_OBS5.md)にある 608/607送信の方が安定することがあります

##　有効化

![twitch](images/plugin_youtube_p1.png)

* プラグインを使うチェックをONにしてください。

## 設定

![twitch](images/plugin_youtube_p2.png)

|設定|意味|
|:--|:---|
|Youtube Live字幕URL|Youtube Liveで提供されるURLをいれます|
|送信する字幕|送信する言語を決めます|
|送信時間の調整|送付時間の調整をします|

!!! Info "送信時間の調整"
    * 現在時刻と送付字幕の時刻差が大きい場合、YouTube側が字幕を受諾しません。
    * そういう場合は字幕の時間を調整し、受諾する範囲を探してください。

!!! Info "YouTubeでのURL取得"
    * ライブ配信設定画面の字幕設定を調整することで得られます
    ![twitch](images/plugin_youtube_p3.png)
