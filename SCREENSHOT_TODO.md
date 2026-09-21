# スクリーンショット撮り直しTODO

このファイルはドキュメント作成者向けのメモです。`docs/` の外に置いてあるため、サイトには公開されません。

各ページの該当箇所にも `<!-- TODO: ... -->` / `<!-- TODO(screenshot): ... -->` のコメントを入れてあります。
ドキュメントは 2026-09 に v2.3 / v3.0 へ分けました。**撮り直しの対象は `docs/v3.0/` 側だけ**です（`docs/v2.3/` は v2.3 時点の画面で凍結しているので、そのままにしてください）。

## 撮り直しが必要（内容が変わっている）

| 画像 | 撮影時点 | 撮り直しの理由 | 使っているページ |
|:--|:--|:--|:--|
| `docs/v3.0/startup/images/startup_menu1.png` | v2.3.59 | 左メニューの構成が変わった（グループ名・項目名） | v3.0/startup/startup_basic.md |
| `docs/v3.0/startup/images/startup_menu3.png` | v2.3.59 | レイアウトの選択肢が増えた（36種） | v3.0/startup/startup_basic.md |
| `docs/v3.0/startup/images/startup_menu4.png` | v2.3.59 | 翻訳エンジンに Parapper翻訳 が追加された | v3.0/startup/startup_basic.md |
| `docs/v3.0/startup/images/startup_menu5.png` | v2.3.59 | 音声認識に Parapper / Windows11音声認識 が追加された（計9種） | v3.0/startup/startup_basic.md |
| `docs/v3.0/startup/images/startup_menu9.png` | v2.3.59 | クイックボタンの並びが変わった（「支援状態」「？」が無くなり、手動入力枠・マニュアル・プラグイン一覧が入った） | v3.0/startup/startup_basic.md |
| `docs/v3.0/startup/images/startup_menu11.png` | v2.3.59 | 簡易設定の項目が11件になった | v3.0/startup/startup_basic.md |
| `docs/v3.0/startup/images/startup_option3.png` | v2.3.59 | 翻訳APIオプションのラベル文言が変わった | v3.0/startup/startup_option.md |
| `docs/v3.0/startup/images/startup_option4.png` | v2.3.59 | ブラウザのオプションに項目が増えた | v3.0/startup/startup_option.md |
| `docs/v3.0/startup/images/startup_option6.png` | v2.3.59 | Gemini の新モデルと Parapper の Port 欄が増えた | v3.0/startup/startup_option.md |
| `docs/v3.0/startup/images/startup_layout1.png` ～ `startup_layout6.png` | 2022-08 | 4年前の画面 | v3.0/startup/startup_layout.md |
| `docs/v3.0/startup/images/startup_layout_p01.png` ～ `startup_layout_p15.png` | 2022-09 | 4年前。わんコメ側のテンプレートも更新されている可能性がある | v3.0/startup/startup_layout.md |
| `docs/v3.0/startup/images/plugin_gas_p3.png` ～ `plugin_gas_p10.png` | 2022-10 | Google Apps Script の管理画面UIが変わっている | v3.0/startup/startup_gas.md |

## 未撮影（画像そのものが無い）

| 必要な画像 | 内容 | 使うページ |
|:--|:--|:--|
| `docs/v3.0/startup/images/startup_layout7.png` | レイアウト「ショート」の表示例 | v3.0/startup/startup_layout.md |
| `docs/v3.0/startup/images/startup_layout8.png` | レイアウト「ショート(動き控えめ)」の表示例 | v3.0/startup/startup_layout.md |
| `docs/v3.0/plugin/images/plugin_talkhistory_p1.png` | 会話の記録：有効化 | v3.0/plugin/plugin_talkhistory.md |
| `docs/v3.0/plugin/images/plugin_replacefwords_p1.png` | 不適切語の置換：有効化 | v3.0/plugin/plugin_replacefwords.md |
| `docs/v3.0/plugin/images/plugin_dynamickeeptime_p1.png` | 表示時間の自動調整：有効化 | v3.0/plugin/plugin_dynamickeeptime.md |

* 未出荷プラグイン（`plugin_MoviePickup.md` / `plugin_captioner.md`）の画像は不要です。配布していないため撮影できません。

## 撮り直したあとの作業

1. 上の表のパスにそのファイル名で置きます。
2. ページ内の `<!-- TODO: ... -->` コメントと、その下の `<!-- ![...](...) -->` のコメント記号を外します。
3. このファイルの該当行を消します。

> **画像は補助という前提で書いています。**
> 本文は、スクリーンショットが無くても設定にたどり着けるように書いてあります（画面名 → メニュー項目 → 項目ラベルの順）。撮り直しは急ぎではありません。

## v3.0 で新しく撮る必要があるもの（2026-09 追加）

| 必要な画像 | 内容 | 使うページ |
|:--|:--|:--|
| `docs/v3.0/startup/images/startup_cockpit.png` | コックピット画面（いま出ている字幕・表示テスト・OBSのアドレス） | v3.0/startup/startup_basic.md |
| `docs/v3.0/startup/images/startup_design_chips.png` | 「見た目を調整する」を押した状態のボタン列（テンプレ/文字/色/配置/タイミング/表示内容） | v3.0/startup/startup_basic.md |
| `docs/v3.0/cs/images/cs_startup_wizard1.png` | セットアップ案内 ステップ 1/3（あなたのこと・やりたいこと） | v3.0/cs/cs_startup.md |
| `docs/v3.0/cs/images/cs_startup_wizard2.png` | セットアップ案内 ステップ 2/3（声を入れる） | v3.0/cs/cs_startup.md |
| `docs/v3.0/cs/images/cs_startup_wizard3.png` | セットアップ案内 ステップ 3/3（配信ソフトに出す） | v3.0/cs/cs_startup.md |
| `docs/v3.0/startup/images/startup_migrate_v23.png` | 「設定保存・復元」の v2.3設定を移行 ボタンと確認ダイアログ | v3.0/startup/startup_profile.md |
| `docs/v3.0/startup/images/startup_layout_extpack.png` | ext-pack のテンプレート一覧（アイコン付き） | v3.0/startup/startup_layout.md |

## 撮影済み（2026-09-22、プラグインの試験用ハーネスで撮影）

プラグインの設定画面は、ソース側の撮影ハーネスで撮って `docs/v3.0/plugin/images/v30/` に置きました（127 枚）。
撮り直すときは同じ手順で撮れます。

* 共通の設定画面: `Machan2017/tools/PluginSettingsProbe`（`<hostBin> <plugin.dll> <outDir> light`）
  * ホストは **Debug ビルド**の `YNC_Neo/bin/x64/Debug` を使う（Release は難読化されていてリソースが引けない）
  * 出力先がそのまま設定フォルダになるので、見本の規則ファイル（`<Plugin_Tag>_rule.config` など）を先に置くと、表に中身が入った絵になる
* 読み上げ: `Plugin_PlayVoice/tools/PaletteProbe`（ボイス一覧 JSON を渡すとパレットと詳細設定 7 ページを撮る）

**公開していない画面**（説明文やフォルダ欄に設定フォルダの場所＝ユーザー名が入る、または撮影環境の情報が写るため）:
MIDI 入力「割り当て」、OBS 連携 WSv4「シーン切り替え」、Python 連携、わんコメ連携「わんコメから受ける」、更新通知、MTG カード「OBS へ渡す」。
実機で、人に見せてよいフォルダ構成の PC から撮ってください。

置き換えた項目（旧 TODO）:
| `docs/v3.0/plugin/images/plugin_playvoice_p2.png` `p5.png` `p7.png` `p8.png` | v2.3系 | 読み上げ連携の設定画面が WPF に変わった（ボイスパレット / 6ページの詳細設定 / 条件ルールの一覧+詳細）。本文からは参照を外してある | v3.0/plugin/plugin_playvoice.md |
| `docs/v3.0/plugin/images/plugin_niconama_p1.png` | ニコニコ生放送連携の設定画面 | v3.0/plugin/plugin_niconama.md |
| `docs/v3.0/plugin/images/plugin_infographics_p1.png` | InfoGraphics の設定画面 | v3.0/plugin/plugin_infographics.md |
| `docs/v3.0/plugin/images/plugin_talkhistory_p2.png` | 会話の記録：設定画面 | v3.0/plugin/plugin_talkhistory.md |
| `docs/v3.0/plugin/images/plugin_replacefwords_p2.png` | 不適切語の置換：設定画面 | v3.0/plugin/plugin_replacefwords.md |
| `docs/v3.0/plugin/images/plugin_dynamickeeptime_p2.png` | 表示時間の自動調整：設定画面 | v3.0/plugin/plugin_dynamickeeptime.md |
| `docs/v3.0/plugin/images/plugin_dynamickeeptime_graph.png` | 文字数と表示時間の関係グラフ | v3.0/plugin/plugin_dynamickeeptime.md |
| `docs/v3.0/plugin/images/plugin_playvoice_palette.png` | ボイスパレット（検索・エンジン絞り込み・お気に入り） | v3.0/plugin/plugin_playvoice.md |
| `docs/v3.0/plugin/images/plugin_playvoice_settings.png` | 詳細設定のホーム | v3.0/plugin/plugin_playvoice.md |
| `docs/v3.0/plugin/images/plugin_playvoice_rules.png` | 詳細設定の条件ルール | v3.0/plugin/plugin_playvoice.md |
| `docs/v3.0/plugin/images/plugin_playvoice_preset.png` | 設定プリセットの作成 | v3.0/plugin/plugin_playvoice.md |
| `docs/v3.0/plugin/images/plugin_ux_common.png` | 新しいプラグイン設定画面（WPF 共通土台）の見本 | v3.0/plugin/enabled.md ほか |
| `docs/v3.0/plugin/images/plugin_ux_table.png` | 新しい設定画面の規則の表（列幅が内容に合わせて配分されるもの） | v3.0/plugin/plugin_regexp.md ほか |
