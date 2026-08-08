# NEO実装APIについて

!!! Info "内容について"
    この内容はサービス改良の中で予告なく改定されることがあります

ゆかコネNEOは、本体の中にWebサーバとWebSocketサーバを持っています。外部のツールから、字幕の受信や設定変更ができます。

## 通信ポートについて

!!! Warning "ポート番号は固定ではありません"
    ゆかコネNEOは、起動時に**使えるポートを自動的に探します**。ほかのソフトがポートを使っていた場合は、別のポートに変わります。
    **実際に使われているポート番号は、必ずレジストリから取得してください。**

* レジストリ位置：``HKCU\Software\YukarinetteConnectorNeo\``

|名前|型|意味|
|:--|:--|:--|
|HTTP|DWord32|HTTPポート番号|
|WebSocket|DWord32|WebSocketポート番号|
|LayoutDir|String|字幕テンプレートが置かれているフォルダ|

* ポートを開放したときに更新されます。

|項目|既定のポート番号|
|:--|:--|
|HTTP|``11900``|
|WebSocket|``11901``|

* 「ネットワークの設定」画面の「使える通信ポートを自動で選びます」をOFFにすると、``11900`` / ``11901`` に固定されます。

!!! Info "このページの例について"
    このページのURLの例では ``11900`` / ``11901`` を使っていますが、**あくまで例**です。お使いの環境では別の番号になっていることがあります。

!!! Info "以前から使っている環境について"
    * ポート番号はレジストリに記録され、次の起動でも引き継がれます。そのため、以前から使っている環境では ``15520`` などの別の番号になっていることがあります。
    * それは正常です。番号を ``11900`` に直す必要はありません。レジストリから読んだ値をそのまま使ってください。

!!! Tip "プラグインのポートについて"
    「翻訳・発話連携」プラグインは、本体とは別のポートを持っています。そちらはサブキー ``HKCU\Software\YukarinetteConnectorNeo\TransServer\`` の ``HTTP`` / ``WebSocket`` を参照してください。詳しくは [プラグイン系API](tech_api_plugin.md) をご覧ください。

## アクセス制御について

!!! Warning "認証はありません"
    ゆかコネNEOのAPIには、**パスワードやトークンによる認証はありません**。接続元のIPアドレスだけで判断しています。

* 既定では、**同じパソコンの中からしか接続できません**（``127.0.0.1`` のみで待ち受けます）。
* 「ネットワークの設定」画面の「すべてのIPアドレスを有効にする」をONにし、**かつ管理者としてゆかコネNEOを起動した場合のみ**、ほかの端末から接続できるようになります。
* ほかの端末から接続できる状態のとき、受け付けられるのは次のものだけです。
    * 同じパソコン（ループバック）
    * プライベートIPアドレス（``10.``／``192.168.``／``172.16``～``172.31`` で始まるもの）
    * 「ネットワークの設定」画面の**Web許可ホスト**に書いたアドレス（改行区切り。前方一致）
* 上記以外からのアクセスは、HTTPなら ``403 - Forbidden``、WebSocketなら接続が切られます。

!!! Info "ブラウザから呼び出す場合（CORS）"
    * すべての応答に ``Access-Control-Allow-Origin`` ／ ``Access-Control-Allow-Methods: GET, POST, OPTIONS`` ／ ``Access-Control-Allow-Headers: Content-Type`` が付きます。
    * ``localhost`` ／ ``127.0.0.1`` ／ ``[::1]`` から呼び出した場合と、Web許可ホストに一致した場合は、そのオリジンを許可します。それ以外は ``*`` になります。

!!! Warning "共有ネットワークでの利用について"
    認証がないため、「すべてのIPアドレスを有効にする」をONにすると、**同じネットワークにいる誰でもAPIを呼び出せます**。ネットカフェや共有Wi-Fiなど、信頼できないネットワークではONにしないでください。

## 入力の受付

* 外部ツールから指定された文字を文字入力として受け付けます。

!!! Tech "使用条件"
    * 特になし

* 送付方式：GET
* 送付先 : /api/input

|クエリ|意味|例|
|:----|:---|:--|
|text|文章|あいうえお|
|fixedText|確定したか（省略時は ``true``）|true / false|
|textID|テキスト固有ID（省略時は自動生成）|4C6E8172-2048-4995-BF36-3893EF31FA67|
|name|**ユーザ名を使うためのスイッチ**|（後述）|
|UserID|ユーザID|0001-002-0003-00005|
|TalkerName|ユーザ名|さいとう|
|owner|発話の由来名（省略時は ``API``）|MyTool|

=== "Query"
    ``` js
    {
        http://localhost:11900/api/input?text=あいうえお
    }
    ```
=== "Query（名前つき）"
    ``` js
    {
        http://localhost:11900/api/input?text=あいうえお&name=&UserID=0001-002&TalkerName=さいとう
    }
    ```

* 成功すると ok が返ってきます。

!!! Warning "name を付けないと名前が反映されません"
    * ``UserID`` と ``TalkerName`` は、**クエリに ``name`` というキーが含まれているときだけ**読み取られます。
    * ``name`` の値は使われません。``name=`` のように空でもかまいません。「名前を使う」というスイッチとして働きます。
    * ``name`` を書き忘れると、``UserID`` と ``TalkerName`` は無視されて名前が付きません。

## 入力の受付(拡張)

* 外部ツールから指定された文字を文字入力として受け付けます。

!!! Tech "使用条件"
    * ゆかコネNEO v2.0.104～

* 送付方式：POST
* 送付先 : /api/input

|パラメータ     |値                    |例                    |
|---------------|----------------------|----------------------|
|ignorePlugin   |実行しないプラグインID（**JSON配列で指定**）|["Plugin_GPT3"]|
|Text           |文章                  |おはよう!天気がいいね |
|UserID         |ユーザID              | 0001-002-0003-00005  |
|TalkerName     |ユーザ名              | さいとう             |
|ServiceName   |発話の由来名（省略時は ``API``）|MyTool|
|fixedText     |確定したか (v2.3.104～)              | true             |
|textID        |テキスト固有ID (v2.3.104～)              |    4C6E8172-2048-4995-BF36-3893EF31FA67         |
=== "Query"
    ``` js
    {
        http://localhost:11900/api/input
    }
    ```
=== "Body"
    ``` json
    {
        "ignorePlugin":
        [
            "Plugin_GPT3"
        ],
        "Text":"おはよう!天気がいいね",
        "fixedText": true,
        "textID": "4C6E8172-2048-4995-BF36-3893EF31FA67",
        "UserID": "0001-002-0003-00005",
        "TalkerName": "さいとう",
        "ServiceName": "MyTool"
    }
    ```

* 成功すると ok が返ってきます。
* ユーザ名を設定するときには UserIDも指定してください。**UserIDが無い場合、TalkerNameは無視されます。**
* UserIDは、ユーザを識別するものなので、ユーザに対して一意となるものにしてください。(一般的には配信サイトから提供されるユニークなユーザIDなどを使います)
* ingorePlugin は、実行しないプラグインを指定できます。（なお、
プラグイン名は大文字・小文字を区別する点に注意してください)
* 途中経過を送る場合には、fixedTextを使います。最初はfalse で経過を送り、最後に確定として True を送ります。IDごとに、かならず 最後にtrueが送られるようにしましょう。

!!! Warning "ignorePlugin は配列で指定してください"
    ``"ignorePlugin": "Plugin_GPT3"`` のように文字列を直接書くとエラーになります。1つだけ指定する場合も ``["Plugin_GPT3"]`` と書いてください。

## 認識のミュート

* すべての入力をシャットアウトします

!!! Tech "使用条件"
    * 特になし

* 送付方式：GET
* 送付先 : /api/mute-**

=== "Mute On"
    ``` js
        http://localhost:11900/api/mute-on
    ```
=== "Mute off"
    ``` js
        http://localhost:11900/api/mute-off
    ```

* 状態が変わったときは ok が返ってきます。
* **すでにその状態だった場合は stay が返ってきます。**（エラーではありません）

## ミュート状態の取得

* いまミュート中かどうかを確認します。

!!! Tech "使用条件"
    * 特になし

* 送付方式：GET
* 送付先 : /api/mute-status

=== "Query"
    ``` js
        http://localhost:11900/api/mute-status
    ```

* ミュート中なら ``true``、そうでなければ ``false`` が返ってきます。
* StreamDeckなどで、ボタンの点灯状態をゆかコネNEOに合わせたいときに使います。

## 母国語設定の変更

* 指定した言語に母国語設定を変更します

!!! Tech "使用条件"
    * ゆかコネNEO v2.0以上

* 送付方式：GET
* 送付先 : /api/setRecognitionParam

|クエリ|意味|例|
|:----|:---|:--|
|language|言語名（ISO表記)|ja|

=== "Query"
    ``` js
        http://localhost:11900/api/setRecognitionParam?language=ja
    ```

* 選択・認知可能な言語であれば変更を反映します
* **``language`` は必須です。** 省略した場合や、知らない言語名を指定した場合は、何も起きません（設定は変わりません）。
* 言語名は ``ja`` のようなISO表記のほか、``JA`` のような大文字の短縮形も受け付けます。

## 認識言語スロットの切替

* ブラウザ音声認識の画面で選べる「認識する言語」を、1～3番目のどれにするか切り替えます。

!!! Tech "使用条件"
    * ブラウザ音声認識（Chrome / Edge）を使用中であること
    * 音声認識ウィンドウが開いていること

* 送付方式：GET
* 送付先 : /api/setRecognitionMode

|クエリ|意味|例|
|:----|:---|:--|
|number|認識言語の番号（1～3）|2|

=== "Query"
    ``` js
        http://localhost:11900/api/setRecognitionMode?number=2
    ```

!!! Info "母国語の変更とは別物です"
    * こちらは**音声認識ウィンドウの言語プルダウンを切り替える**機能です。
    * 母国語そのものを変えたい場合は ``/api/setRecognitionParam`` を使ってください。
    * ブラウザ音声認識以外（オフライン認識・UDトークなど）を使っているときは効きません。

## 翻訳表示設定の変更

* 翻訳字幕表示設定を変更します

!!! Tech "使用条件"
    * ゆかコネNEO v2.0以上

* 送付方式：GET
* 送付先 : /api/setTranslationParam

|クエリ|意味|例|
|:----|:---|:--|
|slot|翻訳ナンバー|1~4|
|language|言語名（ISO表記）|下表を参照|
|engine|翻訳エンジン設定|下表を参照|

=== "Query"
    ``` js
        http://localhost:11900/api/setTranslationParam?slot=1&language=en&engine=deeplpro
    ```

* 選択・認知可能な言語であれば変更を反映します

### language に指定できる特別な値

|`language`|意味|
|:--|:--|
|`ja` `en` `zh-TW` …|その言語に翻訳します（ISO表記）|
|`off`|この枠を使わない（翻訳しない）|
|`none`|`off` と同じです|
|`native`|翻訳せず、母国語をそのまま表示します|

### engine に指定できる値

|`engine`|ID|翻訳エンジン|状態|備考|
|:--|:--|:--|:--|:--|
|`google`|0|Google 翻訳v2(支援①～)|利用可||
|`microsoft`|1|Microsoft翻訳システム(支援①～)|利用可||
|`deeplpro`|2|DeepL API Pro翻訳エンジン(支援③～)|利用可||
|`deeplfree`|3|DeepL API Free翻訳エンジン(個人でKey取得)|利用可||
|`amazon`|4|Amazon 翻訳システム(Asia向け/支援③～)|利用可||
|`amazon-eu`|5|Amazon 翻訳システム(EU圏向け/支援③～)|利用可||
|`googletrans`|6|—|廃止|v2.3.128でエンジン一覧から削除しました。指定しても選択は変わりません|
|`watson`|7|—|廃止|v2.3.128でエンジン一覧から削除しました。指定しても選択は変わりません|
|`papago`|8|NAVER Papago 翻訳システム(支援③～)|利用可||
|`papago-app`|9|NAVER Papago 翻訳システム(個人キー)|利用可||
|`share`|10|共用翻訳(m2m100/無料)|利用可||
|`gas`|11|Google Apps Script 翻訳（個人で用意）|利用可||
|`googlev3`|12|Google 翻訳V3 (支援③～)|利用可||
|`gpt4.1`|13|OpenAI GPT4.1 API翻訳(支援③～/β)|利用可||
|`tencent`|14|Tencent Cloud Translator(個人キー)|利用可||
|`baidu`|15|Baidu(百度)Translator (個人キー)|利用可||
|`roman`|16|Microsoftローマ字変換（支援①～)|利用可||
|`alibaba`|17|Alibaba クラウド翻訳(個人キー)|利用可||
|—|18|共用翻訳(Algos/より良い翻訳/支援①～)|**APIからは指定できません**|アプリの一覧には表示されます|
|`gpt4.1mini`|19|OpenAI GPT-4.1-mini(支援③～/β)|利用可||
|`gpt4.1nano`|20|OpenAI GPT-4.1-nano(支援③～/β)|利用可||
|`gemini25flash`|21|Google Gemini 2.5 flash Lite API翻訳(個人キー)|利用可|使うモデルは 2.5 Flash Lite に固定されます|
|`gemini25pro`|22|Google Gemini API翻訳(個人キー)|利用可|使うモデルは「翻訳（API、設定）」画面の MODEL で決まります。値の名前は ``pro`` ですが、選んだモデルがそのまま使われます|
|`claude`|23|Anthropic Claude （個人キー)|利用可||
|`openrouter`|24|OpenRouter API (個人キー)|利用可||
|`grok`|25|Grok AI 翻訳(個人キー)|利用可||
|`custom`|26|ローカル翻訳（個人API）|利用可||
|—|27|ブラウザ翻訳（β/Free）|**APIからは指定できません**|アプリの一覧には表示されます|
|`off`|28|OFF（翻訳しない）|利用可||
|`parapper`|29|Parapper翻訳|利用可|v2.3.128～|

!!! Info "この表の基準"
    * ゆかコネNEO **v2.3.128** 時点の一覧です。
    * 値は **大文字・小文字を区別します**。``Papago`` は無効で、``papago`` が正しい表記です。
    * 一覧にない文字列を指定した場合、翻訳エンジンの選択は変更されません。
    * ID18 と ID27 は、アプリの一覧には出てきますが**APIから指定する値が用意されていません**。この2つに切り替えたい場合は画面から操作してください。

!!! Warning "値の変更履歴"
    * v2.3.128：``gemini15flash`` → ``gemini25flash``、``gemini15pro`` → ``gemini25pro`` に改名しました（旧名は使えません）
    * v2.3.128：``parapper`` を追加しました
    * v2.3.128：``googletrans`` ``watson`` を廃止しました

## 設定の変更

* 設定項目を外部から書き換えます。

!!! Tech "使用条件"
    * ``Parapper_TransPort`` の対応は ゆかコネNEO v2.3.128～

* 送付方式：POST（``Content-Type: application/json``）
* 送付先 : /api/setconfig

|キー|型|意味|
|:--|:--|:--|
|NativeLanguage|int|母国語の選択番号|
|TranslateLanguage1 ～ TranslateLanguage4|string|翻訳先の言語名|
|Translator1String ～ Translator5String|string|翻訳エンジンの表示名|
|KeepTime|double|字幕の保持時間（秒）|
|ScrollTime|double|スクロール速度|
|Parapper_TransPort|int|Parapper翻訳の接続先ポート（1～65535）|

=== "Query"
    ``` js
        POST http://localhost:11900/api/setconfig
    ```
=== "Body"
    ``` json
    {
        "YNC-NEO": {
            "Parapper_TransPort": 18081
        }
    }
    ```

* 受け付けると ``200`` が返ります。
* ``OPTIONS`` は ``204`` を返します（ブラウザから呼び出すときの事前確認用）。
* ``POST`` ``OPTIONS`` 以外のメソッド、JSONとして解釈できない本文は ``400`` を返します。
* 一覧にないキーは無視されます。エラーにはなりません。

!!! Warning "200は「反映が終わった」という意味ではありません"
    * 設定の反映は、受け付けたあとに非同期で行われます。
    * ``/api/setconfig`` を送った直後に ``/api/setTranslationParam`` などを送ると、反映の順序が入れ替わることがあります。続けて送る場合は少し間隔をあけてください。
    * 同じことは ``/api/setRecognitionParam`` ``/api/setRecognitionMode`` ``/api/setTranslationParam`` にもあてはまります。

!!! Warning "ステータスコードで成否を判断しないでください"
    * 設定変更系のAPIは、処理が終わる前に応答を返します。そのため、**``200`` が返っても指定した値が反映されていないことがあります**（たとえば ``language`` だけ有効で ``engine`` の指定が無効だった場合など）。
    * 反映されたかどうかを確かめたい場合は、``/api/getlayoutdata`` で現在の設定を読み直してください。

!!! Info "扱えるキーについて"
    * ここに載せているキーだけが動作を保証している範囲です。
    * 本文の ``"YNC-NEO"`` は省略して ``{"Parapper_TransPort": 18081}`` と書くこともできますが、将来の互換性のため付けることを推奨します。

## 設定一式の取得

* 現在の設定をまとめてJSONで取得します。

!!! Tech "使用条件"
    * 特になし

* 送付方式：GET
* 送付先 : /api/getlayoutdata

=== "Query"
    ``` js
        http://localhost:11900/api/getlayoutdata
    ```

* 言語・翻訳エンジン・フォント・色・保持時間・レイアウトなど、設定一式がJSONで返ります。
* 外部ツールで設定のバックアップを取ったり、いまの状態を確認したりするのに使えます。

## 設定一式の復元

* ``/api/getlayoutdata`` で取得したJSONを送り返して、設定を復元します。

!!! Tech "使用条件"
    * 特になし

* 送付方式：POST（``Content-Type: application/json``）
* 送付先 : /api/setlayoutdata

=== "Query"
    ``` js
        POST http://localhost:11900/api/setlayoutdata
    ```

* 本文には ``/api/getlayoutdata`` で得たJSONを**そのまま**入れてください。
* ``/api/setconfig`` と違い、``"YNC-NEO"`` で囲む必要はありません。
* 外部ツールで「配信用プリセット」「コラボ用プリセット」を切り替えるような使い方ができます。

!!! Tip "画面から使う場合"
    同じことは「設定保存・復元」画面や、起動オプションの ``/profile=`` でもできます。詳しくは [設定の保存・復元とプロファイル](../startup/startup_profile.md) と [起動オプション](tech_option_neo.md) をご覧ください。

## プラグインコマンド

* プラグイン特有のコマンドを送付します

!!! Tech "使用条件"
    * プラグイン自体が対応していること
    * 対象のプラグインが有効になっていること

* 送付方式：GET
* 送付先 : /api/command

|クエリ|意味|例|
|:----|:---|:--|
|target|送付先プラグイン識別名|Plugin_OBS5|
|command|命令文字列|scene|

* **応答は、プラグインが返した文字列がそのまま返ります。** ``ok`` は返りません。
* 返ってきた内容がJSONとして解釈できる場合は ``Content-Type: application/json``、それ以外はプレーンテキストになります。

|状況|応答|
|:--|:--|
|プラグインが処理した|プラグインが返した文字列|
|プラグインが無効／このコマンドに対応していない|``403``（本文なし）|
|``target`` に一致するプラグインが見つからない|``400``（本文なし）|

* 使えるコマンドの一覧は [プラグイン系API](tech_api_plugin.md) をご覧ください。

## 発話の受信(WebSocket)

* 表示用のデータをJSONとして受け取れます。

!!! Tech "使用条件"
    * 特になし

* 送付方式：Websocket Text
* 送付先 :　ws://127.0.0.1:11901/
* ポート番号は前述のレジストリから取得してください

!!! Warning "パラメータについて"
    * ゆかコネ開発時から拡張してきたこともあり、中身が整理されてません。
    * でも、いますぐ使いたいという声もあるので、触りたい方はつかってみてください
    * リファクタリングが進んだ暁には、このフォーマットは使わなくなるかもしれません

### まず押さえるフィールド

|タグ|内容|
|:--|:--|
|MsgID|この発話につくユニークなID。**これをキーに管理してください**|
|isDeleted|取り消された発話なら ``true``。**このときは表示を消してください**|
|TextFixed|文章が確定したか|
|Text1 / Text6|母国語の文章（``Text1``＝上に表示する設定のとき、``Text6``＝下に表示する設定のとき）|
|**Text2 ～ Text5**|**翻訳文の本体**（翻訳1～翻訳4に対応）|
|Text1HTML ～ Text6HTML|ルビなどをHTMLに展開したもの。表示にはこちらを優先してください|
|Lang1 ～ Lang6|それぞれの言語名。空の枠は使われていません|
|KeepTime|表示を維持する**残り秒数**（後述）|
|SettingUpdate|設定の更新回数。数字が増えたら見た目の設定が変わっています|
|ShowCaptionMode|途中経過を表示しない設定なら ``1``|
|talkerID / talkerName|発話者のIDと名前|
|isOwnersTalkData|自分自身の発話なら ``true``|
|InsertID|前後関係を表すID。このIDの次に続く文章という意味|
|AlreadyShown|すでに表示（確定）されたことがあるか|

### 受け取ったあとの流れ

1. ``isDeleted`` が ``true`` なら、``MsgID`` に対応する字幕を消して**そこで処理を終えます**（見た目の設定を読むより先に行ってください）。
2. ``SettingUpdate`` が前回と変わっていたら、フォント・色などの見た目を更新します。
3. ``MsgID`` をキーに文章を追加・更新します。``TextFixed`` と ``ShowCaptionMode`` で表示するかどうかを決めます。
4. 表示する文章は ``Text1HTML``～``Text6HTML`` を優先して使います。

!!! Warning "KeepTime の意味"
    * ``KeepTime`` は設定値そのものではなく、**このデータを受け取った時点からの残り秒数**です。
    * 確定した字幕は2回届きます（母国語が確定したとき／翻訳が確定したとき）。2回目の ``KeepTime`` は、1回目からの経過時間が差し引かれています。
    * ``0`` 以下（本体は ``-1`` を送ります）の場合は「時間で自動削除しない」という意味です。
    * 実際に消えるタイミングは、``isDeleted`` が ``true`` の別のデータで通知されます。

!!! Info "接続直後に1通届きます"
    * 接続すると必ず1通目が送られてきます。直前の確定した字幕、なければ**本文が空の設定スナップショット**です。
    * 「つないだ直後に空の字幕が来る」のは仕様です。エラーではありません。

!!! Info "取り消し（isDeleted）のときは中身が違います"
    * ``isDeleted`` が ``true`` のときは、見た目の設定を含む全項目ではなく、**必要最小限のフィールドだけ**が届きます（``MsgID`` ``isDeleted`` ``InsertID`` ``talkerID`` ``talkerName`` ``SettingUpdate`` と、空になった ``Lang1``～``Lang6`` ``Text1HTML``～``Text6HTML``）。
    * 見た目の設定を読もうとすると空になっているため、必ず ``isDeleted`` を先に判定してください。

??? note "全フィールドのサンプル（クリックで開きます）"
    ``` js
            {
                "UpdateTranslation": false, //翻訳が更新されるとtrueになる
                "ShowCaptionMode": 0,//途中経過を表示しない設定なら1
                "Text1": "", //母国語(ユーザが上に表示すると指示するとこちらに入る)
                "Text2": "", //翻訳1
                "Text3": "", //翻訳2
                "Text4": "", //翻訳3
                "Text5": "", //翻訳4
                "Text6": "", //母国語(ユーザが下に表示すると指示するとこちらに入る)
                "Text1HTML": "",//母国語（ルビをHTML展開したもの）
                "Text2HTML": "",//翻訳1（同）
                "Text3HTML": "",//翻訳2（同）
                "Text4HTML": "",//翻訳3（同）
                "Text5HTML": "",//翻訳4（同）
                "Text6HTML": "",//母国語（ルビをHTML展開したもの）
                "Text1Clop": "",//母国語（Text1と同じ値が入ります）
                "Text2Clop": "",//翻訳1（Text2と同じ値が入ります）
                "Text3Clop": "",//翻訳2（同）
                "Text4Clop": "",//翻訳3（同）
                "Text5Clop": "",//翻訳4（同）
                "Text6Clop": "",//母国語（Text6と同じ値が入ります）
                "Lang1": "", //言語名
                "Lang2": "en",//言語名（翻訳1）
                "Lang3": "",//言語名（翻訳2）
                "Lang4": "",//言語名（翻訳3）
                "Lang5": "",//言語名（翻訳4）
                "Lang6": "",//言語名
                "LanguageNative": "ja",//母国語の言語名
                "KeepTime": 3.4260476667501467, //表示を維持する残り秒数
                "CaptureTimeMs": 1754630000000, //発話をとらえた時刻(UNIX時刻/ミリ秒)
                "SettingUpdate": 4829,//設定の更新次数。数字がUPしたら、ユーザが何か設定をかえた
                "LimitLine0": true,
                "LimitLine1": false,
                "LimitLine2": false,
                "ShowLangName": true, // ユーザが言語名表示を指示したらtrue
                "MsgID": "f4ad2560-11c0-494f-be04-5734bec5ea41", //文章に任意につくID
                "isDeleted": false,//この文章が消去されているものならtrue。trueになったら表示せず消すこと
                "isWaitClearing": false,//保持時間が過ぎるまで表示を切り替えない設定ならtrue
                "isOwnersTalkData": true,//自分自身の発話ならtrue
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
                "LINESTYLE": "",
                "LINEBORDER": "",
                "WINDOWFRAMEHEIGHT": 181.0,
                "LINENUM": 2.2,
                "WSPORT": 11901,
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
                "BackColor": "#00FF00FF",
                "UseBaseColorSetting": false,
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
                "LINECOLOR_M3_L0": "#FF2600FF",
                "LINECOLOR_M3_L1": "#FF2600FF",
                "LINECOLOR_M3_L2": "#FF2600FF",
                "LINECOLOR_M3_L3": "#FF2600FF",
                "LINECOLOR_M3_L4": "#FF2600FF",
                "LINEWIDTH_L0": 5.4,
                "LINEWIDTH_L1": 5.4,
                "LINEWIDTH_L2": 5.4,
                "LINEWIDTH_L3": 5.4,
                "LINEWIDTH_L4": 5.4,
                "LINEWIDTH2_L0": 0.0,
                "LINEWIDTH2_L1": 0.0,
                "LINEWIDTH2_L2": 0.0,
                "LINEWIDTH2_L3": 0.0,
                "LINEWIDTH2_L4": 0.0,
                "BACKCOLOR_M0": "#00FF00FF",
                "BACKCOLOR_M1": "#00FFFFFF",
                "BACKCOLOR_M2": "#00FF00FF",
                "FORECOLOR_M0": "#00FF00FF",
                "FORECOLOR_M1": "#FFFFFFFF",
                "FORECOLOR_M2": "#FFFFFFFF",
                "LINECOLOR_M1": "#FF2600FF",
                "LINECOLOR_M2": "#FF2600FF",
                "LINECOLOR_M3": "#FF2600FF",
                "LINEWIDTH_M1": 5.4123840909144327,
                "LINEWIDTH_M2": 5.4123840909144327,
                "LINEWIDTH_M3": 0.0,
                "AlreadyShown": false,
                "Neo.WebSocket": "11901",
                "Neo.HTTP": "11900",
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
    * ゆかコネNEO v2.0～

* 送付方式：Websocket Text
* 送付先 :　ws://127.0.0.1:11901/text
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
        "isOwnersTalkData": true,
        "isDeleted": false
        }
    ```

=== "意味"
    |タグ|内容|
    |----|---|
    |textList|発話もしくは翻訳文のリスト（keyは言語名、dataは文章）|
    |fixedText|文章が確定したか|
    |talkerID|発話者のユニークなID|
    |talkerName|発話者名|
    |MessageID|この発話に対するユニークなID|
    |isAlreadyShown|既に表示（確定）されたことがあるか|
    |isOwnersTalkData|自分自身の発話か|
    |isDeleted|文章が取り消されているか|

=== "特性"
    * 途中経過を送るかどうかは、見た目の微調整にある「過程を送る」に左右されます。
    * 未確定の状態（発話途中）はfixedText=falseで送られます
    * 確定した場合、まず母国語が確定した時点で一度送付されます。この時点ではほかの翻訳文は空欄です。
    * その後、翻訳が確定したら、その文が送付されます。
    * 翻訳はエンジンや設定によって並列処理しているので何度か通知が来ます。
    * 基本的にはMessageIDで文章を個体識別し、最新の文章を採用してください。
    * 編集者により文が取り消された場合、isDeleted=trueとなります。

!!! Warning "textList はキーの有無が変わります"
    * ``textList`` には、**その時点で確定している言語だけ**が入ります。翻訳がまだ終わっていない言語は、キーそのものが無いか、空文字になります。
    * 「キーが無いから翻訳しない設定なのだ」とは判断しないでください。
    * ``MessageID`` ごとに、届いた最新のデータで全体を置き換えるのが安全です。

## 発話の受信(WebSocket,文のみ)

* 表示用のデータをテキストとして受け取れます。

!!! Tech "使用条件"
    * ゆかコネNEO v2.0.99～

* 送付方式：Websocket Text
* 送付先 :　ws://127.0.0.1:11901/textonly
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

!!! Warning "届く条件が絞られています"
    * 次のすべてを満たしたときだけ送られます。
        * 文章が**確定**している
        * まだ表示されたことがない（再表示ではない）
        * 取り消されていない
        * 翻訳の更新による再送ではない
    * **母国語だけが届きます。翻訳文は届きません。** 翻訳文も欲しい場合は ``/text`` を使ってください。

## 文字を送る(WebSocket)

* 外部の音声認識ツールなどから、認識結果をゆかコネNEOへ流し込めます。

!!! Tech "使用条件"
    * 特になし

* 送付方式：Websocket Text
* 送付先 :　ws://127.0.0.1:11901/

|送る文字列|意味|
|:--|:--|
|``今日はよい天気です``|**確定した**文章として取り込みます|
|``@今日はよい``|先頭に ``@`` を付けると、**未確定（途中経過）**として取り込みます|
|``@$ja``|認識する言語を指定します|
|``@$ja-en``|認識する言語と翻訳先を指定します|

* 空白だけの文字列は取り込まれません。
* HTTPの ``/api/input`` と違い、つなぎっぱなしにして連続で流し込めるので、途中経過を細かく送りたい場合に向いています。

### 2人目の話者として送る

* 送付先 :　ws://127.0.0.1:11901/2nd

|送る文字列|意味|
|:--|:--|
|``$name$なお``|2人目の話者の表示名を設定します|
|``こんにちは``|2人目の話者の発話として取り込みます|

* 1台のパソコンで2人分の字幕を出したいときに使います。

!!! Info "そのほかの接続先"
    ``/speech`` ``/translate`` ``/llm`` は、ゆかコネNEOがブラウザの読み上げ・翻訳・AI機能とやりとりするために使っている接続先です。外部ツールから使うことは想定していません。

## 字幕テンプレートを自作する

* 配信ソフトのブラウザソースで開くURLと、そのオプションについて説明します。

!!! Tech "使用条件"
    * 特になし

### ブラウザソースのURL

```
http://<IPアドレス>:<HTTPポート>/<テンプレートのフォルダ>/<HTMLファイル>?port=<WebSocketポート>
```

* 「レイアウトデザインの選択」画面に表示されているアドレスがこの形です。ダブルクリックでコピーできます。
* 既定のテンプレートは ``MultiLang_R/MultiLang_R.html`` です。
* テンプレートの実体があるフォルダは、レジストリの ``LayoutDir`` から取得できます。「レイアウトデザインの選択」画面の「テンプレフォルダを開く」でも開けます。

### URLに付けられるオプション

|クエリ|意味|
|:--|:--|
|``?port=``|テンプレートが接続するWebSocketポートの指定。通常はゆかコネNEOが自動で付けます|
|``?solo=native``|母国語だけを表示します|
|``?solo=trans1`` ～ ``?solo=trans4``|翻訳1～翻訳4のどれか1つだけを表示します|
|``?view=me`` / ``?view=other``|左右2分割のテンプレート（トークセッション横並び、ゲーム風横ならべなど）で、どちら側を表示するかの指定|

=== "例）翻訳1だけを別のブラウザソースに出す"
    ``` js
        http://localhost:11900/MultiLang_R/MultiLang_R.html?port=11901&solo=trans1
    ```

!!! Tip "言語ごとに別のソースとして取り込む"
    ``?solo=`` を使うと、言語ごとに位置やサイズを別々に調整できます。同じことは「レイアウトデザインの選択」画面の「応用パターン（１言語ごとの取り込み）」からも行えます。

### データの受け取り方

* テンプレートは ``ws://127.0.0.1:<WebSocketポート>/`` に接続して、前述の「発話の受信(WebSocket)」のデータを受け取ります。
* 処理の流れは「受け取ったあとの流れ」の4ステップと同じです。
* ゆかコネNEOは ``port.js`` にポート番号を書き出しているので、テンプレート側からはそれを読み込んで使うこともできます。

!!! Warning "テンプレートの自作はサポート対象外です"
    * 標準のテンプレートを書き換えた場合、アップデートで上書きされることがあります。自作したものは別のフォルダにコピーして使ってください。
    * データの形式は予告なく変わることがあります。
