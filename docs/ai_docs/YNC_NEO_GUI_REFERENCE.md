# ゆかコネNEO 本体GUIリファレンス

> YNC_Neo本体の設定画面（MainWindow.xaml）のGUI構造と各設定項目の効果をまとめたリファレンスです。

**公式ドキュメント**: [標準設定項目](../startup/startup_basic.md) / [オプション設定](../startup/startup_option.md)

---

## 画面構成概要

YNC_Neoのメイン画面は以下の構造で構成されています：

```
┌─────────────────────────────────────┐
│ タイトルバー（ドラッグ移動可能）      │
├─────────────────────────────────────┤
│ ☰ ハンバーガーメニュー │ ツールバー   │
├─────────────────────────────────────┤
│                                     │
│   メインコンテンツエリア              │
│   （設定パネル / プレビュー）         │
│                                     │
└─────────────────────────────────────┘
```

## ハンバーガーメニュー構造

左側のメニューから各設定セクションにアクセスできます：

### 共通設定 (Setting_Common)
| メニュー項目 | アイコン | 対応セクション |
|-------------|---------|---------------|
| ガイドページ | AboutOutline | ガイドウィンドウ |
| プロファイル | AccountVoice | ExpandProfile |
| 認識ソース選択 | Microphone | ExpandRecognitionSelect |
| 共通設定 | Gift | ExpandCommonSetting |
| 翻訳設定 | TranslateVariant | ExpandTranslate |
| プラグイン一覧 | PowerPlug | TitlePanelPlugin |

### レイアウト設定 (Setting_forLayout)
| メニュー項目 | アイコン | 対応セクション |
|-------------|---------|---------------|
| 表示レイアウト | DockWindow | ExpandShowLayout |
| 表示タイミング | ClockEditOutline | ExpandShowTiming |
| 母国語表示設定 | Translate | ExpandNativeCaption |
| フォント設定 | FormatFont | ExpandFontSetting |
| 色設定 | PaletteOutline | ExpandColorSettings |

### オプション設定 (Setting_Option)
| メニュー項目 | アイコン | 対応セクション |
|-------------|---------|---------------|
| ブラウザ設定 | Wrench | OptionWindow2 |
| 翻訳オプション | Connection | OptionWindow3 |
| ネットワーク設定 | Network | OptionWindow4 |
| フォルダ設定 | Folder | OptionWindow5 |
| 起動設定 | ToDo | OptionWindow6 |

### その他
| メニュー項目 | アイコン | 機能 |
|-------------|---------|------|
| スマート設定 | Wrench | 自動設定ウィザード |
| デザイン保存 | UsbFlashDriveOutline | 設定バックアップ |
| 全設定表示 | Show | 全設定パネルを展開 |
| 手動入力 | KeyboardOutline | テキスト手動入力 |
| ヘルプ | ChatQuestionOutline | ヘルプ表示 |
| 診断チェック | Check | システム診断 |
| レポート | MotherNurse | 問題報告 |
| ログ出力 | ZipBox | ログファイル生成 |

---

## 設定セクション詳細

### 1. プロファイル設定 (ExpandProfile)

**目的**: ユーザー情報と基本言語設定

| GUI要素 | x:Name | 種類 | 効果 |
|---------|--------|------|------|
| あなたの母国語 | `NativeLanguage` | ComboBox | 音声認識・字幕表示の基準言語を設定 |
| 話者名 | `TalkerName` | TextBox | 字幕に表示される話者名を設定 |
| 翻訳言語逆方向 | `CanInvertTranslation2` | CheckBox | 翻訳の方向を反転（外国語→母国語に変更） |

**NativeLanguage選択時の効果**:
- 音声認識エンジンの言語モデルが変更される
- 翻訳元言語として設定される
- 字幕の「母国語」表示に反映される

---

### 2. 音声認識ソース選択 (ExpandRecognitionSelect)

**目的**: 音声入力ソースの選択

| GUI要素 | x:Name | 種類 | 効果 |
|---------|--------|------|------|
| Chrome認識 | `UseChrome` | RadioButton | Google Chromeの音声認識APIを使用 |
| Edge認識 | `UseEdge` | RadioButton | Microsoft Edgeの音声認識APIを使用 |
| VOSK | `UseVOSK` | RadioButton | オフライン音声認識（VOSKエンジン）を使用 |
| UDtalk | `UseUDtalk` | RadioButton | UDtalkサーバーからの音声入力を使用 |
| Yukarinette | `UseYukarinette` | RadioButton | ゆかりねっとConnectorからの入力を使用 |
| Whisper | `UseWhisper` | RadioButton | OpenAI Whisperを使用 |
| Yukane | `UseYukane` | RadioButton | Yukaneエンジンを使用 |

**選択による効果**:
- Chrome/Edge: ブラウザウィンドウが開き、Web Speech APIで認識
- VOSK: ローカルでオフライン認識（ネットワーク不要）
- UDtalk: スマートフォンアプリと連携
- Yukarinette: ゆかりねっとConnectorとの連携モード
- Whisper: 高精度なAI音声認識

**関連設定**:

| GUI要素 | x:Name | 種類 | 効果 |
|---------|--------|------|------|
| ゆかりねっと拡張 | `UseYukarinetteExtend` | CheckBox | 追加の連携機能を有効化 |
| Web認識拡張 | `UseWebRecogExtend` | CheckBox | Web認識の拡張機能を有効化 |
| ChatGPT修正 | `UseHotFixChatGPT` | CheckBox | ChatGPTによる認識結果の修正 |
| 自動ウィンドウ表示 | `isAutoOpenInWindow` | CheckBox | 認識開始時に自動でウィンドウを開く |
| 新認識プログラム | `isNewRecognitionPrg` | CheckBox | 新しい認識エンジンを使用 |

**タイミング設定**:

| GUI要素 | x:Name | 種類 | 範囲 | 効果 |
|---------|--------|------|------|------|
| 分割補助タイミング | `rb_Plugin_DivideAssistTiming` | Slider | - | テキスト分割のタイミング（ミリ秒） |

---

### 3. 翻訳設定 (ExpandTranslate)

**目的**: 翻訳言語と翻訳エンジンの設定

#### 翻訳先言語選択

| GUI要素 | x:Name | 種類 | 効果 |
|---------|--------|------|------|
| 翻訳言語1 | `TranslationLanguage1` | ComboBox | 1番目の翻訳先言語を選択 |
| 翻訳言語2 | `TranslationLanguage2` | ComboBox | 2番目の翻訳先言語を選択 |
| 翻訳言語3 | `TranslationLanguage3` | ComboBox | 3番目の翻訳先言語を選択 |
| 翻訳言語4 | `TranslationLanguage4` | ComboBox | 4番目の翻訳先言語を選択 |

#### 翻訳エンジン選択

| GUI要素 | x:Name | 種類 | 選択肢 |
|---------|--------|------|--------|
| 翻訳エンジン1 | `Translator1` | ComboBox | 下記参照 |
| 翻訳エンジン2 | `Translator2` | ComboBox | 下記参照 |
| 翻訳エンジン3 | `Translator3` | ComboBox | 下記参照 |
| 翻訳エンジン4 | `Translator4` | ComboBox | 下記参照 |

**翻訳エンジン一覧**:

| エンジン名 | 特徴 | APIキー必要 |
|-----------|------|-------------|
| Google Translate | 高品質、多言語対応 | 要（有料） |
| Google Translate Free | 無料版、制限あり | 不要 |
| Google Translate V3 | 最新API | 要（有料） |
| Microsoft Translator | Azure翻訳 | 要（有料） |
| DeepL Pro | 高品質翻訳 | 要（有料） |
| DeepL Free | 無料版DeepL | 要（無料枠） |
| Amazon Translate (Asia/EU) | AWS翻訳 | 要（有料） |
| IBM Translator | Watson翻訳 | 要（有料） |
| NAVER Translator | Papago | 要 |
| GPT-3 | OpenAI翻訳 | 要（有料） |
| GPT-4o | 最新GPT | 要（有料） |
| GPT-4o Mini | 軽量GPT | 要（有料） |
| Gemini | Google AI | 要 |
| Gemini 2.5 Flash Lite | 高速版 | 要 |
| Claude | Anthropic AI | 要（有料） |
| Grok | xAI | 要 |
| OpenRouter | 複数AI統合 | 要 |
| Tencent Translator | 中国語特化 | 要 |
| BAIDU Translator | 中国語特化 | 要 |
| Alibaba Translator | 中国語特化 | 要 |
| Custom Translator | カスタム設定 | 設定による |
| TransOFF | 翻訳無効 | 不要 |

---

### 4. 共通設定 (ExpandCommonSetting)

**目的**: アプリケーション全体の動作設定

| GUI要素 | x:Name | 種類 | 効果 |
|---------|--------|------|------|
| 発話結合 | `UseJoinSubUtterance` | CheckBox | 短い発話を結合して表示 |

---

### 5. レイアウト設定 (ExpandShowLayout)

**目的**: 字幕表示のレイアウトテンプレート選択

| GUI要素 | x:Name | 種類 | 効果 |
|---------|--------|------|------|
| レイアウトプリセット | `LayoutData` | ComboBox | プリセットレイアウトを選択 |
| 外部ウィンドウ自動開く | `isAutoOpenExWindow` | CheckBox | キャプションウィンドウを自動で開く |
| キャプション表示 | `ShowInnerBrowser2` | Button | キャプションウィンドウを表示 |
| OBSに転送 | `LayoutToOBSLocal` | Button | レイアウト設定をOBSに送信 |
| テンプレートフォルダ | `openTemplateFolder` | Button | カスタムテンプレートフォルダを開く |

**レイアウトプリセット一覧** (SettingPreset.jsonより):

| プリセット名 | LayoutID | 用途 |
|-------------|----------|------|
| リスト 1列 | 8 | シンプルな1列表示 |
| リスト 2列 | 16 | 2列並列表示 |
| 多国語 | 9 | 複数言語を縦に並べて表示 |
| スマート表示 | 8 | 中央揃えスマート表示 |
| 海外ドラマ | 0 | 映画字幕風の下部表示 |
| 海外ドラマ・リスト | 1 | ドラマ風リスト表示 |
| ゲームメッセージ | 2 | ゲームのメッセージボックス風 |
| トークセッション | 12 | トーク番組風表示 |
| 電光掲示板 | 8 | スクロール表示 |

---

### 6. 表示タイミング設定 (ExpandShowTiming)

**目的**: 字幕の表示時間とスクロール速度

| GUI要素 | x:Name | 種類 | 範囲 | 効果 |
|---------|--------|------|------|------|
| 表示保持時間 | `KeepTime` | Slider | 1～30秒 | 字幕が消えるまでの時間 |
| 保持時間入力 | `KeepTimeValue` | TextBox | - | 保持時間の直接入力 |
| スクロール時間 | `ScrollTime` | Slider | 1～30秒 | スクロールアニメーション時間 |
| スクロール入力 | `ScrollTimeValue` | TextBox | - | スクロール時間の直接入力 |
| クリア待機 | `isWaitClearing` | CheckBox | - | クリア完了を待ってから次を表示 |

**効果の詳細**:
- **KeepTime**: 値が大きいほど字幕が長く表示される。短い配信では3-4秒、読み上げ中心なら6-8秒推奨
- **ScrollTime**: 電光掲示板レイアウト使用時のスクロール速度

---

### 7. フォント設定 (ExpandFontSetting)

**目的**: 字幕のフォントスタイル設定

#### 基本フォント設定

| GUI要素 | x:Name | 種類 | 範囲 | 効果 |
|---------|--------|------|------|------|
| フォントサイズ | `FontSize1` | Slider | 2～200pt | メインテキストのサイズ |
| サイズ入力 | `FontSize1Value` | TextBox | - | サイズの直接入力 |
| フォント種類 | `FontItem` | ComboBox | - | フォントファミリー選択 |
| 左揃え | `TextAlign_Left` | ToggleButton | - | テキストを左寄せ |
| 中央揃え | `TextAlign_Center` | ToggleButton | - | テキストを中央寄せ |
| 右揃え | `TextAlign_Right` | ToggleButton | - | テキストを右寄せ |

#### 拡張フォント設定 (ExtendFontGroup)

言語ごとに異なるフォントを設定する場合に使用:

| GUI要素 | x:Name | 種類 | 効果 |
|---------|--------|------|------|
| 拡張フォント有効 | `ExtendFontAdjust` | CheckBox | 言語別フォント設定を有効化 |
| フォントサイズ2 | `FontSize2` | Slider | 翻訳1のフォントサイズ |
| フォント種類2 | `FontItem2` | ComboBox | 翻訳1のフォント |
| 配置2 | `TextAlign1_*` | ToggleButton | 翻訳1のテキスト配置 |

**推奨設定**:
- 日本語: UD デジタル 教科書体 NK-B、源ノ角ゴシック等
- 英語: Arial、Roboto等
- 中国語: Microsoft YaHei、Noto Sans CJK等
- 韓国語: Malgun Gothic、Noto Sans Korean等

---

### 8. 色設定 (ExpandColorSettings)

**目的**: 字幕の色とスタイル設定

| GUI要素 | x:Name | 種類 | デフォルト | 効果 |
|---------|--------|------|-----------|------|
| テキスト色 | `FontColor_Lang` | Button(ColorPicker) | 白 | 字幕テキストの色 |
| 背景色 | `BackgroundColor` | Button(ColorPicker) | Lime(#00FF00) | 字幕背景色（クロマキー用） |
| 言語別背景色 | `BackgroundColor_Lang` | Button(ColorPicker) | Cyan | 言語ラベルの背景色 |
| 枠線色 | `BorderColor` | Button(ColorPicker) | 黒 | テキスト縁取り色 |
| 枠線色2 | `BorderColorF3` | Button(ColorPicker) | - | 2重縁取りの外側色 |
| 行線色 | `LineColor` | Button(ColorPicker) | - | 区切り線の色 |

**クロマキー設定のヒント**:
- OBSでクロマキー合成する場合は `BackgroundColor` を緑(#00FF00)に設定
- 透過PNGとして使用する場合は `BackgroundColor` の透明度を0に設定

#### 拡張色設定 (ExtendColorGroup)

言語ごとに異なる色を設定:

| GUI要素 | x:Name | 効果 |
|---------|--------|------|
| 拡張色有効 | `ExtendColorAdjust` | 言語別色設定を有効化 |
| 色1-4 | `FontColor1`-`FontColor4` | 各言語のテキスト色 |
| 枠色1-4 | `BorderColor1`-`BorderColor4` | 各言語の縁取り色 |

---

### 9. 母国語表示設定 (ExpandNativeCaption)

**目的**: 母国語（認識テキスト）の表示方法

| GUI要素 | x:Name | 種類 | 効果 |
|---------|--------|------|------|
| 表示モード | `NativeLanguageShow` | ComboBox/RadioButton | 母国語の表示位置・形式 |

**表示モード選択肢**:
- 翻訳の上に表示
- 翻訳の下に表示
- 非表示
- 翻訳と同列に表示

---

### 10. プラグイン一覧 (TitlePanelPlugin)

**目的**: プラグインの有効/無効と優先順位の管理

| GUI要素 | x:Name | 種類 | 効果 |
|---------|--------|------|------|
| 未使用非表示 | `HideNotUsePlugin` | CheckBox | 無効なプラグインを一覧から隠す |
| プラグイン検索 | `SearchPlugin` | TextBox | 名前でプラグインを検索 |
| 設定メニュー | `configurePlugin` | PackIcon | プラグイン設定メニューを表示 |

#### プラグインリスト (DataGrid: PluginList)

| 列 | 操作 | 効果 |
|----|------|------|
| ↑ボタン | `PluginUp` | プラグインの処理優先度を上げる |
| ↓ボタン | `PluginDown` | プラグインの処理優先度を下げる |
| チェックボックス | - | プラグインの有効/無効切り替え |
| 設定ボタン | `PluginConfigCall` | プラグインのConfigWindowを開く |

**プラグイン優先度の効果**:
- 上位のプラグインほど先にテキストを処理
- 辞書置換→正規表現→TTS の順にしたい場合は、その順に並べる

---

### 11. 手動入力 (ExpandManualInput)

**目的**: キーボードからの直接テキスト入力

| GUI要素 | x:Name | 種類 | 効果 |
|---------|--------|------|------|
| 入力欄 | `ManualInput` | TextBox | テキストを入力 |
| 送信 | `SendText` | Button | 入力したテキストを字幕として送信 |

**使用場面**:
- 音声認識がうまくいかない時の手動入力
- 定型文の送信
- テスト・デバッグ

---

### 12. UDtalk設定 (ExpandUDtalkPanel)

**目的**: UDtalkアプリとの連携設定

| GUI要素 | x:Name | 種類 | 効果 |
|---------|--------|------|------|
| ルーム一覧 | `mnu_RoomList` | ListView | 接続可能なUDtalkルームを表示 |
| IPアドレス | `UDtalkIPAddress` | ComboBox | UDtalkデバイスのIPアドレス |
| 招待確認 | `CheckInvitation` | Button | ルームへの招待を確認 |
| 接続 | `ConnectUDtalk` | Button | UDtalkに接続 |
| 切断 | `DisConnectUDtalk` | Button | UDtalkから切断 |

---

## よくある設定パターン

### パターン1: 基本的な配信設定
```
1. プロファイル: 母国語=日本語、話者名=配信者名
2. 認識ソース: Chrome認識
3. 翻訳: 英語(Google Translate)
4. レイアウト: 海外ドラマ
5. 表示時間: 4秒
6. 背景色: 緑(クロマキー用)
```

### パターン2: 多言語配信設定
```
1. プロファイル: 母国語=日本語
2. 認識ソース: Chrome認識 + ChatGPT修正ON
3. 翻訳: 英語、中国語、韓国語(各DeepL/Google)
4. レイアウト: 多国語
5. 拡張フォント: ON(言語別フォント設定)
6. 拡張色: ON(言語別色分け)
```

### パターン3: VRChat配信設定
```
1. 認識ソース: VOSK(オフライン)
2. 翻訳: 英語(GPT-4o)
3. レイアウト: スマート表示
4. プラグイン: Plugin_VRCHAT_OSC有効
5. 表示時間: 6秒(VR内で読む時間確保)
```

### パターン4: 会議録画設定
```
1. 認識ソース: Whisper(高精度)
2. 翻訳: なし(TransOFF)
3. レイアウト: リスト1列
4. プラグイン: Plugin_Exporter有効(SRT出力)
5. 表示時間: 8秒
```

---

## 設定ファイルの場所

| ファイル | 内容 |
|---------|------|
| `user.config` | ユーザー設定（自動保存） |
| `SettingPreset.json` | レイアウトプリセット定義 |
| `languagelist.json` | 言語リスト定義 |
| `FontList.json` | フォントリスト |

---

## トラブルシューティング

### 字幕が表示されない
1. 「認識ソース選択」で正しいソースが選択されているか確認
2. 「キャプション表示」ボタンでウィンドウを開く
3. 「自動ウィンドウ表示」がONになっているか確認

### 翻訳が動作しない
1. 翻訳エンジンが「TransOFF」になっていないか確認
2. 有料エンジンの場合、APIキーが設定されているか確認
3. ネットワーク接続を確認

### フォントが反映されない
1. 「拡張フォント有効」のチェックを確認
2. システムにフォントがインストールされているか確認
3. 設定後、キャプションウィンドウを再表示

### 色が反映されない
1. 「拡張色有効」のチェックを確認
2. カラーピッカーで透明度(Alpha)が0になっていないか確認

---

## 関連ドキュメント

- [INDEX](./INDEX.md) - 全体案内
- [クイックスタートシナリオ](./QUICKSTART_SCENARIOS.md) - ユースケース別設定例
- [設定リファレンス](./SETTINGS_REFERENCE.md) - 全設定項目の詳細
- [プラグインリファレンス](./PLUGINS_REFERENCE.md) - プラグインGUI詳細
- [FAQ・トラブル対応](./FAQ_TROUBLESHOOTING.md) - よくある質問
- [公式: 標準設定項目](../startup/startup_basic.md)
- [公式: オプション設定](../startup/startup_option.md)
- [公式: レイアウト](../startup/startup_layout.md)
