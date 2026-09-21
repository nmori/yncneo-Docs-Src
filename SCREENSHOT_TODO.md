# スクリーンショット撮り直しTODO

このファイルはドキュメント作成者向けのメモです。`docs/` の外に置いてあるため、サイトには公開されません。

各ページの該当箇所にも `<!-- TODO: ... -->` のコメントを入れてあります。

## 撮り直しが必要（内容が変わっている）

| 画像 | 撮影時点 | 撮り直しの理由 | 使っているページ |
|:--|:--|:--|:--|
| `docs/startup/images/startup_menu1.png` | v2.3.59 | 左メニューの構成が変わった（グループ名・項目名） | startup_basic.md |
| `docs/startup/images/startup_menu3.png` | v2.3.59 | レイアウトの選択肢が増えた（36種） | startup_basic.md |
| `docs/startup/images/startup_menu4.png` | v2.3.59 | 翻訳エンジンに Parapper翻訳 が追加された | startup_basic.md |
| `docs/startup/images/startup_menu5.png` | v2.3.59 | 音声認識に Parapper / Windows11音声認識 が追加された（計9種） | startup_basic.md |
| `docs/startup/images/startup_menu9.png` | v2.3.59 | クイックボタンの並びが変わった（「支援状態」「？」が無くなり、手動入力枠・マニュアル・プラグイン一覧が入った） | startup_basic.md |
| `docs/startup/images/startup_menu11.png` | v2.3.59 | 簡易設定の項目が11件になった | startup_basic.md |
| `docs/startup/images/startup_option3.png` | v2.3.59 | 翻訳APIオプションのラベル文言が変わった | startup_option.md |
| `docs/startup/images/startup_option4.png` | v2.3.59 | ブラウザのオプションに項目が増えた | startup_option.md |
| `docs/startup/images/startup_option6.png` | v2.3.59 | Gemini の新モデルと Parapper の Port 欄が増えた | startup_option.md |
| `docs/startup/images/startup_layout1.png` ～ `startup_layout6.png` | 2022-08 | 4年前の画面 | startup_layout.md |
| `docs/startup/images/startup_layout_p01.png` ～ `startup_layout_p15.png` | 2022-09 | 4年前。わんコメ側のテンプレートも更新されている可能性がある | startup_layout.md |
| `docs/startup/images/plugin_gas_p3.png` ～ `plugin_gas_p10.png` | 2022-10 | Google Apps Script の管理画面UIが変わっている | startup_gas.md |
| `docs/plugin/images/plugin_playvoice_p2.png` `p5.png` `p7.png` `p8.png` | v2.3系 | 読み上げ連携の設定画面が WPF に変わった（ボイスパレット / 6ページの詳細設定 / 条件ルールの一覧+詳細）。本文からは参照を外してある | plugin/plugin_playvoice.md |

## 未撮影（画像そのものが無い）

| 必要な画像 | 内容 | 使うページ |
|:--|:--|:--|
| `docs/startup/images/startup_layout7.png` | レイアウト「ショート」の表示例 | startup_layout.md |
| `docs/startup/images/startup_layout8.png` | レイアウト「ショート(動き控えめ)」の表示例 | startup_layout.md |
| `docs/plugin/images/plugin_niconama_p1.png` | ニコニコ生放送連携の設定画面 | plugin/plugin_niconama.md |
| `docs/plugin/images/plugin_infographics_p1.png` | InfoGraphics の設定画面 | plugin/plugin_infographics.md |
| `docs/plugin/images/plugin_talkhistory_p1.png` | 会話の記録：有効化 | plugin/plugin_talkhistory.md |
| `docs/plugin/images/plugin_talkhistory_p2.png` | 会話の記録：設定画面 | plugin/plugin_talkhistory.md |
| `docs/plugin/images/plugin_replacefwords_p1.png` | 不適切語の置換：有効化 | plugin/plugin_replacefwords.md |
| `docs/plugin/images/plugin_replacefwords_p2.png` | 不適切語の置換：設定画面 | plugin/plugin_replacefwords.md |
| `docs/plugin/images/plugin_dynamickeeptime_p1.png` | 表示時間の自動調整：有効化 | plugin/plugin_dynamickeeptime.md |
| `docs/plugin/images/plugin_dynamickeeptime_p2.png` | 表示時間の自動調整：設定画面 | plugin/plugin_dynamickeeptime.md |
| `docs/plugin/images/plugin_dynamickeeptime_graph.png` | 文字数と表示時間の関係グラフ | plugin/plugin_dynamickeeptime.md |
| `docs/plugin/images/plugin_playvoice_palette.png` | ボイスパレット（検索・エンジン絞り込み・お気に入り） | plugin/plugin_playvoice.md |
| `docs/plugin/images/plugin_playvoice_settings.png` | 詳細設定のホーム | plugin/plugin_playvoice.md |
| `docs/plugin/images/plugin_playvoice_rules.png` | 詳細設定の条件ルール | plugin/plugin_playvoice.md |
| `docs/plugin/images/plugin_playvoice_preset.png` | 設定プリセットの作成 | plugin/plugin_playvoice.md |

* 未出荷プラグイン（`plugin_MoviePickup.md` / `plugin_captioner.md`）の画像は不要です。配布していないため撮影できません。

## 撮り直したあとの作業

1. 上の表のパスにそのファイル名で置きます。
2. ページ内の `<!-- TODO: ... -->` コメントと、その下の `<!-- ![...](...) -->` のコメント記号を外します。
3. このファイルの該当行を消します。

> **画像は補助という前提で書いています。**
> 本文は、スクリーンショットが無くても設定にたどり着けるように書いてあります（画面名 → メニュー項目 → 項目ラベルの順）。撮り直しは急ぎではありません。
