# ゆかコネNEO プラグインリファレンス

> プラグインの設定は ConfigWindow (設定画面) を通じて行います。
> 設定ファイルの直接編集は推奨されません。

**公式ドキュメント**: [プラグインの使い方](../plugin/enabled.md) / [プラグイン一覧](../plugin/index.md)

---

## プラグインアーキテクチャ

### 基本構造

すべてのプラグインは `PluginFunction` 基底クラスを継承し、以下のライフサイクルメソッドを持ちます：

| メソッド | タイミング | 目的 |
|---------|----------|------|
| `onLoad()` | 起動時 | 初期化、設定読み込み、GUI作成 |
| `UpdateText(textdata)` | テキスト受信時 | テキストの処理・変換 |
| `onTrigger(command)` | コマンド受信時 | プラグイン間コマンド処理 |
| `onTerminate()` | 終了時 | 設定保存、リソース解放 |

### 設定画面の共通パターン
全プラグインのConfigWindowは以下の共通要素を持ちます：
- **OKボタン**: 設定を保存して閉じる
- **Cancelボタン**: 変更を破棄して閉じる
- **?ボタン** (openHelp): ヘルプページを開く
- **Versionラベル**: プラグインバージョン表示

---

## Audio/TTS Plugins

### Plugin_PlayVoice - 読み上げプラグイン
**Purpose**: Multi-engine text-to-speech synthesis

#### ConfigWindow構造: 6タブ構成

**タブ1: 基本設定**

| GUI要素 | 種類 | 説明 |
|---------|------|------|
| 使う読み上げエンジン | ComboBox (`TTS_EngineDevice`) | TTS エンジン選択 |
| 読み上げ対象 | ComboBox (`TTS_SpeakMode`) | 母国語/翻訳/両方 |
| 音声出力先 | ComboBox (`TTS_SpeakerDevice`) | オーディオデバイス選択 |
| コントローラ選択 | ComboBox (`SelectSoundEngine`) | PlayEngine/AssistantSeika |
| ひらがなベース読み上げ | CheckBox (`useHiragana`) | かな変換有効化 |
| アルファベット読み上げフォロー | CheckBox (`UseSpeakAssist`) | 英字読み上げ補助 |
| かわいい語尾設定 | TextBox (`KawaiiFixed`) | 語尾変換パターン |

**GroupBox: AssistantSeika接続設定**

| GUI要素 | 種類 | 説明 |
|---------|------|------|
| アドレス | TextBox (`SeikaAddr`) | AssistantSeika接続先 |
| ID | TextBox (`SeikaID`) | 認証ID |
| パスワード | TextBox (`SeikaPW`) | 認証パスワード |

**GroupBox: パラメータ設定**

| GUI要素 | 種類 | 範囲 | 説明 |
|---------|------|------|------|
| Pitch | TrackBar | - | 音程 |
| Accent | TrackBar | - | アクセント |
| Speed | TrackBar | - | 話速 |
| Volume | TrackBar | - | 音量 |
| prePhoneme | TrackBar | - | 前音素 |
| postPhoneme | TrackBar | - | 後音素 |
| Kuten | TrackBar | - | 句点間隔 |
| Toten | TrackBar | - | 読点間隔 |
| Quality | TrackBar | - | 品質 |

**GroupBox: CoeFont設定**

| GUI要素 | 種類 | 説明 |
|---------|------|------|
| AccessKey | TextBox (`CoeFontAccessKey`) | CoeFont APIキー |
| ClientKey | TextBox (`CoeFontClientKey`) | クライアントキー |
| プリセット | ComboBox (`VoicePreset`) | 音声プリセット選択 |
| VoiceUUID | TextBox (`CoeFontVoiceUUID`) | 音声ID |

**ボタン操作**:
- `RestartEngine`: エンジン再起動
- `ParamReset`: パラメータリセット
- `ApplyButton`: 変更適用

---

### Plugin_Bouyomi - 棒読みちゃん連携
**Purpose**: Bouyomi-chan TTS integration

#### ConfigWindow構造: シンプル(単一GroupBox)

**GroupBox: 読み上げ設定 (Settings)**

| GUI要素 | 種類 | デフォルト | 説明 |
|---------|------|------------|------|
| 読み上げ対象言語 | ComboBox (`TTS_SpeakMode`) | - | 母国語/翻訳1～4 |
| 通信方式 | ComboBox (`BouyoumiMethod`) | Socket | Socket通信/HTTP通信 |
| 通信ポート | NumericUpDown (`BouyomiPort`) | 50001 | 棒読みちゃんポート |
| 音声ID | NumericUpDown (`BouyomiID`) | 0 | 0～65535 |
| 音量 | NumericUpDown (`BouyomiVolume`) | -1 | -1=デフォルト |
| 話速 | NumericUpDown (`BouyomiSpeed`) | -1 | -1=デフォルト |
| トーン | NumericUpDown (`BouyomiTone`) | -1 | -1=デフォルト |
| ディレイ(ms) | NumericUpDown (`BouyomiDelay`) | 0 | 遅延時間 |
| ひらがなベース | CheckBox (`useHiragana`) | OFF | かな変換 |

**音声ID一覧**:
- 0: 女性1
- 1: 女性2
- 2: 男性1
- 3: 男性2
- 4: 中性
- 5: ロボット
- 6: 機械

**ボタン操作**:
- `setDefault`: 棒読みちゃんに従う（デフォルト設定適用）

---

### Plugin_PlaySound - 効果音再生
**Purpose**: Trigger sound effects based on conditions

#### ConfigWindow構造: GroupBox + DataGridView

**上部設定**

| GUI要素 | 種類 | 説明 |
|---------|------|------|
| 出力先 | ComboBox (`TTS_SpeakerDevice`) | オーディオ出力デバイス |
| 音楽は重複させない | CheckBox (`isOnePlay`) | 同時再生制限 |
| サウンドは直接再生する | CheckBox (`soundDirectly`) | 直接再生モード |

**DataGridView: 条件設定 (`dgv_Sound`)**

| 列名 | 種類 | 説明 |
|------|------|------|
| モード(Mode) | ComboBox | 完全/一部/無効 |
| 起動キーワード(Keyword) | TextBox | トリガー文字列 |
| 音源ファイル(File) | TextBox | 音声ファイルパス |
| 再生前遅延(Delay[ms]) | TextBox | 再生前待機時間 |
| 再生後遅延(Delay[ms]) | TextBox | 再生後待機時間 |
| 再生モード(Play mode) | ComboBox | 非同期(Async)/同期(Sync) |
| 文字差し替え(Replace) | CheckBox | テキスト置換有効 |
| 読み上げ文字(Caption) | TextBox | 置換後テキスト |
| 後処理(Pre/Post) | CheckBox | 後処理フラグ |
| TTS無効化(No TTS) | CheckBox | 読み上げスキップ |

**CSV操作パネル**:
- `ロード(Load)`: CSVから読み込み
- `セーブ(Save)`: CSVへ保存
- `クリア(All Clear)`: 全削除

**右クリックメニュー**:
- 行の上に挿入
- 行の下に挿入
- 上と入れ替え
- 下と入れ替え
- 削除
- ファイルから読み込み

---

## Streaming Plugins

### Plugin_OBS5 - OBS Studio v28+対応
**Purpose**: OBS Studio WebSocket 5.x integration

#### ConfigWindow構造: 複数GroupBox + StatusBar

**GroupBox: 接続 (Connect to)**

| GUI要素 | 種類 | デフォルト | 説明 |
|---------|------|------------|------|
| 通信先アドレス | TextBox (`OBSAddr`) | 127.0.0.1 | OBS WebSocket IP |
| ポート番号 | NumericUpDown (`OBSPort`) | 4455 | WebSocket ポート |
| パスワード | TextBox (`OBSPass`) | - | WebSocket パスワード (マスク表示) |

**接続ボタン**:
- `接続`: OBSに接続
- `切断`: 接続解除
- `自動設定`: ソース自動検出

**GroupBox: 送信先 (Send to)**

| GUI要素 | 種類 | 説明 |
|---------|------|------|
| 母国語 (Native) | ComboBox (`OBS_Transfer_Source1`) | テキストソース選択 |
| 翻訳1 (Translate1) | ComboBox (`OBS_Transfer_Source2`) | テキストソース選択 |
| 翻訳2 (Translate2) | ComboBox (`OBS_Transfer_Source3`) | テキストソース選択 |
| 翻訳3 (Translate3) | ComboBox (`OBS_Transfer_Source4`) | テキストソース選択 |
| 翻訳4 (Translate4) | ComboBox (`OBS_Transfer_Source5`) | テキストソース選択 |
| 先頭一致で複数送信 | CheckBox (`SendToOBS_MultiSupport`) | ソース名前方一致 |
| 発話名付きで送信 | CheckBox (`SendToOBS_NameSupport`) | 話者名追加 |

**GroupBox: トークの見出し・要約生成**

| GUI要素 | 種類 | 説明 |
|---------|------|------|
| 要約生成有効 | CheckBox (`makeTalkSummary`) | 要約機能ON/OFF |
| 要約送信先 | ComboBox (`OBS_Transfer_Source_Summary`) | 要約用ソース |
| 要約に使う行数 | NumericUpDown (`useSummaryLines`) | 5～50行 |
| フォーマット | TextBox (`summaryFormat`) | 例: 「【$title】$summary」 |
| 要約頻度(分) | NumericUpDown (`SummaryCycleTime`) | 更新間隔 |
| 翻訳で交互表示 | CheckBox (`SummaryLinesMulti`) | 多言語ローテーション |
| 切り替え間隔(秒) | NumericUpDown (`SummaryLinesMultiTime`) | ローテーション間隔 |

**GroupBox: オプション (Option)**

| GUI要素 | 種類 | 説明 |
|---------|------|------|
| テキスト削減有効 | CheckBox (`clopEnabled`) | 長文カット |
| 削減文字数 | NumericUpDown (`clopTextLen`) | 最大文字数 |
| 途中削減方式 | RadioButton (`Method_Clop`) | 中間カット |
| 改行処理方式 | RadioButton (`Method_Return`) | 改行でカット |
| ブロック単位削減 | CheckBox (`ClopByBlock`) | ブロック処理 |
| CR/LFコード処理 | CheckBox (`Reform_CRdata`) | 改行コード変換 |
| OBSに送らない | CheckBox (`mnu_NoRetToOBS`) | 送信無効化 |
| 配信開始/終了検知 | CheckBox (`detectStreamingEnd`) | 配信状態監視 |

**GroupBox: クローズドキャプション**

| GUI要素 | 種類 | 説明 |
|---------|------|------|
| CC送信有効 | CheckBox (`SendOBSClosedCaption`) | CC機能ON |
| CC送信先 | ComboBox (`ClosedCaptionSource`) | CCソース選択 |

---

### Plugin_Discord - Discord連携
**Purpose**: Discord bot for sending/receiving messages

#### ConfigWindow構造: 複数GroupBox

**GroupBox: Discord設定 (Setting)**

| GUI要素 | 種類 | 説明 |
|---------|------|------|
| クライアントID | TextBox (`ClientID`) | Discord App Client ID |
| トークン | TextBox (`Token`) | Bot Token (マスク表示) |
| チャンネルID | TextBox (`ChannelID`) | 対象チャンネルID |
| Discord→NEO | CheckBox (`isSend`) | 受信有効化 |
| NEO→Discord | CheckBox (`isRecv`) | 送信有効化 |
| トークセッション対応 | CheckBox (`MultiUserMode`) | 複数ユーザーモード |
| BOTも受信対象 | CheckBox (`IncludingBOT`) | BOTメッセージ含む |
| Discord標準TTS | CheckBox (`speechTTS`) | Discord TTS使用 |

**ボタン操作**:
- `接続認証ボタン`: OAuth認証実行

**GroupBox: 接続 (Connection)**

| GUI要素 | 種類 | 説明 |
|---------|------|------|
| 接続 | Button (`toConnect`) | サーバー接続 |
| 切断 | Button (`toDisconnect`) | 接続解除 |
| 接続状態 | Panel (`ConnectPanel`) | 状態表示 |

**GroupBox: ユーザを限定**

| GUI要素 | 種類 | 説明 |
|---------|------|------|
| フィルタ対象ユーザ | TextBox (Multiline, `IncludingWriter`) | ユーザーID一覧 (1行1ID) |

**GroupBox: 音声の転送**

| GUI要素 | 種類 | 説明 |
|---------|------|------|
| 読み上げ音声をDiscordへ | CheckBox (`sendSpeechVoice`) | 音声送信 |
| PC側では読み上げない | CheckBox (`stopSpeechOnPC`) | ローカルミュート |

---

### Plugin_Twitch - Twitch連携
**Purpose**: Twitch chat integration

#### ConfigWindow構造: 2つのGroupBox

**GroupBox: Twitch設定 (Setting)**

| GUI要素 | 種類 | 説明 |
|---------|------|------|
| Twitchユーザー名 | TextBox (`twitchUser`) | ログインユーザー |
| OAuth トークン | TextBox (`twitchPassword`) | 認証トークン |
| 配信者ID | TextBox (`twitchJoinCh`) | 接続先チャンネル |
| 転送パターン | TextBox (`TransferFormat`) | メッセージフォーマット |
| トーク転送有効 | CheckBox (`useTalkTransfer`) | 転送ON/OFF |

**転送パターン変数**:
- `%T0～%T4`: 翻訳文 (Text)
- `%L0～%L4`: 言語名 (Language Name)
- `\n`: 改行 (Enter)

**デフォルト**: `/me %T0 \n %T1 (%L0>%L1)`

**ボタン操作**:
- `接続認証(Get a OAuth)`: OAuth取得ページへ
- `接続`: チャット接続
- `切断`: 接続解除

**GroupBox: 要約設定**

| GUI要素 | 種類 | 説明 |
|---------|------|------|
| 要約を有効にする | CheckBox (`useSummary`) | 要約機能ON |
| 要約行数 | NumericUpDown (`useSummaryLines`) | 対象行数 |
| 要約サイクル時間 | NumericUpDown (`SummaryCycleTime`) | 更新間隔(分) |
| 要約フォーマット | TextBox (`summaryFormat`) | 出力形式 |
| 翻訳で要約 | CheckBox (`useSummaryWithTranslate`) | 翻訳版要約 |

---

## VR/Metaverse Plugins

### Plugin_VRCHAT_OSC - VRChat OSC連携
**Purpose**: VRChat avatar control via OSC

#### ConfigWindow構造: 3タブ構成

**GroupBox: VRChat → NEO**

| GUI要素 | 種類 | デフォルト | 説明 |
|---------|------|------------|------|
| ポート番号 | NumericUpDown (`VMCPort`) | 9001 | 受信ポート |
| 接続 | Button (`btVMCConnect`) | - | 受信開始 |
| 切断 | Button (`btVMCDisconnect`) | - | 受信停止 |

**GroupBox: NEO → VRChat**

| GUI要素 | 種類 | デフォルト | 説明 |
|---------|------|------------|------|
| 送信先アドレス | TextBox (`VMCSendIP_YNC`) | 127.0.0.1 | VRChat IP |
| 送信ポート | NumericUpDown (`VMCSendPort_YNC`) | 9000 | OSCポート |

**タブ1: VRChat - チャット送信設定**

| GUI要素 | 種類 | 説明 |
|---------|------|------|
| 母国語送信 | CheckBox (`vrchatSendText1`) | Native送信 |
| 翻訳送信 | CheckBox (`vrchatSendText2`) | 翻訳送信 |
| 翻訳1～4 | CheckBox (`Trans1`～`Trans4`) | 各言語選択 |
| VRChat音声ミュート連動 | CheckBox (`linkingMute`) | ミュート同期 |
| 左ジェスチャー連動 | CheckBox (`linkingStyle`) | ジェスチャー同期 |
| 確定結果のみ送信 | CheckBox (`sendOnlyFixed`) | 途中結果除外 |
| テスト送信 | Button (`SendTest`) | 動作確認 |

**GroupBox: オプション**

| GUI要素 | 種類 | 説明 |
|---------|------|------|
| 対象ユーザ名リスト | TextBox (Multiline, `IncludingUser`) | フィルタ対象 |

**タブ3: Option - ルール/変換ルール**

DataGridView (`DicFix`) で条件設定:

| 列名 | 種類 | 説明 |
|------|------|------|
| 有効(Enabled) | CheckBox | ルール有効化 |
| モード(Mode) | ComboBox | マッチング方式 |
| 対象(Target) | ComboBox | 判定対象言語 |
| キーワード(Phrase) | TextBox | トリガー文字列 |
| OSCアドレス | TextBox | 送信先アドレス |
| パラメータ(Parameter) | TextBox | OSC値 |
| 対象者(TargetName) | TextBox | ユーザー名 |
| ExternalCallTag | TextBox | 外部呼び出しタグ |

**タブ2: YNC Msg - YNCMessage設定**

| GUI要素 | 種類 | 説明 |
|---------|------|------|
| 母国語送信 | CheckBox (`vmcSendText1`) | VMC Native |
| 翻訳言語送信 | CheckBox (`vmcSendText2`) | VMC翻訳 |
| 送信タイプを整数で指定 | CheckBox (`SendInt`) | Int型送信 |

---

### Plugin_VCas - VirtualCast連携
**Purpose**: VirtualCast integration

#### ConfigWindow構造: 複数タブ + GroupBox

**GroupBox: VMC接続設定**

| GUI要素 | 種類 | 説明 |
|---------|------|------|
| ローカルポート | NumericUpDown (`VMCPort`) | 受信ポート |
| 接続 | Button (`btVMCConnect`) | 接続開始 |
| 切断 | Button (`btVMCDisconnect`) | 接続解除 |

**GroupBox: VMC送信設定**

| GUI要素 | 種類 | 説明 |
|---------|------|------|
| VMC送信IP | TextBox (`VMCSendIP_YNC`) | 送信先IP |
| VMC送信ポート | NumericUpDown (`VMCSendPort_YNC`) | 送信ポート |

**タブ: VCas設定**

| GUI要素 | 種類 | 説明 |
|---------|------|------|
| VCas送信テキスト1 | CheckBox (`VCasSendText1`) | Native送信 |
| VCas送信テキスト2 | CheckBox (`VCasSendText2`) | 翻訳送信 |
| 翻訳1～4 | CheckBox (`Trans1`～`Trans4`) | 言語選択 |
| ユーザー指定 | TextBox (`IncludingUser`) | フィルタ |
| テスト送信 | Button (`SendTest`) | 動作確認 |

**タブ: ファイル設定**

| GUI要素 | 種類 | 説明 |
|---------|------|------|
| 設定読み込み | Button (`ConfigLoad`) | 設定復元 |
| 設定保存 | Button (`ConfigSave`) | 設定保存 |

---

## Text Processing Plugins

### Plugin_Dictionary - 辞書プラグイン
**Purpose**: Word/phrase replacement using dictionary

#### ConfigWindow構造: 複数GroupBox + テスト領域

**GroupBox: 音声認識後の補正 (After voice recognition)**

| GUI要素 | 種類 | 説明 |
|---------|------|------|
| 辞書ファイルパス | TextBox (`Dictionary2Name`) | CSVファイルパス |
| ファイル選択 | Button (`SelectDictionary2`) | ファイル選択ダイアログ |
| 保存(Save) | Button (`EditCSV_After`) | 変更保存 |
| リロード(Reload) | Button (`Reload1`) | 再読み込み |

DataGridView (`ReplaceWordsRecogList`):

| 列名 | 種類 | 説明 |
|------|------|------|
| ItemFrom | TextBox | 置換元 |
| ItemTo | TextBox | 置換先 |

**GroupBox: 対訳辞書 (bilingual dictionary)**

| GUI要素 | 種類 | 説明 |
|---------|------|------|
| 対訳辞書ファイルパス | TextBox (`Dictionary1Name`) | CSVファイルパス |
| ファイル選択 | Button (`SelectDictionary1`) | ファイル選択 |
| 編集(Edit) | Button (`EditCSV_Bilingual`) | 外部エディタで開く |
| リロード(Reload) | Button (`Reload2`) | 再読み込み |

**追加オプション**

| GUI要素 | 種類 | 説明 |
|---------|------|------|
| 翻訳注釈を取り除く | CheckBox (`DeepLFixed`) | DeepL注釈削除 |
| 置換処理の精度向上 | CheckBox (`ReplaceAssist`) | マッチング改善 |
| 共用NGワード辞書を適用 | CheckBox (`NGWordDic`) | NG辞書有効化 |
| NG辞書更新 | Button (`dictionaly_update`) | 辞書更新 |

**GroupBox: 辞書のテスト (Trial Run)**

| GUI要素 | 種類 | 説明 |
|---------|------|------|
| 入力文章 | TextBox (`Text_Input`) | テスト入力 |
| テスト実行 | Button (`TrialRun`) | 変換実行 |
| 翻訳前テキスト | TextBox (ReadOnly) | 変換結果 |
| 翻訳後テキスト1～4 | TextBox (ReadOnly) | 各言語結果 |

---

### Plugin_RegExp - 正規表現プラグイン
**Purpose**: Regex-based text transformation

#### ConfigWindow構造: 3つのGroupBox

**GroupBox: 辞書 / Conversion Rule**

DataGridView (`DicFix`) で正規表現ルール管理:

| 列名 | 種類 | 選択肢/説明 |
|------|------|-------------|
| 有効(Enabled) | CheckBox | ルール有効化 |
| 対象(Target) | ComboBox | 母国語/翻訳1～4 |
| 置換前(before) | TextBox | 正規表現パターン |
| 置換後(after) | TextBox | 置換文字列 |
| モード(mode) | ComboBox | 削除/置換/全体置換/クリア |

**モード選択肢**:
- `1:一致部の削除(DELETE)`: マッチ部分を削除
- `2:一致部の置換(REPLACE)`: マッチ部分を置換
- `3:全体の置換(REPLACEALL)`: テキスト全体を置換
- `4:クリア(CLEAR)`: テキストをクリア

**右クリックメニュー**: 行の挿入/入れ替え/削除

**GroupBox: 動作テスト (Operation test)**

| GUI要素 | 種類 | 説明 |
|---------|------|------|
| 対象(Target) | ComboBox (`conversionMode`) | テスト対象言語 |
| 入力(Input) | TextBox (`Test_Input`) | テスト文字列 |
| 結果(Result) | TextBox (`Test_Result`) | 変換結果 |
| 実行 | Button (`Test_Run`) | テスト実行 |

**GroupBox: ファイル (File)**

| GUI要素 | 種類 | 説明 |
|---------|------|------|
| ゆかりねっとから読み込み | Button (`ImportRun`) | 既存設定インポート |
| 読み込み(Import) | Button (`settingImport`) | 設定ファイル読込 |
| 書き出し(Export) | Button (`settingExport`) | 設定ファイル保存 |

---

### Plugin_HotKey - ホットキー対応
**Purpose**: Global keyboard shortcut triggers

#### ConfigWindow構造: 単一GroupBox + DataGridView

**GroupBox: 条件 (operating conditions)**

DataGridView (`dgv_Sound`) でホットキー設定:

| 列名 | 種類 | 選択肢/説明 |
|------|------|-------------|
| モード(S_Patern) | ComboBox | 完全/一部/消去時/無効 |
| 判定対象言語(JudgeTarget) | ComboBox | 判定対象 |
| 起動キーワード(S_Keyword) | TextBox | トリガー文字列 |
| 送信キー(SendKey) | TextBox | 送信するキー |
| 文字差し替え(S_ReplaceWord) | CheckBox | 置換有効 |
| 読み上げ文字(S_TalkWord) | TextBox | 置換後テキスト |
| 後処理(S_Post) | CheckBox | 後処理フラグ |
| TTS無効化(s_NoSpeak) | CheckBox | 読み上げスキップ |
| 対象者名(TargetName) | TextBox | ユーザー指定 |

**CSV操作パネル**:

| GUI要素 | 種類 | 説明 |
|---------|------|------|
| ロード(Load) | Button (`openCSV`) | CSV読み込み |
| セーブ(Save) | Button (`saveCSV`) | CSV保存 |
| クリア(All Clear) | Button (`clearCSV`) | 全削除 |

---

## AI/Cloud Plugins

### Plugin_GPT3 - ChatGPT/GPT統合
**Purpose**: OpenAI GPT integration for text generation

#### ConfigWindow構造: 7タブ構成

**共通設定 - GPTオプション**

| GUI要素 | 種類 | 説明 |
|---------|------|------|
| モデル選択 | ComboBox (`GPT3Model`) | gpt-4, gpt-3.5-turbo等 (37種類) |
| 画像生成モデル | ComboBox (`GPT3ModelImage`) | dall-e-2, dall-e-3等 |
| APIページを開く | Button (`openAPIPage`) | OpenAI設定ページ |

**タブ1: 加工 (Convert)**

| GUI要素 | 種類 | 説明 |
|---------|------|------|
| 文章加工有効 | CheckBox (`EffectMessage`) | 機能ON/OFF |
| プロンプト設定 | TextBox (Multiline, `ConvertPrompt`) | 変換指示 |
| AI役割設定 | TextBox (Multiline, `ConvertRole`) | システムプロンプト |
| パラメータ(JSON) | TextBox (Multiline, `ConvertPromptParam`) | API設定 |
| 実行下限文字数 | NumericUpDown (`EffectMessageUnderChars`) | 最小文字数 |
| 過去結果を読み込む | CheckBox (`useHistoryData_Conv`) | 履歴使用 |

**タブ2: マスク (Filter)**

| GUI要素 | 種類 | 説明 |
|---------|------|------|
| フィルタリング有効 | CheckBox (`MaskWord`) | 機能ON/OFF |
| 悪口フィルタ | CheckBox (`MaskWord_Hate`) | Hate filter |
| 性的表現フィルタ | CheckBox (`MaskWord_Sexual`) | Sexual filter |
| 暴力フィルタ | CheckBox (`MaskWord_Violence`) | Violence filter |
| 自傷フィルタ | CheckBox (`MaskWord_SelfHarm`) | Self-harm filter |
| 閾値(%) | NumericUpDown (`GPT3_Threthold`) | 検出感度 |

**タブ3: 画像 (Image)**

| GUI要素 | 種類 | 説明 |
|---------|------|------|
| 画像生成有効 | CheckBox (`MakePicture`) | 機能ON/OFF |
| 起動ワード | TextBox (`MakePictureWord`) | トリガー文字列 |
| 画像サイズ | ComboBox (`GPT3PictureSize`) | 256x256～1024x1792 |
| クリアタイミング | RadioButton | 消さない/時間経過で消す |
| 表示時間(秒) | TextBox (`RemainTimer`) | 表示秒数 |
| 写真画面表示 | Button (`ShowImageWindow`) | 画像ウィンドウ表示 |
| 自動で写真画面を開く | CheckBox (`autoOpenPictureWindow`) | 自動表示 |

**タブ4: 応答 (Action)**

| GUI要素 | 種類 | 説明 |
|---------|------|------|
| 問い合わせに応じる | CheckBox (`responseQuery`) | 応答機能ON |
| 起動キーワード | TextBox (Multiline, `AITriggerKeyword`) | 反応ワード |
| AI役割プロンプト | TextBox (Multiline, `AIRolePrompt`) | キャラクター設定 |
| 優先指示構文 | TextBox (Multiline, `AIRolePromptHighPriority`) | 強制指示 |
| AI名前 | TextBox (`AIUserName`) | 表示名 |
| VRM_AIに出力 | CheckBox (`outputToVRMAI`) | VRM連携 |
| VRM_AI通信先 | TextBox (`VRMAI_Port`) | 例: 127.0.0.1:5000 |
| 表情をOSC送信 | CheckBox (`useVMC`) | 表情同期 |
| 過去の問い合わせを記憶 | CheckBox (`useHistoryData`) | 会話履歴保持 |

**タブ5: オプション (Option)**

| GUI要素 | 種類 | 説明 |
|---------|------|------|
| 処理言語選択 | ComboBox (`LanguageMode`) | 母国語/翻訳1～4 |
| 無視するプラグイン | CheckedListBox (`IgnorePluginParam`) | スキップ対象 |
| クエリパラメータ | TextBox (Multiline, `ConvertPromptParamQuery`) | API設定 |
| 失敗時メッセージ | TextBox (Multiline, `failsMessage`) | 例: 「・・・。」 |

**タブ6: 提案 (Suggest)**

| GUI要素 | 種類 | 説明 |
|---------|------|------|
| 提案ページを開く | Button (`openSuggestWnd`) | 提案ウィンドウ表示 |
| 提案者の役割 | TextBox (Multiline, `SuggestRole`) | 提案プロンプト |
| 対象行数 | NumericUpDown (`SuggestTargetLine`) | 分析対象行 (デフォルト25) |

**タブ7: 拡張 (Fn)**

| GUI要素 | 種類 | 説明 |
|---------|------|------|
| 機能選択 | CheckedListBox (`GPTFunctionCallList`) | Wikipedia_JP/EN/Wiki等 |
| Wiki URL設定 | TextBox (`WikiAccessURL`) | Wiki API URL |

---

### Plugin_HTTPCall - HTTP呼び出し
**Purpose**: Generic HTTP request trigger

#### ConfigWindow構造: 単一GroupBox

**GroupBox: ルール / Conversion Rule**

DataGridView (`DicFix`) でHTTPルール管理:

| 列名 | 種類 | 説明 |
|------|------|------|
| 有効(Enabled) | CheckBox | ルール有効化 |
| モード(Mode) | ComboBox | 完全/一部 |
| 判定対象(Target) | ComboBox | 母国語/翻訳1～4 |
| 起動フレーズ(Phrase) | TextBox | トリガー文字列 |
| コールURL | TextBox | リクエストURL |
| 対象者(TargetName) | TextBox | ユーザー指定 |
| API用タグ(ExternalCallTag) | TextBox | 外部呼び出しタグ |

---

### Plugin_Notion - Notion連携
**Purpose**: Notion database/page integration

#### ConfigWindow構造: シンプル(単一GroupBox)

**GroupBox: Notion設定 (Setting)**

| GUI要素 | 種類 | 説明 |
|---------|------|------|
| Secret Key | TextBox (`NotionSecret`) | APIシークレット (マスク表示) |
| 転送親ノートURL | TextBox (`TransferTo`) | NotionページURL |

---

### Plugin_TalkHistory - 会話履歴管理
**Purpose**: Conversation logging and MCP server

#### ConfigWindow構造: 4つのGroupBox

**GroupBox: 会話履歴データ管理**

| GUI要素 | 種類 | 説明 |
|---------|------|------|
| 保存済み会話数 | Label (`labelDataCount`) | 統計表示 |
| データをインポート | Button (`buttonImport`) | ファイル読込 |
| データをエクスポート | Button (`buttonExport`) | ファイル保存 |
| 全データ削除 | Button (`buttonClearData`) | 削除 (赤ボタン) |

**GroupBox: 会話履歴一覧**

| GUI要素 | 種類 | 説明 |
|---------|------|------|
| 会話一覧 | ListBox (`listBoxConversations`) | セッション一覧 |
| 会話削除 | Button (`buttonDeleteConversation`) | 選択削除 |
| サマリー生成 | Button (`buttonGenerateSummary`) | 要約作成 |
| アドバイス生成 | Button (`buttonGenerateAdvice`) | 助言作成 |

**GroupBox: 詳細表示**

| GUI要素 | 種類 | 説明 |
|---------|------|------|
| 詳細内容 | RichTextBox (`textBoxDetails`) | 選択会話の内容 |

**GroupBox: 検索**

| GUI要素 | 種類 | 説明 |
|---------|------|------|
| 検索キーワード | TextBox (`textBoxSearch`) | 検索文字列 |
| 検索実行 | Button (`buttonSearch`) | 検索開始 |
| 検索結果 | ListBox (`listBoxSearchResults`) | 結果一覧 |

---

## Utility Plugins

### Plugin_Exporter - データエクスポート
**Purpose**: Export captions to files

#### ConfigWindow構造: 複数GroupBox + ステータスバー

**エクスポート形式ボタン群**:

| ボタン | 出力形式 |
|--------|----------|
| ExportSRT | SRT字幕 |
| ExportSTL | STL字幕 |
| ExportXML | XML |
| ExportOxk | OXK |
| ExportText | プレーンテキスト |
| ExportAviUtil | AviUtl用 |
| ExportSAMI | SAMI字幕 |
| ExportVTT | WebVTT |
| ExportSubViewer | SubViewer |
| ExportRecotteStudio | Recotte Studio用 |
| ExportSRV3 | SRV3 |
| ExportYMM4 | ゆっくりMovieMaker4用 |

**GroupBox: 出力設定**

| GUI要素 | 種類 | 説明 |
|---------|------|------|
| タイムオフセット | NumericUpDown (`OffsetTime`) | オフセット(ms) |
| 表示時間 | NumericUpDown (`ShownTime`) | 表示秒数 |
| 最小表示時間 | NumericUpDown (`TimerUnderLimit`) | 下限(ms) |
| 時間モード | CheckBox (`TimeMode1`) | 時間形式選択 |
| タイム0オフセット | CheckBox (`ExportTimeZeroOfs`) | ゼロ基準 |

**GroupBox: EXO出力設定** (AviUtl用)

| GUI要素 | 種類 | 説明 |
|---------|------|------|
| レイヤー番号 | NumericUpDown (`LayerNo`) | レイヤー1 |
| 表示幅/高さ | NumericUpDown | サイズ設定 |
| 位置X/Y | NumericUpDown | 配置座標 |
| レイヤー番号2 | NumericUpDown (`LayerNo2`) | レイヤー2 |
| 位置X2/Y2 | NumericUpDown | 座標2 |

**GroupBox: フォント設定**

| GUI要素 | 種類 | 説明 |
|---------|------|------|
| 言語選択 | ComboBox (`LanguageName`) | 対象言語 |
| フォント1/2 | ComboBox | フォントファミリー |
| フォントサイズ1/2 | NumericUpDown | サイズ設定 |

**GroupBox: 色設定**

| GUI要素 | 種類 | 説明 |
|---------|------|------|
| 前景色 | Panel (`fore_exo_color`) | 文字色選択 |
| 影色 | Panel (`shadow_exo_color`) | 影色選択 |

**その他**:
- `ClearData`: データクリア
- `SaveLog`: ログ保存チェック
- `ResultText`: 処理状況表示(ステータスバー)

---

## 共通UI操作パターン

### DataGridViewの操作
多くのプラグインで条件・ルール設定に使用:

1. **行の追加**: 最下行の空行に入力
2. **行の編集**: セルをクリックして直接編集
3. **行の削除**: 右クリック→「削除」
4. **行の並べ替え**: 右クリック→「上/下と入れ替え」
5. **行の挿入**: 右クリック→「上/下に挿入」

### CSV入出力
Plugin_PlaySound, Plugin_HotKey, Plugin_RegExp等で使用:

1. **ロード(Load)**: CSVファイルから設定を読み込み
2. **セーブ(Save)**: 現在の設定をCSVに保存
3. **クリア(All Clear)**: 全ルールを削除

### 接続系プラグインの操作
Plugin_Discord, Plugin_OBS5, Plugin_VRCHAT_OSC等:

1. 接続情報(IP/Port/Token等)を入力
2. 「接続」ボタンで接続開始
3. ステータスバー/パネルで接続状態確認
4. 「切断」ボタンで接続解除

### テスト機能
Plugin_Dictionary, Plugin_RegExp等:

1. テスト入力欄にサンプル文字列を入力
2. 「実行」ボタンでテスト実行
3. 結果欄で変換結果を確認

---

## プラグイン別公式ドキュメント

### 読み上げ系
- [読み上げ](../plugin/plugin_playvoice.md)
- [棒読みちゃん連携](../plugin/plugin_bouyomi.md)

### 配信連携系
- [OBS連携 WSv5](../plugin/plugin_OBS5.md) (OBS28以降)
- [OBS連携 WSv4](../plugin/plugin_OBS.md) (OBS27以前)
- [配信ソフト向けテキスト出力](../plugin/plugin_OBSFile.md)

### VR/メタバース系
- [VRChat OSC連携](../plugin/plugin_vrchat_osc.md)
- [バーチャルキャスト連携](../plugin/plugin_vcas.md)
- [VRオーバーレイ](../plugin/plugin_vroverlay.md)

### プラットフォーム連携系
- [Discord BOT連携](../plugin/plugin_dicord.md)
- [Discord Webhook連携](../plugin/plugin_dicordwebhook.md)
- [Twitch連携](../plugin/plugin_twitch.md)
- [YouTube Live字幕送信](../plugin/plugin_youtube.md)

### テキスト処理系
- [辞書](../plugin/plugin_dictionary.md)
- [正規表現](../plugin/plugin_regexp.md)
- [GPT3整形/AIアシスタント](../plugin/plugin_GPT3.md)

### API/ツール系
- [HTTPコール](../plugin/plugin_httpcall.md)
- [WebSocketコール](../plugin/plugin_wscall.md)
- [ファイル出力](../plugin/plugin_exporter.md)

---

## 関連ドキュメント

- [INDEX](./INDEX.md) - 全体案内
- [クイックスタートシナリオ](./QUICKSTART_SCENARIOS.md) - ユースケース別設定例
- [設定リファレンス](./SETTINGS_REFERENCE.md) - 全設定項目の詳細
- [GUIリファレンス](./YNC_NEO_GUI_REFERENCE.md) - 本体GUI操作
- [公式: プラグインの使い方](../plugin/enabled.md)
- [公式: プラグイン一覧](../plugin/index.md)
