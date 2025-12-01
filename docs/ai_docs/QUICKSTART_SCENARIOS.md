# ゆかコネNEO クイックスタートシナリオ

> ユースケース別の設定パターン集です。
> 詳細な手順や画像付き解説は公式ドキュメントを参照してください。

---

## シナリオ一覧

| シナリオ | 用途 | 難易度 |
|---------|------|--------|
| [1. 基本配信セットアップ](#シナリオ-1-基本配信セットアップ) | OBS+字幕表示 | 簡単 |
| [2. 多言語配信](#シナリオ-2-多言語配信) | 4言語同時翻訳 | 普通 |
| [3. VRChat字幕](#シナリオ-3-vrchat字幕表示) | VRChat OSC連携 | 普通 |
| [4. Discord連携](#シナリオ-4-discord連携) | BOT双方向通信 | やや複雑 |
| [5. 読み上げ(TTS)](#シナリオ-5-読み上げtts) | 音声出力 | 簡単 |
| [6. アクセシビリティ字幕](#シナリオ-6-アクセシビリティ字幕) | 見やすい字幕 | 簡単 |
| [7. 会議録画・議事録](#シナリオ-7-会議録画議事録) | テキストログ保存 | 普通 |
| [8. Webhook通知](#シナリオ-8-webhook通知) | Slack/Teams連携 | 普通 |
| [9. ホットキー操作](#シナリオ-9-ホットキー操作) | キーボードショートカット | 普通 |
| [10. テキストフィルタ](#シナリオ-10-テキストフィルタ処理) | NGワード・置換 | 普通 |

---

## シナリオ 1: 基本配信セットアップ

**目的**: OBSで日本語字幕+英語翻訳を表示

**公式ドキュメント**: [OBSできれいに出す](../cs/cs_obs.md) / [配信ソフトに取り込む](../cs/cs_import_obs.md)

### 必要な設定

| 設定項目 | 値 | 説明 |
|---------|---|------|
| `NativeLanguage` | 43 | 日本語 |
| `TranslationLanguage1` | 16 | 英語 |
| `Translator1` | 10 | Google翻訳 |
| `LayoutID` | 9 | 多言語レイアウト |
| `BackgroundColor` | #00FF00 | クロマキー用緑 |

### 必要なプラグイン

**Plugin_OBS5** - OBS WebSocket 5.x 連携（OBS28以降）

| 設定 | 値 |
|-----|---|
| Host | 127.0.0.1 |
| Port | 4455 |
| Password | OBSで設定したパスワード |

### セットアップ手順

1. OBS側: ツール → WebSocketサーバー設定 → 有効化
2. NEO側: Plugin_OBS5を有効化、接続情報を設定
3. 背景色を緑(#00FF00)に設定（クロマキー用）
4. OBSでブラウザソースとして取り込み

---

## シナリオ 2: 多言語配信

**目的**: 4言語同時翻訳（日英中韓など）

**公式ドキュメント**: [支援版で高品質翻訳](../cs/cs_en_sp.md)

### 必要な設定

| 設定項目 | 値 | 説明 |
|---------|---|------|
| `NativeLanguage` | 43 | 日本語 |
| `TranslationLanguage1` | 16 | 英語 |
| `TranslationLanguage2` | 49 | 韓国語 |
| `TranslationLanguage3` | 18 | フランス語 |
| `TranslationLanguage4` | 107 | 中国語(簡体) |
| `LayoutID` | 9 | 多言語レイアウト |
| `ShowLangName` | true | 言語名表示 |
| `ExtendFontAdjust` | true | 言語別フォント有効 |
| `ExtendColorAdjust` | true | 言語別色有効 |

### 言語別フォント推奨設定

| 言語 | 設定 | 推奨フォント |
|-----|------|-------------|
| 日本語 | `FontItem` | UD デジタル 教科書体 NK-B |
| 英語 | `FontItem2` | Arial |
| 韓国語 | `FontItem3` | Malgun Gothic |
| 中国語 | `FontItem4` | Microsoft YaHei |

---

## シナリオ 3: VRChat字幕表示

**目的**: VRChatアバター上に字幕を表示

**公式ドキュメント**: [VRChat OSC連携](../plugin/plugin_vrchat_osc.md) / [VRChatのチャットとつなぐ](../cs/cs_vrchat.md)

### 必要なプラグイン設定

**Plugin_VRCHAT_OSC**

| 設定 | 値 | 説明 |
|-----|---|------|
| 送信先アドレス | 127.0.0.1 | ローカル |
| 送信ポート | 9000 | VRChat固定ポート |
| 母国語送信 | true | 日本語を送信 |
| 翻訳送信 | true | 翻訳文を送信 |

### VRChat側の設定

1. アクションメニュー → Options → OSC → Enable
2. 初回は設定後ワールドリロードが必要な場合あり

### 起動順序（重要）

1. **ゆかコネNEO を先に起動**
2. その後 VRChat を起動

### アバターパラメータ制御（オプション）

| パラメータ名 | アドレス | 型 |
|------------|---------|---|
| Talking | /avatar/parameters/Talking | bool |
| Caption | /avatar/parameters/Caption | string |

---

## シナリオ 4: Discord連携

**目的**: Discordチャンネルと双方向連携

**公式ドキュメント**: [Discord BOT連携](../plugin/plugin_dicord.md) / [Discord Webhook連携](../plugin/plugin_dicordwebhook.md)

### 方法A: BOT連携（双方向）

**Discord開発者ポータルでの準備**

1. https://discord.com/developers/applications でアプリ作成
2. BOTを作成、トークンをコピー
3. OAuth2でBOT権限を設定（Send Messages, Read Message History）
4. BOT設定で「Message Content Intent」をON
5. サーバーにBOTを追加

**Plugin_Discord設定**

| 設定 | 値 |
|-----|---|
| ClientID | Discord App Client ID |
| Token | BOTトークン |
| ChannelID | 対象チャンネルID |
| isSend (Discord→NEO) | true |
| isRecv (NEO→Discord) | true |

### 方法B: Webhook連携（一方向、簡単）

**Plugin_DiscordWebhook設定**

| 設定 | 値 |
|-----|---|
| WebhookURL | Discordで生成したWebhook URL |

---

## シナリオ 5: 読み上げ(TTS)

**目的**: 字幕を音声で読み上げ

**公式ドキュメント**: [読み上げ](../plugin/plugin_playvoice.md) / [棒読みちゃん連携](../plugin/plugin_bouyomi.md)

### オプション A: Windows標準TTS

**Plugin_PlayVoice**

| 設定 | 値 |
|-----|---|
| TTS_EngineDevice | SAPI5 |
| TTS_SpeakMode | 母国語/翻訳/両方 |

### オプション B: VOICEVOX

**Plugin_PlayVoice**

| 設定 | 値 |
|-----|---|
| TTS_EngineDevice | VOICEVOX |
| VoicevoxHost | http://127.0.0.1:50021 |
| SpeakerId | 1（ずんだもん等） |

**重要**: VOICEVOX を **先に起動** してから NEO を起動

### オプション C: 棒読みちゃん

**Plugin_Bouyomi**

| 設定 | 値 |
|-----|---|
| BouyoumiMethod | Socket |
| BouyomiPort | 50001 |
| BouyomiID | 0～7 (音声選択) |

**音声ID一覧**: 0=女性1, 1=女性2, 2=男性1, 3=男性2, 4=中性, 5=ロボット, 6=機械

---

## シナリオ 6: アクセシビリティ字幕

**目的**: 聴覚障害のある方向けの見やすい字幕

### 推奨設定

| 設定項目 | 値 | 説明 |
|---------|---|------|
| `LayoutID` | 0 | 海外ドラマ風 |
| `FontItem` | UD デジタル 教科書体 NK-B | 読みやすいフォント |
| `FontSize` | 48 | 大きめサイズ |
| `BorderSize` | 6 | 太めの縁取り |
| `FontColor_Jimaku` | #FFFFFF | 白文字 |
| `BorderColor` | #000000 | 黒縁取り |
| `BackgroundColor_Jimaku` | #80000000 | 半透明黒背景 |
| `KeepTime` | 6 | 長めの表示時間 |
| `rb_Plugin_LineSpan` | 1.5 | 行間を広めに |
| `Alignment_Center` | true | 中央揃え |

### 動的表示時間調整

**Plugin_DynamicKeepTime**

| 設定 | 値 | 説明 |
|-----|---|------|
| BaseTime | 3.0 | 基本表示時間(秒) |
| TimePerChar | 0.15 | 1文字あたり追加(秒) |
| MinTime | 2.0 | 最小表示時間 |
| MaxTime | 12.0 | 最大表示時間 |

---

## シナリオ 7: 会議録画・議事録

**目的**: 字幕をファイルに保存

**公式ドキュメント**: [ファイル出力](../plugin/plugin_exporter.md) / [会話の記録](../plugin/plugin_talkhistory.md)

### ファイル出力

**Plugin_Exporter**

| 出力形式 | 用途 |
|---------|------|
| SRT | 動画編集ソフト用字幕 |
| CSV | Excel等で分析 |
| VTT | Web動画用字幕 |
| YMM4 | ゆっくりMovieMaker4 |
| AviUtl | AviUtl用 |

### 会話履歴保存

**Plugin_TalkHistory**

SQLite形式で会話を保存、検索・エクスポート可能

---

## シナリオ 8: Webhook通知

**目的**: Slack/Teams等に字幕を送信

**公式ドキュメント**: [HTTPコール](../plugin/plugin_httpcall.md) / [Slack Webhook連携](../plugin/plugin_slackwebhook.md)

### Slack

**Plugin_SlackWebHook**

| 設定 | 値 |
|-----|---|
| WebhookURL | Slack Incoming Webhook URL |

### Microsoft Teams

**Plugin_TeamsWebHook**

| 設定 | 値 |
|-----|---|
| WebhookURL | Teams Webhook URL |

### カスタムHTTP

**Plugin_HTTPCall**

任意のAPIエンドポイントにリクエスト送信可能

---

## シナリオ 9: ホットキー操作

**目的**: キーボードショートカットで操作

**公式ドキュメント**: [ホットキー](../plugin/plugin_hotkey.md)

### 設定例

**Plugin_HotKey**

| キー | 修飾キー | アクション |
|-----|---------|----------|
| F1 | Ctrl | ミュート切替 |
| F2 | Ctrl | 字幕クリア |
| F3 | Ctrl | レイアウト変更 |
| 1 | Ctrl+Alt | 定型文送信「こんにちは」 |
| 2 | Ctrl+Alt | 定型文送信「ありがとう」 |

---

## シナリオ 10: テキストフィルタ・処理

**目的**: NGワード除去、テキスト整形

**公式ドキュメント**: [正規表現](../plugin/plugin_regexp.md) / [辞書](../plugin/plugin_dictionary.md)

### NGワードフィルタ

**Plugin_replaceFWords**

| 設定 | 値 |
|-----|---|
| DictionaryFile | badwords.csv |
| ReplacementChar | * |

### 正規表現置換

**Plugin_RegExp**

| 対象 | パターン | 置換後 | 用途 |
|-----|---------|-------|------|
| 母国語 | `\[.*?\]` | (空) | 括弧内削除 |
| 母国語 | `\s+` | (空白1つ) | 連続空白を1つに |

### 辞書置換

**Plugin_Dictionary**

用語統一、読み方修正に使用

---

## トラブルシューティング早見表

### 字幕が表示されない

| 確認項目 | 対処法 |
|---------|--------|
| ミュート状態 | `MuteStatus` がfalseか確認 |
| 入力ソース | 音声認識（UseUDtalk/UseVOSK等）が有効か |
| 翻訳エンジン | `Translator1` が23(無効)でないか |
| 上級者モード | ONの場合、接続確立まで非表示 |

### 翻訳されない

| 確認項目 | 対処法 |
|---------|--------|
| エンジン選択 | `Translator1` が23(無効)でないか |
| APIキー | 有料エンジンは `UseChangeAPIKey_*` と APIキー設定が必要 |
| 文字数制限 | `TransCharCount` で月間上限確認 |
| ネットワーク | インターネット接続確認 |

### OBS連携できない

| 確認項目 | 対処法 |
|---------|--------|
| WebSocket有効 | OBSでWebSocketサーバー有効化 |
| ポート一致 | NEOとOBSで同じポート番号 |
| パスワード一致 | NEOとOBSで同じパスワード |
| OBSバージョン | OBS28以降はPlugin_OBS5、OBS27以前はPlugin_OBS |

### プラグインが動かない

| 確認項目 | 対処法 |
|---------|--------|
| プラグイン有効 | チェックボックスがONか |
| ロード設定 | MaintenanceToolでロード有効か |
| 設定 | プラグイン個別設定を確認 |
| 処理順序 | プラグインの並び順を確認 |
| DLLの場所 | `plugin/` フォルダに配置されているか |

---

## 関連ドキュメント

- [INDEX](./INDEX.md) - 全体案内・ユースケース別ガイド
- [設定リファレンス](./SETTINGS_REFERENCE.md) - 全設定項目の詳細
- [プラグインリファレンス](./PLUGINS_REFERENCE.md) - プラグインGUI詳細
- [FAQ・トラブル対応](./FAQ_TROUBLESHOOTING.md) - よくある質問
- [公式: 5分クイックスタート](../guide/quickstart.md)
- [公式: よくある質問](../qa/faq.md)
- [公式: こんなときは](../qa/troubleshooting.md)
