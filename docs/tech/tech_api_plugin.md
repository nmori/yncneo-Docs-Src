# プラグイン系APIについて

!!! Info "内容について"
    この内容はサービス改良の中で予告なく改定されることがあります

プラグインには、外部から呼び出せる機能を持つものがあります。呼び出し方は大きく2種類あります。

|方式|使うポート|説明|
|:--|:--|:--|
|``/api/command``|**ゆかコネNEO本体**のHTTPポート|本体経由でプラグインに命令を送ります。ほとんどのプラグインはこちらです|
|翻訳・発話連携サーバ|**プラグイン独自**のHTTP/WebSocketポート|翻訳や読み上げを外部ツールから使うための専用サーバです|

## 共通事項

### 通信ポートの特定

!!! Warning "本体のポートとプラグインのポートは別物です"
    ``/api/command`` は**ゆかコネNEO本体**のHTTPポートに送ります。翻訳・発話連携サーバのポートとは別です。混同しやすいので注意してください。

* ``/api/command`` で使うポート（本体）
    * レジストリ位置：``HKCU\Software\YukarinetteConnectorNeo\``
    * ``HTTP``（DWord32）／``WebSocket``（DWord32）
    * 既定は ``11900`` / ``11901``
    * 詳しくは [本体内蔵API](tech_api_neo.md) の「通信ポートについて」をご覧ください
* 翻訳・発話連携サーバのポート
    * レジストリ位置：``HKCU\Software\YukarinetteConnectorNeo\TransServer\``
    * ``HTTP``（DWord32）／``WebSocket``（DWord32）
    * 既定は HTTP ``8080``、WebSocket は ``32000`` 番台の空きポート
    * プラグインの「設定」ボタンを押すと、いま使っているアドレスが表示されます

!!! Tech "使用条件"
    * ポートを開放したときに更新されます

!!! Warning "無効化しても古い値が残ります"
    翻訳・発話連携サーバのレジストリ値は、プラグインを無効にしてもクリアされません。値が書かれていても、プラグインが動いているとは限りません。

!!! Info "このページの例について"
    このページのURLの例では本体のポートを ``11900`` としていますが、**あくまで例**です。実際の値はレジストリから取得してください。

### /api/command の書式と応答

```
http://localhost:11900/api/command?target=<プラグイン識別名>&command=<命令>&<パラメータ>
```

* 送付方式：HTTP(GET)
* ``target`` の大文字・小文字は区別されません。ただし**綴りは正確に**書いてください。
* パラメータ名は、プラグインによって大文字・小文字を区別します。各項の説明に従ってください。
* 値に ``/`` を含める場合は ``%2F`` に置き換えてください。

**応答について**

|状況|応答|
|:--|:--|
|プラグインが処理した|**プラグインが返した文字列がそのまま返ります**|
|プラグインが無効／このコマンドに対応していない|``403``（本文なし）|
|``target`` に一致するプラグインが見つからない|``400``（本文なし）|

!!! Warning "ok は返りません"
    ``/api/command`` は ``ok`` を返しません。返ってくるのはプラグインが用意した文字列で、内容はプラグインごとに違います。JSONとして解釈できる場合は ``Content-Type: application/json``、それ以外はプレーンテキストになります。

## プラグイン別コマンド一覧

対応しているプラグインと命令の一覧です。詳細は各項をご覧ください。

|プラグイン（target）|command|主なパラメータ|できること|
|:--|:--|:--|:--|
|Plugin_PlayVoice|``speech``|Text, Engine ほか|読み上げさせる|
|Plugin_PlayVoice|``set``|engine ほか|読み上げのパラメータを変える|
|Plugin_PlayVoice|``stop``|—|読み上げを止める|
|Plugin_PlayVoice|``device``|—|使える音声の一覧を取得する|
|Plugin_PlayVoice|``exec``|tag|APIタグに登録したパラメータへ切り替える|
|Plugin_InputAssist|``prev`` ``next`` ``send`` ``sendnext``|—|入力支援の行を移動・送信する|
|Plugin_Dictionary|``load``|type, file|辞書を臨時で差し替える|
|Plugin_LyricAssist|``play`` ``pause`` ``stop`` ``load``|file|歌詞表示を操作する|
|Plugin_OBS / Plugin_OBS5|``set``|text, source, sourceNo|OBSのテキストソースに文字を出す|
|Plugin_OBS / Plugin_OBS5|``scene``|scene|OBSのシーンを切り替える|
|Plugin_OBS / Plugin_OBS5|``startreplay`` ``stopreplay``|—|リプレイバッファを開始・停止する|
|Plugin_VRChat_OSC|``exec``|tag|APIタグに登録したOSCを送る|
|Plugin_VRChat_OSC|``send``|address, message|任意のOSCアドレスへ送る|
|Plugin_VRChat_OSC|``chat``|message|VRChatのChatboxへ送る|
|Plugin_VRChat_OSC|``scenario``|action, text|シナリオロールを遠隔操作する|
|Plugin_VCas|``send``|address, message|バーチャルキャストへOSCを送る|
|Plugin_VMC|``send``|address, message|ばもきゃへOSCを送る|
|Plugin_VMC|``send_face``|face, value|ばもきゃの表情を変える|
|Plugin_NeosVR|``exec``|tag|APIタグに登録したメッセージを送る|
|Plugin_NeosVR|``send``|address, message|任意のメッセージを送る|
|Plugin_VtubeStudio|``exec``|tag|APIタグに登録したキーバインドを発火する|
|Plugin_VtubeStudio|``call``|tag|キーバインド名を直接指定して発火する|
|Plugin_HTTPCall|``exec``|tag|APIタグに登録したHTTP呼び出しを送る|
|Plugin_WSCall|``exec``|tag|APIタグに登録したWebSocket呼び出しを送る|
|Plugin_ClusterTrigger|``exec``|tag|APIタグに登録したウェブトリガーを発火する|
|Plugin_Discord|``exec``|text|Discordのテキストチャンネルへ送る|
|Plugin_Discord|``sendvoice``|filename|Discordのボイスチャンネルで音声を再生する|
|Plugin_DiscordWebHook|``exec``|text, ID, talkername|Webhookへ投稿する|
|Plugin_Ruby|``makehiragana``|text|ひらがな読みを作る|
|Plugin_Ruby|``makemorph``|text|形態素解析の結果を得る|
|Plugin_TalkHistory|``gethistory``|limit|会話の記録を取り出す|
|Plugin_TalkHistory|``search``|q|会話の記録を検索する|
|Plugin_TalkHistory|``stats`` ``karte``|—|集計結果を取得する|
|Plugin_TalkHistory|``dashboard``|—|ダッシュボードを作り直してURLを得る|
|Plugin_GPT3|``question`` ``response``|prompt, premise ほか|AIに文章を作らせる|

!!! Info "対応していないプラグイン"
    次のプラグインは ``/api/command`` に対応していません。呼び出しても何も起きず、``403`` が返ります。

    * 直接入力／MIDI入力／ホットキー／Python連携／遅延（DynamicKeepTime）／UDP通信／不適切語の置換

## 読み上げプラグイン

* ゆかコネNEOを通して読み上げ設定のコントロールをサポートします。

!!! Tech "使用条件"
    * 読み上げプラグインをONにしていること

### 発話の停止

* 送付方式：HTTP(GET)

=== "停止指示"
    ```js
        http://localhost:11900/api/command?target=Plugin_PlayVoice&command=stop
    ```

### 発話パラメータの設定

* 送付方式：HTTP(GET)

=== "パラメータ"

    |パラメータ|値    |例          |
    |---------|------|------------|
    |engine   |エンジン名|さとうささら/CeVIO_64|
    |pitch    |高さ    | 1.0 |
    |accent   |抑揚    | 1.0 |
    |speed   |速度    | 1.0 |
    |volume   | 音量  | 1.0 |
    |quality   |声質    | 1.0 |

* engineに指定する文字の区切り文字 ``/`` は、``%2F`` に置き換えてください

=== "指示"
    ```js
        http://localhost:11900/api/command?target=Plugin_PlayVoice&command=set&engine=さとうささら%2FCeVIO_64
    ```

### デバイスの取得

* 送付方式：HTTP(GET)

=== "Request"
    ```js
        http://localhost:11900/api/command?target=Plugin_PlayVoice&command=device
    ```

=== "Result"
    ```json
    [
    'ずんだもん-ノーマル/VOICEVOX',
    'ずんだもん-あまあま/VOICEVOX'
    ]  
    ```

### 読み上げ指示

* 送付方式：HTTP(GET)

=== "パラメータ"

    |パラメータ|値    |例          |
    |---------|------|------------|
    |Text   |読む文章   | "おはよう" |
    |ID   |識別用のID   | "00000-0000-0000-000000" |
    |Engine   |エンジン名|さとうささら/CeVIO_64|
    |VoiceCastName|キャラクター名だけを指定する|ずんだもん|
    |VoiceStyleName|スタイル名だけを指定する|あまあま|
    |ReadingPhrase|読み方を指定する（表示と違う読みにしたいとき）|"おはよー"|
    |speakerDevice|音を出すデバイス名|スピーカー (Realtek)|
    |soundVolume|出力デバイスの音量|1.0|
    |Pitch    |高さ    | 1.0 |
    |Accent   |抑揚    | 1.0 |
    |Speed   |速度    | 1.0 |
    |Volume   | 音量  | 1.0 |
    |Quality   |声質    | 1.0 |
    |Kuten   |句点待ち時間    | 1.0 |
    |Toten   |読点待ち時間   | 1.0 |
    |prePhoneme   |前空白    | 1.0 |
    |postPhoneme   |後空白   | 1.0 |

* engineに指定する文字の区切り文字 ``/`` は、``%2F`` に置き換えてください
* パラメータ名は大文字・小文字を区別します
* IDを指定した場合は、何度要求しても1度しか読み上げません。
* ``Engine`` は「キャラクター名/エンジン名」をまとめて指定します。片方だけ変えたい場合は ``VoiceCastName`` ``VoiceStyleName`` を使ってください。

=== "Request"
    ```js
        http://localhost:11900/api/command?target=Plugin_PlayVoice&command=speech&Engine=さとうささら%2FCeVIO_64&Text=Hello
    ```

### APIタグでパラメータを切り替える

* 読み上げプラグインの設定に登録した「APIタグ」を指定して、音源や読み上げパラメータをまとめて切り替えます。

=== "実行"
    ```js
        http://localhost:11900/api/command?target=Plugin_PlayVoice&command=exec&tag=CALL
    ```

## 翻訳・発話連携サーバ

* ゆかコネNEOを通して翻訳と読み上げをサポートします。

!!! Tech "使用条件"
    * 翻訳/発話連携サーバプラグインをONにしていること
    * 翻訳１の翻訳エンジンを選定していること（これが使われます）
    * 送信先ポートはレジストリから取得します（前述の ``TransServer`` サブキー）
    * プラグイン v2.3以上

!!! Info "他のパソコンから使う場合"
    * 既定では同じパソコンの中からしか接続できません。
    * ほかの端末から使うには、「ネットワークの設定」画面の「すべてのIPアドレスを有効にする」をONにし、**さらにゆかコネNEOを管理者として起動**する必要があります。管理者権限がないと ``127.0.0.1`` のみでの待ち受けに戻ります。

### プラグイン通信

#### 翻訳（１言語）

* 翻訳/発話連携サーバプラグインが開いているHTTPサーバもしくはWebSocketサーバに下記のリクエストを送付してください。
* 送付方式：HTTPの場合はPOST、WSの場合はテキスト

=== "Request"
    ```js
    {
        operation: 'translate',
        params: [
            {
                id: '0000-0000-0000-0000',
                lang: 'en_US',
                text: 'こんにちは'
            }
        ]
    }
    ```
=== "Response(OK)"
    ```js
    {
        operation: 'translate',
        status: 'success'
        id: '0000-0000-0000-0000',
        lang: 'ja_JP',
        text: 'Hello.'
    }
    ```
=== "Response(NG)"
    ```js
    {
        operation: 'translate',
        status: 'failure'
        id: '0000-0000-0000-0000',
        lang: 'ja_JP',
        text: 'こんにちは.'
    }
    ```
* 要求時は、翻訳してほしい言語を指定します。
* 返答時には、推定した言語と翻訳した文が来ます。
* statusがfailureの場合は、処理に失敗しています。

#### 翻訳（複数言語）

!!! Tips "対応プラグインバージョン: v1.4以上"

* 翻訳/発話連携サーバプラグインが開いているHTTPサーバもしくはWebSocketサーバに下記のリクエストを送付してください。
* 送付方式：HTTPの場合はPOST、WSの場合はテキスト

=== "Request"
    ```js
    {
        operation: 'translates',
        params: [
            {
                id: '0000-0000-0000-0000',
                lang: [
                    'ja_JP',
                    'en_US',
                    'fr_FR'
                ],
                text: 'こんにちは'
            }
        ]
    }
    ```
=== "Response(OK) Case1"
    ```js
    {
        operation: 'translates',
        status: 'success'
        id: '0000-0000-0000-0000',
        detect_language : 'ja_JP',
        result : [
            {
                lang: 'ja_JP',
                text: 'こんにちは' 
            },
            {
                lang: 'en_US',
                text: 'Hello.' 
            },
            {
                lang: 'fr_FR',
                text: 'bonjour.' 
            }
        ]
    }
    ```
=== "Response(OK) Case2"
    ```js
    {
        operation: 'translates',
        status: 'success'
        id: '0000-0000-0000-0000',
        detect_language : 'unknown',
        result : [
            {
                lang: 'ja_JP',
                text: 'こんにちは' 
            },
            {
                lang: 'en_US',
                text: 'Hello.' 
            },
            {
                lang: 'fr_FR',
                text: 'bonjour.' 
            }
        ]
    }
    ```

=== "Response(NG)"
    ```js
    {
        operation: 'translates',
        status: 'failure'
        id: '0000-0000-0000-0000',
        message: '翻訳に失敗しました'
    }
    ```
* 要求時は、翻訳してほしい言語を指定します。
* 返答時には、推定した言語と翻訳した文が来ます。
* statusがfailureの場合は、処理に失敗しています。
* ``message`` には ``翻訳に失敗しました``（翻訳そのものが失敗）または ``パラメータ処理に失敗``（リクエストの内容が正しくない）が入ります。

#### 言語特定

* 翻訳/発話連携サーバプラグインが開いているHTTPサーバもしくはWebSocketサーバに下記のリクエストを送付してください。
* 送付方式：HTTPの場合はPOST、WSの場合はテキスト
* 対応バージョン : 連携プラグイン v1.6b～

=== "Request"
    ```js
    {
        operation: 'detectLanguage',
        params: [
            {
                id: '0000-0000-0000-0000',
                text: 'こんにちは'
            }
        ]
    }
    ```
=== "Response(OK)"
    ```js
    {
        operation: 'detectLanguage',
        status: 'success'
        id: '0000-0000-0000-0000',
        lang: 'ja_JP',
        text: 'こんにちは'
    }
    ```
=== "Response(NG)"
    ```js
    {
        operation: 'detectLanguage',
        status: 'failure'
        id: '0000-0000-0000-0000',
        lang: 'unknown',
        text: 'こんにちは'
    }
    ```

* 要求時は、言語特定してほしい文を指定します。
* 返答時には、推定した言語が来ます。
* 特定実行したが判断できない場合は言語名が unknow になります。
* statusがfailureの場合は、処理に失敗しています。

#### 読み上げ

* 翻訳/発話連携サーバプラグインが開いているHTTPサーバもしくはWebSocketサーバに下記のリクエストを送付してください。
* 送付方式：HTTPの場合はPOST、WSの場合はテキスト

!!! info "パラメータ拡張"
    * v2.0.73よりパラメータが追加されました。(volume)
    * volumeは発話音量の設定です。（`float`型、単位は`倍`。有効指定範囲 `0.2～2`　）

|パラメータ|意味|
|:--|:--|
|id|識別用のID|
|text|読ませる文章|
|talker|``キャラクター名/エンジン名`` をまとめて指定|
|volume|発話音量（0.2～2）|
|autherName|発話者名|
|voiceCast|キャラクター名だけを指定|
|voiceEngine|エンジン名だけを指定|
|voice|``キャラクター名/エンジン名``（``talker`` と同じ書き方）|
|soundCard|音を出すデバイス名|

=== "Request(Standard)"
    ```js
    {
        operation: 'speech',
        params: [
            {
                id: '0000-0000-0000-0000',
                text: 'こんにちは',
                talker: 'ずんだもん-ノーマル/VOICEVOX'
            }
        ]
    }
    ```
=== "Request(Extend)"
    ```js
    {
        operation: 'speech',
        params: [
            {
                id: '0000-0000-0000-0000',
                text: 'こんにちは',
                talker: 'ずんだもん-ノーマル/VOICEVOX',
                volume: 1.0,
                autherName: 'なお',
                soundCard: 'スピーカー (Realtek High Definition Audio)'
            }
        ]
    }
    ```
=== "Response(OK)"
    ```js
    {
        operation: 'speech',
        status: 'sended'
        id: '0000-0000-0000-0000',
        text: 'こんにちは.',
        talker: 'ずんだもん-ノーマル/VOICEVOX'
    }
    ```
=== "Response(NG)"
    ```js
    {
        operation: 'speech',
        status: 'failure'
        id: '0000-0000-0000-0000',
        text: 'こんにちは.' 
    }
    ```

* 要求時は、発話してほしいボイスキャラクターを指定するとその音源で話そうとします。
* statusがfailureの場合は、プラグインが無効な場合など要求が出せなかった場合にでます。
* statusがsendedの場合、要求自体はだせたという意味で、発話が完了したわけではありません。

#### 音声話者リスト

* 送付方式：HTTPの場合はPOST、WSの場合はテキスト
=== "Request"
    ```js
    {
        operation: 'speech.getvoicelist',
        params: [
            {
                id: '0000-0000-0000-0000',
            }
        ]
    }
    ```
=== "Response(OK)"
    ```js
    {
        operation: 'speech.getvoicelist',
        status: 'success'
        id: '0000-0000-0000-0000',
        voice: [
                'ずんだもん/VOICEVOX',
                '弦巻マキ(日)/CeVIO AI'
            ]
    }
    ```
=== "Response(NG)"
    ```js
    {
        operation: 'speech.getvoicelist',
        status: 'failure'
        id: '0000-0000-0000-0000'
    }
    ```

#### 出力デバイスリスト

* 音を出せるサウンドデバイスの一覧を取得します。
* 送付方式：HTTPの場合はPOST、WSの場合はテキスト

=== "Request"
    ```js
    {
        operation: 'speech.getdevicelist',
        params: [
            {
                id: '0000-0000-0000-0000',
            }
        ]
    }
    ```
=== "Response(OK)"
    ```js
    {
        operation: 'speech.getdevicelist',
        status: 'success'
        id: '0000-0000-0000-0000',
        voice: [
                'スピーカー (Realtek High Definition Audio)',
                'CABLE Input (VB-Audio Virtual Cable)'
            ]
    }
    ```

!!! Warning "キー名は voice です"
    デバイス一覧が入るキーは ``device`` ではなく **``voice``** です。音声話者リストと同じキー名を使っています。

* ここで得た名前を、読み上げの ``soundCard`` に指定できます。

#### 発話の強制停止

* 送付方式：HTTPの場合はPOST、WSの場合はテキスト
* 待っている分をクリアします。すでに発話が始まっているものは最後まで読み上げられます。

=== "Request"
    ```js
    {
        operation: 'speech.stop',
        params: [
            {
                id: '0000-0000-0000-0000',
            }
        ]
    }
    ```
=== "Response(OK)"
    ```js
    {
        operation: 'speech.stop',
        status: 'sended'
        id: '0000-0000-0000-0000',
    }
    ```
=== "Response(NG)"
    ```js
    {
        operation: 'speech.stop',
        status: 'failure'
        id: '0000-0000-0000-0000'
    }
    ```

#### バージョンの取得

!!! Tips "対応プラグインバージョン: v1.4a以上"

* 送付方式：HTTPの場合はPOST、WSの場合はテキスト

=== "Request"
    ```js
    {
        operation: 'version',
        params: [
            {
                id: '0000-0000-0000-0000',
            }
        ]
    }
    ```
=== "Response(OK)"
    ```js
    {
        operation: 'version',
        status: 'success',
        version: {
            System: '1.959',
            Plugin: '1.4a'
        },
        id: '0000-0000-0000-0000',
    }
    ```
=== "Response(NG)"
    ```js
    {
        operation: 'version',
        status: 'failure',
        id: '0000-0000-0000-0000'
    }
    ```
|名前|型|意味|
|:--|:--|:--|
|System|String|NEO本体のバージョン|
|Plugin|String|翻訳/発話連携サーバプラグイン|

!!! Warning "version は配列ではありません"
    ``version`` は ``{ System: ..., Plugin: ... }`` というオブジェクトです。配列としては返りません。

#### OSCの送信

* 翻訳/発話連携サーバプラグインが開いているHTTPサーバもしくはWebSocketサーバに下記のリクエストを送付してください。
* 送付方式：HTTPの場合はPOST、WSの場合はテキスト
* 対応バージョン：v2.0.73～

=== "Request"
    ```js
    {
        operation: 'osc',
        params: [
            {
                address: '/comment/text',
                id: '0000-0000-0000-0000',
                text: 'こんにちは',
                autherName: 'なお',
                target : [
                    'vrchat',
                    'virtualcast',
                    'unity',
                    'neosvr'
                ]
            }
        ]
    }
    ```
=== "Response(OK)"
    ```js
    {
        operation: 'osc',
        status: 'sended'
        id: '0000-0000-0000-0000',
        text: 'こんにちは.'
    }
    ```
=== "Response(NG)"
    ```js
    {
        operation: 'osc',
        status: 'failure'
        id: '0000-0000-0000-0000',
        text: 'こんにちは.'
    }
    ```
!!! info "連携に必要なプラグイン名"
    |送信先        |有効化すべきプラグイン|
    |-------------------|------------------------------|
    |vrchat       |VRChatプラグイン　　　　　　　　　　|
    |virtualcast   |VirtualCastプラグイン　　　　　　　　　　|
    |unity         |VMCプラグイン　　　　　　　　　　|
    |neosvr       |NeosVRプラグイン　　　　　　　　　　|

* 指定したOSC通信をプラットフォームに送信します。
* statusがfailureの場合は、プラグインが無効な場合など要求が出せなかった場合にでます。
* statusがsendedの場合、要求自体はだせたという意味です。

#### チャットとしてのOSC送信

* ``osc`` とほぼ同じですが、**チャット送信として**プラグインに渡します。VRChatのChatboxなどに出したい場合はこちらを使ってください。
* 送付方式：HTTPの場合はPOST、WSの場合はテキスト

=== "Request"
    ```js
    {
        operation: 'osc.chat',
        params: [
            {
                id: '0000-0000-0000-0000',
                text: 'こんにちは',
                target : [
                    'vrchat'
                ]
            }
        ]
    }
    ```

* ``osc`` は「任意のOSCアドレスへ送る」動作、``osc.chat`` は「チャット欄へ出す」動作です。
* VRChatのChatboxには送信の間隔制限があるため、``osc.chat`` では順番待ちの調整が入ります。

#### AIをつかった言葉の処理

* ゆかコネNEO本体で選んでいるAI（「翻訳（API、設定）」画面の「プラグインで使うAIの種類」）へ問い合わせます。
* 送付方式：HTTPの場合はPOST、WSの場合はテキスト

=== "Request"
    ```js
    {
        "operation": "llm",
        "params": [
            {
                "id": "0000-0000-0000-0000",
                "premise": "あなたはおじいさん役。",
                "prompt": "役割に合わせ発言せよ。「おはよう」",
                "model": "gpt-4o"
            }
        ]
    }
    ```
=== "Response(OK)"
    ```js
    {
        operation: 'llm',
        status: 'success'
        id: '0000-0000-0000-0000',
        text: '「皆の者、おはよう」'
    }
    ```
=== "Response(NG)"
    ```js
    {
        operation: 'llm',
        status: 'failure'
        id: '0000-0000-0000-0000',
        text: ''
    }
    ```

* ``model`` を省略すると ``gpt-4o`` が使われます。
* AIのAPIキーが設定されていない場合は failure になります。

#### GPTをつかった言葉の処理

* GPT3プラグイン経由でAIに文章を作らせます。
* 送付方式：HTTPの場合はPOST、WSの場合はテキスト
* 対応バージョン：v2.0.94～

=== "Request"
    ```js
    {
        "operation": "gpt",
        "params": [
            {
                "id": "0000-0000-0000-0000",
                "command": "question",
                "premise": "あなたはおじいさん役。",
                "prompt": "役割に合わせ発言せよ。「おはよう」",
                "maxtokens": 1000,
                "temperature":0.5
            }
        ]
    }
    ```

=== "Response(OK)"
    ```js
    {
        operation: 'gpt',
        status: 'success'
        id: '0000-0000-0000-0000',
        text: '「皆の者、おはよう」' 
    }
    ```
=== "Response(NG)"
    ```js
    {
        operation: 'gpt',
        status: 'failure'
        id: '0000-0000-0000-0000',
        text: ''
    }
    ```

* GPT3プラグイン自体が有効で、APIキーなどが設定済みであるときに使用可能です。
* statusがfailureの場合は、プラグインが無効な場合など要求が出せなかった場合にでます。

#### 知らない operation を送ったとき

* HTTPのステータスは ``200`` のまま、次の内容が返ります。

```js
{
    operation: '(送ったoperation)',
    status: 'failure',
    message: 'Bad Request',
    id: '0000-0000-0000-0000'
}
```

* ``params`` そのものが解釈できない場合だけ、HTTP ``400`` になります。

## 入力支援

* ゆかコネNEOの文字入力を支援します
!!! Tech "使用条件"
    * 入力支援プラグインをONにしていること

### 遠隔操作

* 送付方式：HTTP(GET)

=== "１行前に移動"
    ```js
        http://localhost:11900/api/command?target=Plugin_InputAssist&command=prev
    ```
=== "１行後に移動"
    ```js
        http://localhost:11900/api/command?target=Plugin_InputAssist&command=next
    ```
=== "カーソル行を送信"
    ```js
        http://localhost:11900/api/command?target=Plugin_InputAssist&command=send
    ```
=== "カーソル行を送り次の行に移動"
    ```js
        http://localhost:11900/api/command?target=Plugin_InputAssist&command=sendnext
    ```

## 辞書プラグイン

* ゆかコネNEOの文字精度UPを支援します
!!! Tech "使用条件"
    * 辞書プラグインをONにしていること
    * バージョン v1.8以上

### 辞書の臨時差し替え

* 送付方式：HTTP(GET)

=== "置換辞書"
    ```js
        http://localhost:11900/api/command?target=Plugin_Dictionary&command=load&type=replace&file=d:/dic1.csv
    ```
=== "対訳辞書"
    ```js
        http://localhost:11900/api/command?target=Plugin_Dictionary&command=load&type=translation&file=d:/dic2.csv
    ```

## 歌詞プラグイン

* 音楽にあわせて歌詞表示を支援します
!!! Tech "使用条件"
    * 歌詞プラグインをONにしていること

### 遠隔操作

* 送付方式：HTTP(GET)

=== "再生"
    ```js
        http://localhost:11900/api/command?target=Plugin_LyricAssist&command=play
    ```
=== "一時停止"
    ```js
        http://localhost:11900/api/command?target=Plugin_LyricAssist&command=pause
    ```
=== "停止"
    ```js
        http://localhost:11900/api/command?target=Plugin_LyricAssist&command=stop
    ```
=== "ファイルロード"
    * ``sukiyuki.stl`` を読み込む場合
    ```js
        http://localhost:11900/api/command?target=Plugin_LyricAssist&command=load&file=d:/sukiyuki.stl
    ```

## OBS WSプラグイン

* 指定した字幕ソースに文字を表示したり、OBSを操作します。

!!! Tech "使用条件"
    * OBS-WSプラグインをONにしていること
    * OBS-WSプラグイン v2.1以上で有効

### ソースに指定した字幕を表示する

* 送付方式：HTTP(GET)

|パラメータ|意味|
|:--|:--|
|text|表示する文字|
|source|ソース名|
|sourceNo|同じ名前のソースが複数あるときの番号（省略時 ``0``）|

=== "実行"
    * ソース名 ``字幕枠`` に ``あいうえお`` と表示したい場合
    ```js
        http://127.0.0.1:11900/api/command?target=Plugin_OBS&command=set&text=あいうえお&source=字幕枠
    ```

### シーンを切り替える

=== "実行"
    * シーン ``トーク`` に切り替えたい場合
    ```js
        http://127.0.0.1:11900/api/command?target=Plugin_OBS&command=scene&scene=トーク
    ```

### リプレイバッファを操作する

=== "開始"
    ```js
        http://127.0.0.1:11900/api/command?target=Plugin_OBS&command=startreplay
    ```
=== "停止"
    ```js
        http://127.0.0.1:11900/api/command?target=Plugin_OBS&command=stopreplay
    ```

* OBS側でリプレイバッファが有効になっている必要があります。

## OBS WS5プラグイン

* 指定した字幕ソースに文字を表示したり、OBSを操作します。
* 使えるコマンドとパラメータは「OBS WSプラグイン」と同じです。``target`` だけが変わります。

!!! Tech "使用条件"
    * OBS-WS5プラグインをONにしていること
    * OBS-WS5プラグイン v2.3以上で有効

=== "字幕を表示"
    ```js
        http://127.0.0.1:11900/api/command?target=Plugin_OBS5&command=set&text=あいうえお&source=字幕枠
    ```
=== "シーン切替"
    ```js
        http://127.0.0.1:11900/api/command?target=Plugin_OBS5&command=scene&scene=トーク
    ```
=== "リプレイバッファ"
    ```js
        http://127.0.0.1:11900/api/command?target=Plugin_OBS5&command=startreplay
        http://127.0.0.1:11900/api/command?target=Plugin_OBS5&command=stopreplay
    ```

## VRChat OSCプラグイン

* 指定したOSCメッセージを送付します。

!!! Tech "使用条件"
    * VRChat OSCプラグインをONにしていること
    * OSCプラグイン v1.5以上で有効

### OSCメッセージの遠隔発火

* 送付方式：HTTP(GET)

=== "実行"
    * 送信タグ名 ``EyeClose`` を送りたい場合
    ```js
        http://localhost:11900/api/command?target=Plugin_VRChat_OSC&command=exec&tag=EyeClose
    ```

### 任意のOSCアドレスへ送る

|パラメータ|意味|
|:--|:--|
|address|OSCアドレス（省略時 ``/comment/text``）|
|message|送る文字列|

=== "実行"
    ```js
        http://localhost:11900/api/command?target=Plugin_VRChat_OSC&command=send&address=/avatar/parameters/Wave&message=1
    ```

### VRChatのChatboxへ送る

=== "実行"
    ```js
        http://localhost:11900/api/command?target=Plugin_VRChat_OSC&command=chat&message=こんにちは
    ```

* VRChatのChatboxには送信間隔と文字数の制限があるため、順番待ちの調整が入ります。長い文は分割して送られます。
* プラグイン設定の「効果音を鳴らさない」「自動送信しない」に従います。

### シナリオロールの遠隔操作

|``action``|動作|
|:--|:--|
|``open``（省略時）|シナリオロールの画面を開く|
|``close``|画面を閉じる|
|``run``|``text`` に指定した1行をその場で実行する|
|``send``|カーソル行を送信する|
|``sendnext``|カーソル行を送信して次の行へ|
|``next`` / ``prev``|カーソルを次／前の行へ|
|``stop``|実行を止める|

=== "実行"
    ```js
        http://localhost:11900/api/command?target=Plugin_VRChat_OSC&command=scenario&action=sendnext
    ```

* 画面が開いていない状態で操作しようとすると ``シナリオロールが開いていません`` が返ります。

## HTTPコールプラグイン

* 指定したHTTP呼び出し(GET)を送付します。

!!! Tech "使用条件"
    * HTTPコールプラグインをONにしていること
    * ゆかコネNEO v2.0～で有効

### HTTPメッセージの遠隔発火

* 送付方式：HTTP(GET)

=== "実行"
    * 送信タグ名 ``CALL`` を送りたい場合
    ```js
        http://localhost:11900/api/command?target=Plugin_HTTPCall&command=exec&tag=CALL
    ```

!!! Warning "置換マクロは空になります"
    このコマンドで発火した場合、``{text0}`` などの置換マクロは**すべて空文字**になります。発話にひもづいた呼び出しではないためです。

## WebSocketコールプラグイン

* 指定したWebSocket呼び出しを送付します。

!!! Tech "使用条件"
    * WebSocketコールプラグインをONにしていること
    * ゆかコネNEO v2.3.128～（それ以前のバージョンでは正しく送信できません）

### WebSocketメッセージの遠隔発火

* 送付方式：HTTP(GET)

=== "実行"
    * 送信タグ名 ``CALL`` を送りたい場合
    ```js
        http://localhost:11900/api/command?target=Plugin_WSCall&command=exec&tag=CALL
    ```

* 設定した接続先へつなぎ、「送信文字」に書いた内容を送ったあと、通信を終了します。

!!! Warning "置換マクロは空になります"
    このコマンドで発火した場合、``{text0}`` などの置換マクロは**すべて空文字**になります。発話にひもづいた呼び出しではないためです。これはコールURL・送信文字の両方にあてはまります。

## clusterウェブトリガープラグイン

* 指定したHTTP呼び出し(GET)を送付します。

!!! Tech "使用条件"
    * clusterウェブトリガープラグインをONにしていること
    * ゆかコネNEO v2.0～で有効

### ウェブトリガーの遠隔発火

* 送付方式：HTTP(GET)

=== "実行"
    * 送信タグ名 ``Trig1`` を発火したい場合
    ```js
        http://localhost:11900/api/command?target=Plugin_ClusterTrigger&command=exec&tag=Trig1
    ```

## NeosVRプラグイン

* NeosVRと通信してトリガーをかけることができます。

!!! Tech "使用条件"
    * NeosVRプラグインをONにしていること
    * ゆかコネNEO v2.0～で有効

### メッセージの遠隔発火

* 送付方式：HTTP(GET)

=== "APIタグで発火"
    * 送信タグ名 ``CALL`` を送りたい場合
    ```js
        http://localhost:11900/api/command?target=Plugin_NeosVR&command=exec&tag=CALL
    ```
=== "任意のメッセージを送る"
    ```js
        http://localhost:11900/api/command?target=Plugin_NeosVR&command=send&address=/comment/text&message=こんにちは
    ```

## バーチャルキャストプラグイン

* バーチャルキャストへOSCメッセージを送ります。

!!! Tech "使用条件"
    * バーチャルキャストプラグインをONにしていること

=== "実行"
    ```js
        http://localhost:11900/api/command?target=Plugin_VCas&command=send&address=/comment/text&message=こんにちは
    ```

* ``address`` を省略すると ``/comment/text`` が使われます。

## ばもきゃ（VMC）プラグイン

* ばもきゃへOSCメッセージを送ったり、表情を変えたりできます。

!!! Tech "使用条件"
    * ばもきゃ連携プラグインをONにしていること

### 任意のOSCアドレスへ送る

=== "実行"
    ```js
        http://localhost:11900/api/command?target=Plugin_VMC&command=send&address=/comment/text&message=こんにちは
    ```

### 表情を変える

|パラメータ|意味|
|:--|:--|
|face|表情の名前（省略時 ``Fun``）|
|value|強さ（省略時 ``0.0``）|

=== "実行"
    ```js
        http://localhost:11900/api/command?target=Plugin_VMC&command=send_face&face=Joy&value=1.0
    ```

## VTubeStudio プラグイン

* VTubeStudioと通信してトリガーをかけることができます。

!!! Tech "使用条件"
    * VTubeStudioプラグインをONにしていること
    * ゆかコネNEO v2.0.17～で有効

!!! Warning "識別名の綴りに注意"
    ``target`` は **``Plugin_VtubeStudio``** です。``Plugin_VtuberStudio``（"Vtuber"）ではありません。綴りが違うとプラグインが見つからず ``400`` になります。

### キーバインドアクションの遠隔発火

* 送付方式：HTTP(GET)

=== "APIタグで発火"
    * プラグイン設定に登録したAPIタグ ``CALL`` を発火する場合
    ```js
        http://localhost:11900/api/command?target=Plugin_VtubeStudio&command=exec&tag=CALL
    ```
=== "キーバインド名を直接指定"
    * VTubeStudio側のキーバインド名 ``手をふる`` を直接発火する場合
    ```js
        http://localhost:11900/api/command?target=Plugin_VtubeStudio&command=call&tag=手をふる
    ```

* ``exec`` はプラグインに登録したルール（APIタグ）を経由します。``call`` はルールを経由せず、``tag`` の値をそのままキーバインド名として使います。

## Discord BOTプラグイン

* Discordへメッセージや音声を送ります。

!!! Tech "使用条件"
    * Discord BOTプラグインをONにしていること
    * プラグイン設定の「受信」がONになっていること

=== "テキストチャンネルへ送る"
    ```js
        http://localhost:11900/api/command?target=Plugin_Discord&command=exec&text=こんにちは
    ```
=== "ボイスチャンネルで音声を再生"
    ```js
        http://localhost:11900/api/command?target=Plugin_Discord&command=sendvoice&filename=d:/sound/se1.wav
    ```

* テキスト送信は、プラグイン設定の読み上げ（TTS）設定に従います。

## Discord Webhookプラグイン

* Webhookへ投稿します。

!!! Tech "使用条件"
    * Discord WebhookプラグインをONにしていること

|パラメータ|意味|
|:--|:--|
|text|投稿する文字|
|ID|識別用のID（省略すると自動で採番されます）|
|talkername|表示名（省略時 ``ync-webhook``）|

=== "実行"
    ```js
        http://localhost:11900/api/command?target=Plugin_DiscordWebHook&command=exec&text=こんにちは&talkername=なお
    ```

* ``ID`` は同じ内容を二重に投稿しないために使われます。

## ルビ付与プラグイン

* 日本語の読みや形態素解析の結果を取得できます。

!!! Tech "使用条件"
    * ルビ付与プラグインをONにしていること

=== "ひらがな読みを得る"
    ```js
        http://localhost:11900/api/command?target=Plugin_Ruby&command=makehiragana&text=今日は良い天気です
    ```
=== "形態素解析の結果を得る"
    ```js
        http://localhost:11900/api/command?target=Plugin_Ruby&command=makemorph&text=今日は良い天気です
    ```

* ``makehiragana`` はプレーンテキスト、``makemorph`` はJSONを返します。

## 会話の記録プラグイン

* 記録した会話を取り出したり、集計結果を得られます。

!!! Tech "使用条件"
    * 会話の記録プラグインをONにしていること

|command|パラメータ|内容|
|:--|:--|:--|
|``gethistory``|``limit``（省略時100、最大1000）|新しい順に会話を取り出す|
|``search``|``q``（必須）|本文と話者名の部分一致で検索する（最大100件）|
|``stats``|—|総件数・話者数・最も古い記録などの統計|
|``karte``|—|「喋りカルテ」の集計結果|
|``dashboard``|—|ダッシュボードを作り直し、表示用のURLを返す|

=== "会話を取り出す"
    ```js
        http://localhost:11900/api/command?target=Plugin_TalkHistory&command=gethistory&limit=50
    ```
=== "検索する"
    ```js
        http://localhost:11900/api/command?target=Plugin_TalkHistory&command=search&q=天気
    ```

* いずれもJSONを返します。``gethistory`` は ``{success, count, data}``、``search`` は ``{success, searchTerm, count, data}`` の形です。
* 対応していない ``command`` を送ると、使えるコマンドの一覧が返ります。

## GPT3 プラグイン

* AIに文章を作らせることができます。

!!! Tech "使用条件"
    * GPT3プラグインをONにしていること
    * APIキーが設定済みであること
    * ゆかコネNEO v2.0.94～で有効

### AIに文章を作らせる

* 送付方式：HTTP(GET)

|パラメータ|意味|
|:--|:--|
|prompt|AIに投げる文章|
|premise|前提（役割や状況の指定）|
|talkerName|相手の名前。プロンプト内の ``$name_user`` に入ります|
|maxtokens|返答の最大長|
|temperature|ばらつきの度合い|

=== "実行"
    ```js
        http://localhost:11900/api/command?target=Plugin_GPT3&command=question&premise=あなたはおじいさん役。&prompt=役割に合わせ発言せよ。「おはよう」&maxtokens=1000&temperature=0.5
    ```

* ``command`` には ``question`` または ``response`` を指定します。どちらも同じ動作です。
* AIが返した文章がそのまま応答本文になります。

!!! Info "JSON形式で送りたい場合"
    JSONでやりとりしたい場合は、このページの「翻訳・発話連携サーバ」にある「GPTをつかった言葉の処理」または「AIをつかった言葉の処理」を使ってください。こちらの ``/api/command`` はクエリ形式のみです。

## 本体のWebサーバから配信されるファイル

* 一部のプラグインは、ゆかコネNEO本体のHTTPサーバ上にファイルを公開します。配信ソフトのブラウザソースなどから直接読み込めます。
* ベースとなるアドレスは、各プラグインの設定画面に表示されています。

|パス|プラグイン|内容|
|:--|:--|:--|
|``/Native.txt``|配信ソフト向けテキスト出力|母国語の字幕|
|``/Translate1.txt``～``/Translate4.txt``|同上|翻訳1～翻訳4の字幕|
|``/Summary.txt``|同上|要約|
|``/Footnote.txt``|同上|脚注|
|``/api/screenshot``|clusterウェブトリガ|直近のスクリーンショット画像|
|``/comment.json`` ``/api/comments``|わんコメテンプレ連携|わんコメ形式のコメントJSON|
|``/style.css`` ``/Templates/…``|同上|テンプレート用のCSSや素材|
|``/Plugin_TalkHistory/karte.html``|会話の記録|喋りカルテのダッシュボード|
|``/Plugin_TalkHistory/karte.json``|同上|カルテのデータ|

* 配信ソフト向けテキスト出力は、話者ごとに ``/Native_なお.txt`` のような名前でも配信されます。ファイル名を自分で決めた場合はその名前になります。
* これらが公開されるのは、該当プラグインが有効で、かつHTTP出力の設定がONのときだけです。

## 置換マクロ（テンプレート変数）

* 一部のプラグインでは、設定した文字列の中に発話の内容を差し込めます。

|プラグイン|使えるマクロ|使える場所|
|:--|:--|:--|
|HTTPコール|``{text0}``～``{text4}`` ``{lang0}``～``{lang4}`` ``{talker}``|アドレス（URL）|
|WebSocketコール|``{text0}``～``{text4}`` ``{lang0}``～``{lang4}`` ``{talker}``|コールURL と 送信文字の両方|
|clusterウェブトリガ|``{talker}``|送信内容|
|配信ソフト向けテキスト出力|``$title`` ``$summary``|要約フォーマット（既定 ``【$title】$summary``）|
|GPT3/AIアシスタント|``$name_ai`` ``$name_user`` ``$message``|AIロールプロンプト、高優先プロンプト|
|Teams Webhook|``{{Text1}}`` ``{{Text2}}``|送信カードのテンプレート|

|マクロ|内容|
|:--|:--|
|``{text0}``|母国語の文章|
|``{text1}``～``{text4}``|翻訳1～翻訳4の文章|
|``{lang0}``|母国語の言語名|
|``{lang1}``～``{lang4}``|翻訳1～翻訳4の言語名|
|``{talker}``|発話者名|

!!! Warning "マクロは自動でURLエンコードされます"
    * 差し込まれる値は URLエンコード（パーセントエンコード）されます。日本語は ``%E3%81%82`` のような形になります。
    * 受け取る側でデコードが必要です。
    * URL以外の場所（WebSocketコールの送信文字など）でもエンコードされる点に注意してください。

!!! Warning "APIタグで発火した場合は空になります"
    ``/api/command?command=exec&tag=…`` で発火したときは、発話にひもづいていないため**すべてのマクロが空文字**になります。マクロを使いたい場合は、発話をきっかけに動くルールとして設定してください。
