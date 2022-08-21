!!! Info "前提条件"
    * [VRChat](https://vrchat.com/home/)が動作することが必要です
    * この機能単品では機能しません。ワールドかアバターにギミックが必要です。

## このプラグインで出来ること

* VRChat内に信号を出すことができます。

##　有効化

![VRChat](images/plugin_vrchat_osc_p1.png)

* プラグインを使うチェックをONにしてください。

## 設定

![VRChat](images/plugin_vrchat_osc_p2.png)

|設定|意味|
|:--|:---|
|Port|VRChat→NEO OSCポートの番号を指定します。デフォルトは　``9001`` です。|
|Address|NEO→VRCha OSC送付先アドレスを指定します。デフォルトは　``127.0.0.1`` です。|
|Port|NEO→VRChat OSCポートの番号を指定します。デフォルトは　``9000`` です。|
|Native Language|母国語を送ります|
|Translation Language|翻訳文を送ります|
|SendType(int)|文字列を数字(アスキーコード)として送ります|
|ルール|音声認識文に特定の文字列を含む場合は、指定したアドレスにデータを送ります|


!!! Info "パラメータの記述"
    * Boolean型でデータを送る場合は、``false`` ``true`` で記述します
    * 配列で数字を送る場合は　``0x00 0x01`` のようにスペース区切りで記述します
    * 浮動小数点で送付する場合は ``1.0`` のように小数で記述します

!!! Info "字幕の送付"
    * データは ``/YNC/Text/ja/Int`` や ``/YNC/Text/ja/String`` のようなアドレスに送られます。
    * VRChatであれば Stringが受け付けられないので、Intを使うことになります
    * Int の場合は、UTF-8のバイトコードが１文字ずつ送付され、0x00 で終端します。

## 使い方
1. VRChatを起動します
2. Openをおして通信を開始します



