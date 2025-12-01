# ゆかコネNEO 設定リファレンス

> user.config に保存される全設定項目のリファレンスです。
> GUI操作方法の詳細は [YNC_NEO_GUI_REFERENCE.md](./YNC_NEO_GUI_REFERENCE.md) を参照してください。

**公式ドキュメント**: [標準設定項目](../startup/startup_basic.md) / [オプション設定](../startup/startup_option.md)

---

## 翻訳設定

### 翻訳エンジン選択

| 設定 | 型 | デフォルト | 説明 |
|-----|---|---------|------|
| `Translator1` | int | 10 | 翻訳エンジン1のID |
| `Translator2` | int | 23 | 翻訳エンジン2のID |
| `Translator3` | int | 23 | 翻訳エンジン3のID |
| `Translator4` | int | 23 | 翻訳エンジン4のID |
| `Translator1s`～`Translator4s` | string | "" | カスタム翻訳エンジン名 |

### 翻訳エンジンID一覧

| ID | エンジン名 | 特徴 |
|---|----------|------|
| 10 | Google翻訳 | 高品質、多言語対応 |
| 23 | 無効(TransOFF) | 翻訳しない |
| - | Microsoft Azure | Azure翻訳API |
| - | DeepL | 高品質（支援プラン③以上） |
| - | IBM Watson | Watson翻訳 |
| - | Papago | 韓国語特化 |
| - | GPT-3/4 | OpenAI翻訳 |
| - | Gemini | Google AI |
| - | Claude | Anthropic AI |

**公式ドキュメント**: [無料で英語翻訳を出す](../cs/cs_en.md) / [支援版で高品質翻訳](../cs/cs_en_sp.md)

### APIキー設定

| 設定 | 型 | 説明 |
|-----|---|------|
| `ChangeAPIKey_Google` | string | Google Cloud Translation APIキー |
| `UseChangeAPIKey_Google` | bool | カスタムGoogleキーを使用 |
| `ChangeAPIKey_MS` | string | Microsoft Azure Translatorキー |
| `UseChangeAPIKey_MS` | bool | カスタムMSキーを使用 |
| `SelectAzureRegion` | string | Azureリージョン（例: "japaneast"） |
| `ChangeAPIKey_DeepL` | string | DeepL APIキー |
| `UseChangeAPIKey_DeepL` | bool | カスタムDeepLキーを使用 |
| `ChangeAPIKey_Watson` | string | IBM Watson APIキー |
| `ChangeAPIInst_Watson` | string | Watsonサービスインスタンス |
| `UseChangeAPIKey_Watson` | bool | カスタムWatsonキーを使用 |
| `PAPAGO_APIKEY` | string | Naver Papago APIキー |
| `PAPAGO_APIKEY_ID` | string | Papago APIクライアントID |
| `UseChangeAPIKey_PapagoAPI` | bool | Papago APIを使用 |
| `GPT3_APIKEY` | string | OpenAI APIキー |
| `UseChangeAPIKey_OpenAI` | bool | OpenAI連携を有効化 |
| `GAS_URL` | string | Google Apps Script URL |

**公式ドキュメント**: [GASの設定](../startup/startup_gas.md)

### 言語設定

| 設定 | 型 | デフォルト | 説明 |
|-----|---|---------|------|
| `NativeLanguage` | int | 43 | 母国語ID（43=日本語） |
| `TranslationLanguage1` | int | 16 | 翻訳先言語1（16=英語） |
| `TranslationLanguage2` | int | 107 | 翻訳先言語2（107=中国語簡体） |
| `TranslationLanguage3` | int | 49 | 翻訳先言語3（49=韓国語） |
| `TranslationLanguage4` | int | 18 | 翻訳先言語4（18=フランス語） |
| `NativeLanguageShow` | int | 0 | 母国語表示モード |
| `CanInvertTranslation` | bool | false | 翻訳方向を逆転 |

### 主要言語ID

| ID | 言語 |
|---|------|
| 43 | 日本語 |
| 16 | 英語 |
| 107 | 中国語(簡体) |
| 108 | 中国語(繁体) |
| 49 | 韓国語 |
| 18 | フランス語 |
| 26 | ドイツ語 |
| 73 | スペイン語 |

### 翻訳最適化

| 設定 | 型 | デフォルト | 説明 |
|-----|---|---------|------|
| `EnableTranslationCache` | bool | false | 翻訳キャッシュ有効 |
| `EnableTranslationCacheConstant` | bool | false | 定型句キャッシュ |
| `isSavingUseAPI` | bool | true | API使用統計を保存 |
| `isSavingUseAPI_MAX` | bool | true | API使用量制限 |
| `isAsyncUseAPI` | bool | true | 非同期翻訳リクエスト |
| `TransCharCount` | int | 0 | 翻訳済み文字数 |
| `TransCountMonth` | int | 0 | 今月の翻訳回数 |
| `TransCount` | int | 0 | セッション翻訳回数 |
| `TransCountTotal` | string | "{}" | 累計カウント(JSON) |

---

## 表示設定

### フォント設定

| 設定 | 型 | デフォルト | 説明 |
|-----|---|---------|------|
| `FontItem` | string | "UD デジタル 教科書体 NK-B" | メインフォント |
| `FontItem2`～`FontItem5` | string | "ＭＳ ゴシック" | 言語別フォント |
| `FontSize` | double | 32 | メインフォントサイズ(pt) |
| `FontSize2`～`FontSize5` | double | 17 | 言語別フォントサイズ |
| `ExtendFontAdjust` | bool | false | 言語別フォント設定を有効化 |
| `letterSpacing` | double | 0 | 文字間隔 |

### 色設定

| 設定 | 型 | デフォルト | 説明 |
|-----|---|---------|------|
| `BackgroundColor` | hex | #00FF00 | 背景色（クロマキー用） |
| `FontColor_Jimaku` | hex | #FFFFFF | 字幕テキスト色 |
| `FontColor_Lang` | hex | #FFFFFF | 言語ラベル色 |
| `FontColor1`～`FontColor4` | hex | #FFFFFF | 言語別テキスト色 |
| `BorderColor` | hex | #000000 | テキスト縁取り色 |
| `BorderColor1`～`BorderColor4` | hex | 各種 | 言語別縁取り色 |
| `BackgroundColor_Jimaku` | hex | #0023FF | 字幕背景色 |
| `BackgroundColor_Lang` | hex | #00FFFF | 言語ラベル背景色 |
| `LineColor` | hex | #FFFFFF | 区切り線色 |
| `ExtendColorAdjust` | bool | false | 言語別色設定を有効化 |

### 縁取り・線

| 設定 | 型 | デフォルト | 説明 |
|-----|---|---------|------|
| `BorderSize` | double | 4.25 | 縁取り太さ |
| `BorderSize2` | double | 0 | 二重縁取り太さ |
| `LineWidth` | double | 2 | 区切り線の太さ |

### レイアウト

| 設定 | 型 | デフォルト | 説明 |
|-----|---|---------|------|
| `LayoutID` | int | 13 | レイアウトテンプレートID |
| `SelectLineStyle` | int | 10 | 行スタイルプリセット |
| `ShowCaptionMode` | int | 0 | 字幕表示モード |
| `ShowLangName` | bool | false | 言語名を表示 |
| `Alignment_Left` | bool | false | 左揃え |
| `Alignment_Center` | bool | true | 中央揃え |
| `Alignment_Right` | bool | false | 右揃え |
| `Alignment1`～`Alignment4` | string | "center" | 言語別配置 |

### レイアウトID一覧

| ID | 名前 | 説明 |
|---|------|------|
| 0 | 海外ドラマ | 映画字幕風の下部中央表示 |
| 1 | 海外ドラマ(リスト) | ドラマ風リスト表示 |
| 2 | ゲームメッセージ風 | ゲームのメッセージボックス風 |
| 8 | STD-LIST | 標準リストレイアウト |
| 9 | 多言語 | 複数言語を縦に並べて表示 |
| 12 | トークセッション | トーク番組風表示 |
| 13 | Default | デフォルトレイアウト |
| 16 | STD-GAMEWINDOW-H3 | 2列ゲームレイアウト |

**公式ドキュメント**: [レイアウト](../startup/startup_layout.md)

### 間隔設定

| 設定 | 型 | デフォルト | 説明 |
|-----|---|---------|------|
| `rb_Plugin_LineSpan` | double | 1.05 | 行間倍率 |
| `rb_Plugin_ParagraphSpan` | double | 1.0 | 段落間隔倍率 |
| `windowFrameHeight` | double | 160 | 字幕フレーム高さ |

---

## タイミング設定

| 設定 | 型 | デフォルト | 説明 |
|-----|---|---------|------|
| `KeepTime` | double | 4 | 字幕表示時間(秒) |
| `ScrollTime` | double | 4 | スクロールアニメーション時間(秒) |
| `rb_Plugin_DivideAssistTiming` | double | 3000 | テキスト分割タイミング(ms) |

---

## 入力ソース設定

### UDトーク

| 設定 | 型 | デフォルト | 説明 |
|-----|---|---------|------|
| `UseUDtalk` | bool | false | UDトーク入力を有効化 |
| `UDtalkIPAddress` | string | "127.0.0.1" | UDトークデバイスIP |
| `AddLocalUDtalkIP` | string | "" | 追加UDトークIP |

### その他の入力ソース

| 設定 | 型 | デフォルト | 説明 |
|-----|---|---------|------|
| `UseVOSK` | bool | false | VOSKオフライン認識を有効化 |
| `UseYukarinette` | bool | false | ゆかりねっと連携を有効化 |
| `UseYukarinetteExtend` | bool | false | ゆかりねっと拡張モード |
| `UseWebRecogExtend` | bool | false | Web認識拡張を有効化 |
| `UsePlayBouyomi` | bool | false | 棒読みちゃんを有効化 |

**公式ドキュメント**: [音声認識できないとき](../startup/startup_asr.md)

---

## ウィンドウ設定

### メインウィンドウ

| 設定 | 型 | デフォルト | 説明 |
|-----|---|---------|------|
| `Top` | double | 0 | ウィンドウY位置 |
| `Left` | double | 0 | ウィンドウX位置 |
| `Width` | double | 510 | ウィンドウ幅 |
| `Height` | double | 890 | ウィンドウ高さ |
| `isAutoOpenInWindow` | bool | true | 字幕ウィンドウを自動で開く |
| `isTopmostWindow` | bool | true | 常に最前面に表示 |

### 字幕ウィンドウ位置

| 設定 | 型 | デフォルト | 説明 |
|-----|---|---------|------|
| `CaptionWindow_X` | int | -1 | 字幕ウィンドウX座標 |
| `CaptionWindow_Y` | int | -1 | 字幕ウィンドウY座標 |
| `CaptionWindow_CX` | int | -1 | 字幕ウィンドウ幅 |
| `CaptionWindow_CY` | int | -1 | 字幕ウィンドウ高さ |
| `CaptionWindow_Flags` | int | 0 | ウィンドウ状態フラグ |

### ブラウザ設定

| 設定 | 型 | デフォルト | 説明 |
|-----|---|---------|------|
| `BrowserPath_Edge` | string | (パス) | Edgeブラウザパス |
| `UseExternalBrowser` | bool | true | 外部ブラウザを使用 |
| `UseChrome` | bool | true | Chromeを優先 |
| `BrowserWidth` | int | 800 | ブラウザウィンドウ幅 |
| `BrowserHeight` | int | 400 | ブラウザウィンドウ高さ |
| `isBrowserSizeLock` | bool | false | ブラウザサイズを固定 |
| `BrowserParam` | string | "" | ブラウザ起動パラメータ |

---

## 出力設定

### OBS連携

| 設定 | 型 | デフォルト | 説明 |
|-----|---|---------|------|
| `UseOBSOutput` | bool | false | OBSファイル出力を有効化 |
| `OBSOutputDir` | string | "" | OBS出力ディレクトリ |

**公式ドキュメント**: [OBSできれいに出す](../cs/cs_obs.md)

### 行数制限

| 設定 | 型 | デフォルト | 説明 |
|-----|---|---------|------|
| `ViewAtLimitLine0` | bool | true | 行制限1を有効化 |
| `ViewAtLimitLine1` | bool | false | 行制限2を有効化 |
| `ViewAtLimitLine2` | bool | false | 行制限3を有効化 |
| `LimitDialogMode` | int | 0 | ダイアログ制限モード |

---

## プラグイン設定

| 設定 | 型 | デフォルト | 説明 |
|-----|---|---------|------|
| `PluginEnableList` | string | "{}" | 有効プラグインのJSON |
| `HideNotUsePlugin` | bool | false | 無効プラグインを非表示 |
| `LoadMissPluginMode` | bool | false | 読み込み失敗プラグインをスキップ |
| `LoadingPluginName` | string | "" | 現在読み込み中のプラグイン名 |

**公式ドキュメント**: [プラグインの使い方](../plugin/enabled.md)

---

## ユーザープロファイル

| 設定 | 型 | デフォルト | 説明 |
|-----|---|---------|------|
| `UserID` | string | "" | ユーザー識別子 |
| `MyUserID` | string | "" | カスタムユーザーID |
| `TalkerName` | string | "" | 表示名（話者名） |
| `TalkerImageDataDir` | string | "" | プロファイル画像ディレクトリ |
| `SharingUserData` | string | "" | 共有ユーザーデータ |
| `isIPAddressFullOpen` | bool | false | 全IP接続を許可 |

---

## システム設定

| 設定 | 型 | デフォルト | 説明 |
|-----|---|---------|------|
| `DebugOption` | bool | false | デバッグモードを有効化 |
| `isOffSystemMessage` | bool | false | システムメッセージを無効化 |
| `MuteStatus` | bool | false | グローバルミュート状態 |
| `isSavingMute` | bool | true | ミュート状態を保持 |
| `UpdatedCounter` | int | 0 | アップデート確認カウンタ |
| `AmbasadorName` | int | 0 | アンバサダーキャラクターID |

---

## UI状態（設定パネル展開状態）

| 設定 | 型 | デフォルト | 説明 |
|-----|---|---------|------|
| `ExpandProfile` | bool | false | プロファイルセクション展開 |
| `ExpandShowLayout` | bool | false | レイアウトセクション展開 |
| `ExpandTranslate` | bool | false | 翻訳セクション展開 |
| `ExpandCommonSetting` | bool | false | 共通設定セクション展開 |
| `ExpandRecognitionSelect` | bool | false | 認識設定セクション展開 |
| `ExpandFontSetting` | bool | false | フォントセクション展開 |
| `ExpandColorSettings` | bool | false | 色設定セクション展開 |
| `ExpandDesignCustom` | bool | false | デザインセクション展開 |
| `ExpandShowTiming` | bool | false | タイミングセクション展開 |

---

## 設定カテゴリ別まとめ

### プロファイル関連
- `TalkerName`, `TalkerImageDataDir`, `UserID`, `MyUserID`

### レイアウト関連
- `LayoutID`, `SelectLineStyle`, `ShowCaptionMode`

### 翻訳関連
- `Translator1`～`4`, `NativeLanguage`, `TranslationLanguage1`～`4`
- すべての `*APIKey*` 設定

### フォント関連
- `FontItem`, `FontItem2`～`5`, `FontSize`, `FontSize2`～`5`
- `letterSpacing`, `ExtendFontAdjust`

### 色関連
- すべての `*Color*` 設定, `BorderSize`, `ExtendColorAdjust`

### タイミング関連
- `KeepTime`, `ScrollTime`, `rb_Plugin_*` 設定

### 認識関連
- `UseUDtalk`, `UseVOSK`, `UseYukarinette`, `UseWebRecogExtend`
- `UDtalkIPAddress`, `AddLocalUDtalkIP`

---

## 関連ドキュメント

- [INDEX](./INDEX.md) - 全体案内
- [クイックスタートシナリオ](./QUICKSTART_SCENARIOS.md) - ユースケース別設定例
- [プラグインリファレンス](./PLUGINS_REFERENCE.md) - プラグインGUI詳細
- [GUIリファレンス](./YNC_NEO_GUI_REFERENCE.md) - 本体GUI操作
- [公式: 標準設定項目](../startup/startup_basic.md)
- [公式: オプション設定](../startup/startup_option.md)
