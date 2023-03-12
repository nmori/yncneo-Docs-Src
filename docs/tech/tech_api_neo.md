# NEO実装APIについて

!!! Info "内容について"
    この内容はサービス改良の中で予告なく改定されることがあります

!!! Tech "通信先"
    * ゆかりねっとコネクターNEOのWebポートに送付してください。デフォルトは ``15520`` です。

## 入力の受付

* 外部ツールから指定された文字を文字入力として受け付けます。

!!! Tech "使用条件"
    * 特になし

* 送付方式：GET
* 送付先 : /api/input

=== "Query"
    ``` js
    {
        http://localhost:15520/api/input?text=あいうえお
    }
    ```

* 成功すると ok が返ってきます。

## 入力の受付(拡張)

* 外部ツールから指定された文字を文字入力として受け付けます。

!!! Tech "使用条件"
    * ゆかりねっとコネクターNEO v2.0.104～

* 送付方式：POST
* 送付先 : /api/input

|パラメータ     |値                    |例                    |
|---------------|----------------------|----------------------|
|ignorePlugin   |実行しないプラグインID|Plugin_GPT3           |
|Text           |文章                  |おはよう!天気がいいね |
|UserID         |ユーザID              | 0001-002-0003-00005  |
|TalkerName     |ユーザ名              | さいとう             |

=== "Query"
    ``` js
    {
        http://localhost:15520/api/input
    }
    ```
=== "Body"
    ``` json
    {
        "ignorePlugin":
        [
            "Plugin_GPT3"
        ],
        "Text":"おはよう!天気がいいね"
    }
    ```

* 成功すると ok が返ってきます。
* ユーザ名を設定するときには UserIDも指定してください。
* UserIDは、ユーザを識別するものなので、ユーザに対して一意となるものにしてください。(一般的には配信サイトから提供されるユニークなユーザIDなどを使います)
* ingorePlugin は、実行しないプラグインを指定できます。（なお、
プラグイン名は大文字・小文字を区別する点に注意してください)

## 認識のミュート

* すべての入力をシャットアウトします

!!! Tech "使用条件"
    * 特になし

* 送付方式：GET
* 送付先 : /api/mute-**

=== "Mute On"
    ``` js
        http://localhost:15520/api/mute-on
    ```
=== "Mute off"
    ``` js
        http://localhost:15520/api/mute-off
    ```

* 成功すると ok が返ってきます。

## 母国語設定の変更

* 指定した言語に母国語設定を変更します

!!! Tech "使用条件"
    * ゆかりねっとコネクターNEO v2.0以上

* 送付方式：GET
* 送付先 : /api/setRecognitionParam

|クエリ|意味|例|
|:----|:---|:--|
|language|言語名（ISO表記)|ja|

=== "Query"
    ``` js
        http://localhost:15520/api/setRecognitionParam?language=ja
    ```

* 選択・認知可能な言語であれば変更を反映します


## 翻訳表示設定の変更

* 翻訳字幕表示設定を変更します

!!! Tech "使用条件"
    * ゆかりねっとコネクターNEO v2.0以上
* 送付方式：GET
* 送付先 : /api/setTranslationParam

|クエリ|意味|例|
|:----|:---|:--|
|slot|翻訳ナンバー|1~4|
|language|言語名（ISO表記)|ja|
|engine|翻訳エンジン設定|`google`,`microsoft`,`deeplpro`,`deeplfree`,`amazon`,`amazon-eu`,`googletrans`,`watson`,`Papago`,`papago-app`,`share`,`gas`,`off`|

=== "Query"
    ``` js
        http://localhost:15520/api/setTranslationParam?slot=1&language=en&engine=deeplpro
    ```

* 選択・認知可能な言語であれば変更を反映します

## プラグインコマンド

* プラグイン特有のコマンドを送付します

!!! Tech "使用条件"
    * プラグイン自体が対応していること
* 送付方式：GET
* 送付先 : /api/command

|クエリ|意味|例|
|:----|:---|:--|
|target|送付先プラグイン識別名||
|command|命令文字列||


* 成功すると ok が返ってきます。

## NEOとの通信APIポートを特定

* ポートナンバーはレジストリから取得できます

!!! Tech "使用条件"
    * ポートを開放したときに更新されます

* レジストリ位置：HKCU\Software\YukarinetteConnectorNeo\

|名前|型|意味|
|:--|:--|:--|
|WebSocket|DWord32|WebSocketポート番号|
|HTTP|DWord32|HTTPポート番号|

## 発話の受信(WebSocket)

* 表示用のデータをJSONとして受け取れます。

!!! Tech "使用条件"
    * 特になし

* 送付方式：Websocket Text
* 送付先 :　ws://127.0.0.1:50000/ 
* ポート番号は前述のレジストリから取得してください

!!! Warning "パラメータについて"
    * ゆかりねっとコネクター開発時から拡張してきたこともあり、中身が整理されてません。
    * でも、いますぐ使いたいという声もあるので、触りたい方はつかってみてください
    * リファクタリングが進んだ暁には、このフォーマットは使わなくなるかもしれません

=== "Query"
    ``` js
        
            {
                "VoiceText": "12", 
                "UpdateTranslation": false, //翻訳が更新されるとtrueになる
                "ShowCaptionMode": 0,//途中経過を表示しない設定なら1
                "Text1": "", //母国語(ユーザが上に表示すると指示するとこちらに入る)
                "Text6": "", //母国語(ユーザが下に表示すると指示するとこちらに入る)
                "Text1HTML": "",//母国語（ルビをHTML展開したもの）
                "Text6HTML": "",//母国語（ルビをHTML展開したもの）
                "Text1Clop": "",//母国語（ユーザが文字を切るよう指示した結果）
                "Text6Clop": "",//母国語（ユーザが文字を切るよう指示した結果）
                "Lang1": "", //言語名
                "Lang2": "en",//言語名（翻訳1）
                "Lang3": "",//言語名（翻訳2）
                "Lang4": "",//言語名（翻訳3）
                "Lang5": "",//言語名（翻訳4）
                "Lang6": "",//言語名
                "KeepTime": 3.4260476667501467, //ユーザが指示した表示を維持する時間の指示
                "SettingUpdate": 4829,//設定の更新次数。数字がUPしたら、ユーザが何か設定をかえた
                "LimitLine0": true,
                "LimitLine1": false,
                "LimitLine2": false,
                "ShowLangName": true, // ユーザが言語名表示を指示したらtrue
                "MsgID": "f4ad2560-11c0-494f-be04-5734bec5ea41", //文章に任意につくID
                "isDeleted": false,//この文章が消去されているものならtrue。trueになったら表示せず消すこと
                "InsertID": "",//前後関係を表すID。ここに指示されたIDの次に続く文章
                "Alignment": "center",//文章の配置。left,center,right
                "AuthorName": "nao",
                "talkerID": "8141cf31-1685-4e88-97ce-9ae92981174b",//発話者に任意につくID
                "talkerName": "nao",//発話者名
                "BACKGROUND": "#00FF00FF",
                "FOREGROUND": "#FFFFFFFF",
                "DIVIDECOLOR": "#00FF00FF",
                "LINECOLOR": "#00FF00FF",
                "LINEWIDTH": 5.4123840909144327,
                "LINEADVHEIGHT": 1.8,
                "LINEHEIGHT": -0.5,
                "LINESPACE": -0.1,
                "WINDOWFRAMEHEIGHT": 181.0,
                "LINENUM": 2.2,
                "WSPORT": 55501,
                "Direction1": "ltr",
                "Direction2": "ltr",
                "Direction3": "ltr",
                "Direction4": "ltr",
                "Direction5": "ltr",
                "Direction6": "ltr",
                "FONT1NAME": "ＭＳ ゴシック",
                "FONT2NAME": "ＭＳ ゴシック",
                "FONT1SIZE": 70.9823527803947,
                "FONT2SIZE": 42.594463711823266,
                "FONT_M1_SIZE": 70.9823527803947,
                "FONT_M2_SIZE": 42.594463711823266,
                "FONT_M3_SIZE": 25.478836014663941,
                "FONT_M4_SIZE": 13.736800910932674,
                "FONT_M5_SIZE": 10.0,
                "FONT_M6_SIZE": 70.9823527803947,
                "FONT_M1_NAME": "ＭＳ ゴシック",
                "FONT_M2_NAME": "ＭＳ ゴシック",
                "FONT_M3_NAME": "ＭＳ ゴシック",
                "FONT_M4_NAME": "",
                "FONT_M5_NAME": "",
                "FONT_M6_NAME": "ＭＳ ゴシック",
                "Alignment1": "center",
                "Alignment2": "left",
                "Alignment3": "left",
                "Alignment4": "left",
                "TextFixed": false,
                "WINDOW_WIDTH_M": 800,
                "WINDOW_HEIGHT_M": 400,
                "WINDOW_LOCK_M": false,
                "FORECOLOR_M2_L0": "#FFFFFFFF",
                "FORECOLOR_M2_L1": "#FFFFFFFF",
                "FORECOLOR_M2_L2": "#FFFFFFFF",
                "FORECOLOR_M2_L3": "#FFFFFFFF",
                "FORECOLOR_M2_L4": "#FFFFFFFF",
                "LINECOLOR_M2_L0": "#FF2600FF",
                "LINECOLOR_M2_L1": "#FF2600FF",
                "LINECOLOR_M2_L2": "#FF2600FF",
                "LINECOLOR_M2_L3": "#FF2600FF",
                "LINECOLOR_M2_L4": "#FF2600FF",
                "BACKCOLOR_M0": "#00FF00FF",
                "BACKCOLOR_M1": "#00FFFFFF",
                "BACKCOLOR_M2": "#00FF00FF",
                "FORECOLOR_M0": "#00FF00FF",
                "FORECOLOR_M1": "#FFFFFFFF",
                "FORECOLOR_M2": "#FFFFFFFF",
                "LINECOLOR_M1": "#FF2600FF",
                "LINECOLOR_M2": "#FF2600FF",
                "LINEWIDTH_M1": 5.4123840909144327,
                "LINEWIDTH_M2": 5.4123840909144327,
                "AlreadyShown": false,
                "Neo.WebSocket": "55501",
                "Neo.HTTP": "15520",
                "Plugin_OCTemplateGen.Port.WebSocket": "54000",
                "Plugin_PlayVoice.VoiceList": "[\"つくよみちゃん-れいせい/COEIROINK\",\"MANA-のーまる/COEIROINK\",\"おふとんP-のーまる/COEIROINK\",\"ディアちゃん-のーまる/COEIROINK\",\"アルマちゃん-のーまる/COEIROINK\",\"つくよみちゃん-おしとやか/COEIROINK\",\"つくよみちゃん-げんき/COEIROINK\",\"れみ♀-キュート/LMROID\"
                ]",
                "Plugin_TransSrv.Port.HTTP": "8080",
                "Plugin_TransSrv.Port.WebSocket": "52000"
        }
    ```
    
## 発話の受信(WebSocket,シンプル)

* 表示用のデータをJSONとして受け取れます。

!!! Tech "使用条件"
    * ゆかりねっとコネクターNEO v2.0～

* 送付方式：Websocket Text
* 送付先 :　ws://127.0.0.1:50000/text
* ポート番号は前述のレジストリから取得してください

!!! Info "パラメータについて"
    * 前述のAPIと異なり、内容がかなり絞られています

=== "Query"
    ``` js
        {
        "textList": {
            "ja": "今日はよい天気です",
            "en": "Good weather today"
        },
        "fixedText": true,
        "talkerID": "8141cf31-1685-4e88-97ce-9ae92981174b",
        "talkerName": "なお",
        "MessageID": "f72e0ee4-a8f1-4bfa-8a0c-773d348b8375",
        "isAlreadyShown": false,
        "isDeleted": false
        }
    ```
=== "意味"
    |タグ|内容|
    |----|---|
    |textList|発話もしくは翻訳文のリスト（keyは言語名、dataは文章)|
    |fixedText|文章が確定したか|
    |talkerID|発話者のユニークなID|
    |talkerName|発話者名|
    |MessageID|この発話に対するユニークなID|
    |isAlreadyShown|既に表示(確定）されたことがあるか|
    |isDeleted|文章が取り消されているか|
=== "特性"
    * 途中経過を送るかどうかは、見た目の微調整にある「過程を送る」に左右されます。
    * 未確定の状態（発話途中）はfixedText=falseで送られます
    * 確定した場合、まず母国語が確定した時点で一度送付されます。この時点ではほかの翻訳文は空欄です。
    * その後、翻訳が確定したら、その文が送付されます。
    * 翻訳はエンジンや設定によって並列処理しているので何度か通知が来ます。
    * 基本的にはMessageIDで文章を個体識別し、最新の文章を採用してください。
    * 編集者により文が取り消された場合、isDeleted=trueとなります。

## 発話の受信(WebSocket,文のみ)

* 表示用のデータをテキストとして受け取れます。

!!! Tech "使用条件"
    * ゆかりねっとコネクターNEO v2.0.99～

* 送付方式：Websocket Text
* 送付先 :　ws://127.0.0.1:50000/textonly
* ポート番号は前述のレジストリから取得してください

!!! Info "パラメータについて"
    * 文のみです

=== "Query"

    ``` js
        今日はよい天気です
    ```
=== "特性"

    * 文しかきません。
    * アップデートされた分や削除された分は届きません。
